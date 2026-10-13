---
title: Token Exchange for AI Agents
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/agentic-ai/ai-agents/token-exchange-for-agents.md
---

# Token Exchange for AI Agents


This guide walks you through how an AI agent can act on behalf of a user by exchanging a token that the user already holds. The flow uses the [token exchange grant](../../authentication/configure-token-exchange.md), as defined in the [OAuth 2.0 Token Exchange specification (RFC 8693)](https://datatracker.ietf.org/doc/html/rfc8693).

The issued token identifies the user in the `sub` claim and records the agent as the acting party in the `act` claim. A resource server can then see both identities in a single token.





<Applies to="Self-hosted">

:::note

This feature is available from **update level 7.3.0.18** onwards. See the instructions on [updating WSO2 products](https://updates.docs.wso2.com/en/latest/).

:::

</Applies>



:::note[Agent friendly delegation mechanism]

- This flow does **not use redirects** and needs **no new user interaction**.
- It is suited to bringing an agent into work the user has already authorized.
- The agent reuses the token it already obtained through its own [authentication flow](agent-authentication.md#ai-agent-acting-on-its-own).

:::

---

## How the flow works

![Agent Delegation via Token Exchange Flow Diagram](../../../../assets/img/guides/agentic-ai/ai-agent-token-exchange-flow.png)

As shown in the above sequence diagram, the flow proceeds as follows.

1. **Agent Authentication**
   The agent authenticates with its **Agent ID** and **Agent Secret** and obtains its own access token, as described in [AI agent acting on its own](agent-authentication.md#ai-agent-acting-on-its-own). This token becomes the `actor_token`.

2. **Task Delegation**
   The user, or an agent earlier in the chain, delegates a task to the agent and provides the subject token. The subject token identifies the user on whose behalf the agent acts. WSO2 Identity Platform accepts a token issued by itself or by a trusted token issuer, as described in [Token exchange flows](../../authentication/configure-token-exchange.md#token-exchange-flows).

3. **Token Exchange Request**
   The agent sends both tokens to the token endpoint using the token exchange grant.

4. **Validation**
   WSO2 Identity Platform validates both tokens, resolves the agent from the `sub` claim of the actor token, and verifies that the agent is a registered and active identity in the organization.

5. **Delegated Token Issuance**
   WSO2 Identity Platform issues an access token that carries the user in `sub` and the agent in `act.sub`.

6. **Authorized Request**
   The agent calls the protected resource with the delegated token. The resource server can authorize the request against the user's identity while attributing the action to the agent.

## Requesting a delegated token

:::note[Before you begin]

- Enable the token exchange grant for the application that requests the token, as described in [Enable token exchange in your app](../../authentication/configure-token-exchange.md#enable-token-exchange-in-your-app).
- Configure the agent's application to issue `JWT` access tokens. WSO2 Identity Platform rejects opaque actor tokens.

:::

Send both tokens to the token endpoint.

<Tabs>
<TabItem value="tab-0" label="Request Format">


```bash
curl --location '<API_BASE_PATH>/oauth2/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Authorization: Basic <base64 Encoded (clientId:clientSecret)>' \
--data-urlencode 'grant_type=urn:ietf:params:oauth:grant-type:token-exchange' \
--data-urlencode 'subject_token={user_token}' \
--data-urlencode 'subject_token_type=urn:ietf:params:oauth:token-type:jwt' \
--data-urlencode 'actor_token={agent_token}' \
--data-urlencode 'actor_token_type=urn:ietf:params:oauth:token-type:jwt' \
--data-urlencode 'requested_token_type=urn:ietf:params:oauth:token-type:access_token' \
--data-urlencode 'scope={requested_scopes}'
```

</TabItem>
</Tabs>

The request contains the following delegation parameters:

<table>
    <tr>
        <th>Parameter</th>
        <th>Description</th>
    </tr>
    <tr>
        <td><code>subject_token</code></td>
        <td>A JWT token that identifies the user on whose behalf the agent acts.</td>
    </tr>
    <tr>
        <td><code>actor_token</code></td>
        <td>A JWT token issued by WSO2 Identity Platform for the agent.</td>
    </tr>
    <tr>
        <td><code>actor_token_type</code></td>
        <td>Should be <code>urn:ietf:params:oauth:token-type:access_token</code> or
        <code>urn:ietf:params:oauth:token-type:jwt</code>.</td>
    </tr>
</table>

:::note[Scopes of the delegated token]

When WSO2 Identity Platform issues the subject token, it limits the scopes of the delegated token to the scopes granted to the subject token. An agent can narrow the scopes it receives, but it can't widen them beyond what the user already approved.


To prevent WSO2 Identity Platform from issuing scopes when a trusted token issuer issues the subject token, see [Restrict scope issuance for federated tokens](../../authentication/configure-token-exchange.md#restrict-scope-issuance-for-federated-tokens).

:::
    

## The delegated token

The decoded token identifies the user in `sub` and the agent in `act.sub`.

```json
{
  "sub": "<user_identifier>",
  "act": {
    "sub": "<agent_identifier>"
  },
  ...
}
```

A resource server can use the `act` claim to record which agent acted for the user, or to apply policies that depend on the acting agent. This gives you an audit trail that attributes the action to the agent independently of the user, as described in [Comprehensive auditing and explainability](index.md#comprehensive-auditing-and-explainability).

## Chaining delegation across agents

When an agent hands a task to another agent, the second agent exchanges the delegated token again with its own actor token. The new agent becomes the current acting party and the existing `act` claim nests under it, so the token carries the full chain.

```json
{
  "sub": "<user_identifier>",
  "act": {
    "sub": "<second_agent_identifier>",
    "act": {
      "sub": "<first_agent_identifier>"
    }
  },
  ...
}
```

The most recent agent appears at the top level of the chain. When the request presents no actor token, WSO2 Identity Platform carries the existing chain forward unchanged. An agent that re-exchanges a token it received can't alter the chain behind it.

To learn more about the delegation model and the `act` claim, see [Delegation](../../authorization/delegation.md).
