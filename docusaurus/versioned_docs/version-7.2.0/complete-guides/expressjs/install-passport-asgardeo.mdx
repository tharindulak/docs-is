---
title: Configure Passport Asgardeo
mkdocs_template: complete-guide
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/complete-guides/expressjs/install-passport-asgardeo.md
---

## Install Passport and Passport WSO2 Identity Platform

For this integration, we are going to use Passport and the passport-asgardeo strategy. Install the dependencies using the following commands:

```bash
npm install passport
npm install @asgardeo/passport-asgardeo
npm install dotenv
```

:::info


[Passport](https://www.passportjs.org) is an authentication middleware for Node.js that is widely used in the Node.js community. It provides a simple way to authenticate requests and manage sessions. Passport strategies are used to authenticate requests. Passport WSO2 Identity Platform strategy is a Passport strategy that allows you to authenticate with OIDC using WSO2 Identity Server.

:::

## Configure AsgardeoStrategy

Next, let's create a file that will contain authentication related functionality:

```bash
touch routes/auth.js
```

Add the following code to the `routes/auth.js` file:

```javascript
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
      scope: ["profile"],
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
      });
    }
  )
);
```

Next, let's create a `.env` file to store the domain, client ID, and client secret from the WSO2 Identity Server Application as environment variables:

```bash
touch .env
```

Add the following environment variables to the `.env` file:

```bash
CLIENT_ID=<YOUR_CLIENT_ID>
CLIENT_SECRET=<YOUR_CLIENT_SECRET>
```

Add the following line to the start of the `app.js` file to load the environment variables:

```javascript {1}
require("dotenv").config();

var createError = require("http-errors");
var express = require("express");
...
```

Now that the strategy is configured, we are ready to add login routes to the app.
