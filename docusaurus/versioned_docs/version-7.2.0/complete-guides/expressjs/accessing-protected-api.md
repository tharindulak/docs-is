---
title: Accessing protected API
mkdocs_template: complete-guide
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/complete-guides/expressjs/accessing-protected-api.md
---

In this section, we will focus on how to call a secure API from your Express.js app using the other token—the access token.

For simplicity, let's assume that the APIs we’re calling are secured by the same Identity Provider (IdP) and use the same issuer— in this case, the same WSO2 Identity Server organization. This is typical when Express.js apps are interacting with internal APIs within the same organization.

:::tip[Tip]


If your app needs to call APIs secured by a different IdP, you’ll need to exchange your current access token for a new one issued by the IdP securing those APIs. This can be done using the OAuth2 token exchange grant type or other supported grant types. We will cover these scenarios in a separate guide.

:::

In the following example we'll see how to call a protected API endpoint, such as scim2/Me (to get the user profile details after signing in). In this case, the SCIM 2 endpoint is secured by the same WSO2 Identity Server organization. WSO2 Identity Server provides a SCIM 2 API for managing users within your organization. While user management with SCIM 2 is a topic for a different guide, we will use the API as part of our current guide.

If you observe the `routes/auth.js` file, you can see that the WSO2 Identity Server strategy loads the access token in the `accessToken` parameter of the `verify` callback. This access token can be used to call the protected API.

Let's return the access token from the callback and serialize it to the session.

You will notice that the WSO2 Identity Server documentation lists the scopes required to access the SCIM 2 API. In this case, the `internal_login` scope is required to access the `/scim2/Me` endpoint.

We will add the `internal_login` scope as well to the `scope` parameter in the WSO2 Identity Server strategy configuration.

```javascript {19,34,47}
var passport = require("passport");
var AsgardeoStrategy = require("@asgardeo/passport-asgardeo");
const BASE_URL = "https://localhost:9443";

passport.use(
  new AsgardeoStrategy(
    {
      issuer:
        BASE_URL + "/oauth2/token",
      authorizationURL:
        BASE_URL + "/oauth2/authorize",
      tokenURL:
        BASE_URL + "/oauth2/token",
      userInfoURL:
        BASE_URL + "/oauth2/userinfo",
      clientID: process.env.CLIENT_ID,
      clientSecret: process.env.CLIENT_SECRET,
      callbackURL: "/oauth2/redirect",
      scope: ["profile internal_login"],
    },
    function verify(
      issuer,
      uiProfile,
      idProfile,
      context,
      idToken,
      accessToken,
      refreshToken,
      params,
      verified
    ) {
      return verified(null, {
        uiProfile: uiProfile,
        accessToken: accessToken,
      });
    }
  )
);

passport.serializeUser(function (user, cb) {
  process.nextTick(function () {
    cb(null, {
      id: user?.uiProfile?.id,
      username: user?.uiProfile?._json?.username,
      givenName: user?.uiProfile?.name?.givenName,
      familyName: user?.uiProfile?.name?.familyName,
      accessToken: user?.accessToken,
    });
  });
});

passport.deserializeUser(function (user, cb) {
  process.nextTick(function () {
    return cb(null, user);
  });
});
...
```

Now we can use the access token to call the protected API. Let's modify the `routes/users.js` to try out the SCIM 2 API call.

```javascript {4,8-35}
var express = require("express");
var ensureLogIn = require("connect-ensure-login").ensureLoggedIn;
var router = express.Router();
const BASE_URL = "https://localhost:9443";

var ensureLoggedIn = ensureLogIn();
/* GET users listing. */
router.get("/", ensureLoggedIn, async function (req, res, next) {
  try {
    console.log("Calling scim2/Me endpoint");
    const response = await fetch(
      BASE_URL + "/scim2/Me",
      {
        method: "GET",
        headers: {
          Accept: "application/scim+json",
          "Content-Type": "application/scim+json",
          Authorization: `Bearer ${req?.user?.accessToken}`,
        },
      }
    );

    if (!response.ok) {
      throw new Error(
        "Response: " + JSON.stringify(await response.json(), null, 2)
      );
    }

    console.log(
      "Protected data fetched. Response: " +
        JSON.stringify(await response.json(), null, 2)
    );
  } catch (error) {
    console.error("Failed to fetch protected data: ", error);
  }

  res.send("This is a protected resource");
});

module.exports = router;
```

When you login to the application and navigate to the `/users` route, you will see that the SCIM 2 API is called and the protected data is fetched successfully. The response will be logged in the terminal.

![Accessing protected API](../../../../assets/_versions/7.2.0/img/complete-guides/nodejs/image16.png)

In this step, we have successfully called a protected API from our Express.js app using the access token. This is a common requirement in many applications. Next you can look into additional features that WSO2 Identity Server offers to make the authentication flow more diverse and secure.
