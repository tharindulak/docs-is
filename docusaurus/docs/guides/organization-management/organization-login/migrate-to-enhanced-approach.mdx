---
title: Migrate applications to enhanced approach
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/guides/organization-management/organization-login/migrate-to-enhanced-approach.md
---

# Migrate applications to enhanced approach

Enhanced organization authentication changes how WSO2 Identity Platform routes B2B login requests. This page describes what to update when moving an application from the legacy federation-based approach to enhanced organization authentication.

:::warning

Switching the same application between organization login approaches is not recommended. Create a new application and configure it with enhanced organization authentication instead of modifying an existing one.

:::

---

## What changes

The following areas require attention when migrating to enhanced organization authentication.

### Passing discovery parameters

In the legacy approach, routing users to their organization required both `fidp=OrganizationSSO` and a discovery parameter. Under enhanced organization authentication, `fidp` is not required — passing a discovery parameter alone is enough. WSO2 Identity Platform resolves the organization from the parameter and routes the user automatically.

<Tabs>
<TabItem value="tab-0" label="Before">


```bash
https://<HOST_NAME>/t/<root_org_handle>/oauth2/authorize?
client_id=<client_id>
&redirect_uri=<redirect_url>
&scope=<scopes>
&response_type=code
&fidp=OrganizationSSO
&orgId=<organization_id>
```

</TabItem>
<TabItem value="tab-1" label="After">


```bash
https://<HOST_NAME>/t/<root_org_handle>/oauth2/authorize?
client_id=<client_id>
&redirect_uri=<redirect_url>
&scope=<scopes>
&response_type=code
&orgId=<organization_id>
```

</TabItem>
</Tabs>

### Conditional authentication scripts

Review any conditional authentication scripts configured for your application. In the legacy approach, the Organization SSO authenticator was a federated IdP (`SSO`). Under enhanced organization authentication, the authenticator becomes a local authenticator (`OrganizationIdentifierHandler`). Update any place in your scripts where the `SSO` IdP is selected or where authenticator properties are set — replace references to the federated `SSO` authenticator with the local `OrganizationIdentifierHandler`.

### Custom parameter forwarding

In the legacy approach, custom query parameters on the authorize request were not automatically forwarded to the organization's authentication flow. Scripts explicitly forwarded them using `ssoAdditionalParams`. Under enhanced organization authentication, custom parameters are forwarded automatically — this script logic should be removed since the SSO IdP is no longer applicable.
