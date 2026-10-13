---
title: Express.js Quickstart
mkdocs_template: quick-start
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/quick-starts/expressjs.md
quick_start:
  what_you_will_learn:
    - Create new Express.js app
    - Install Passport Asgardeo strategy <a href='https://www.npmjs.com/package/@asgardeo/passport-asgardeo' target='_blank' rel='noopener noreferrer'>@asgardeo/passport-asgardeo</a>
    - Add user login and logout
    - Display user profile information
  prerequisites:
    - About 15 minutes
    - <a href='{{ base_path }}/get-started/quick-set-up/'>Set-up {{ product_name }}</a>
    - Install <a href='https://nodejs.org/en/download/package-manager' target='_blank' rel='noopener noreferrer'>Node.js</a> on your system.
    - Make sure you have a JavaScript package manager like <code>npm</code>, <code>yarn</code>, or <code>pnpm</code>.
    - A favorite text editor or IDE
  source_code: <a href='https://github.com/asgardeo-samples/asgardeo-javascript-samples/tree/main/passport-asgardeo-sample' target='_blank' class='github-icon'>WSO2 IS Express.js Sample</a>
---

# Express.js Quickstart

Welcome to the Express.js Quickstart guide! In this document, you will learn to build an Express.js app, add user login and display user profile information using WSO2 Identity Server.



## Configure an Application in WSO2 Identity Server

- Sign into WSO2 Identity Server console and navigate to **Applications > New Application.**
- Select **Traditional Web Application** and complete the wizard popup by providing a suitable name and an authorized redirect URL. (*Ensure that the protocol remains set to OpenID Connect (OIDC).)*

:::note

Name : is-expressjs

Authorized redirect URL: http://localhost:3000/oauth2/redirect, http://localhost:3000/

:::

:::info


The authorized redirect URL determines where WSO2 Identity Server should send users after they successfully log in. Typically, this will be the web address where your app is hosted. For this guide, we'll use `http://localhost:3000/oauth2/redirect` and http://localhost:3000 as the authorized redirect URL. The http://localhost:3000/ URL is used to redirect the user after logging out. 

:::

Make a note of the following values from the **Protocol** tab of the registered application. You will need them during the **Step 4**

- **`client-id`** from the **Protocol** tab.
- **`client-secret`** from the **Protocol** tab.

## Create an Express.js app

Create your new Express.js app using npx `express-generator` command.

<Tabs>
<TabItem value="tab-0" label="npm">


```bash
npx express-generator is-expressjs --view=ejs

cd is-expressjs

npm install

npm start
```

</TabItem>
<TabItem value="tab-1" label="yarn">


```bash
yarn dlx express-generator is-expressjs --view=ejs

cd is-expressjs

yarn install

yarn start
```

</TabItem>
<TabItem value="tab-2" label="pnpm">


```bash
pnpm dlx express-generator is-expressjs --view=ejs

cd is-expressjs

pnpm install

pnpm start
```

</TabItem>
</Tabs>

Navigate to [http://localhost:3000](http://localhost:3000) and you should see the sample app working in the browser.

## Install @asgardeo/passport-asgardeo

Passport WSO2 Identity Platform strategy is a Passport strategy that allows you to authenticate  using WSO2 Identity Server. To get started, simply add the Passport WSO2 Identity Platform strategy to the project together with the other required dependencies. Make sure to stop the dev server started in the previous step.

<Tabs>
<TabItem value="tab-0" label="npm">


```bash
npm install passport express-session dotenv @asgardeo/passport-asgardeo 

``` 

</TabItem>
<TabItem value="tab-1" label="yarn">


```bash
yarn add passport express-session dotenv @asgardeo/passport-asgardeo 

```

</TabItem>
<TabItem value="tab-2" label="pnpm">


```bash
pnpm add passport express-session dotenv @asgardeo/passport-asgardeo 

```

</TabItem>
</Tabs>

## Configure Passport WSO2 Identity Platform

Create `.env` environment properties file, and add the following  variables:

```bash
CLIENT_ID=<YOUR_CLIENT_ID>
CLIENT_SECRET=<YOUR_CLIENT_SECRET>
```

:::warning


Replace below placeholders with your registered organization name in WSO2 Identity Server and the generated`client-id` from the app you registered in WSO2 Identity Server.

- `<YOUR_CLIENT_ID>`
- `<YOUR_CLIENT_SECRET>`

:::


:::note

If running in a local development or testing environment using self-signed SSL certificates, application may fail to connect due to Transport Layer Security(TLS) certificate validation errors. To bypass this check add `NODE_TLS_REJECT_UNAUTHORIZED=0` to the `.env` file.

:::


Then, Add the following line to the start of the `app.js` file to load the environment variables from the `.env` file.

```javascript title="app.js" {1}
require("dotenv").config();

var createError = require("http-errors");
var express = require("express");
```

Next, create `routes/auth.js` file and add the following code to configure the app with the WSO2 Identity Server configuration parameters.

```javascript title="routes/auth.js"

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
            clientID:
                process.env.CLIENT_ID,
            clientSecret:
                process.env.CLIENT_SECRET,
            callbackURL:
                "/oauth2/redirect",
            scope:
                ["profile"],
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

## Add login and logout link to your app

Modify the `views/index.ejs` file with the following code to show the login and logout buttons.

```html title="views/index.ejs" {10-22}

<!DOCTYPE html>
<html>
  <head>
    <title><%= title %></title>
    <link rel='stylesheet' href='/stylesheets/style.css' />
  </head>
  <body>
    <h1><%= title %></h1>
    <p>Welcome to <%= title %></p>
    <% if (locals.user) { %>
      <div>
        <form action="/logout" method="post">
          <button type="submit">Logout</button>
        </form>
      </div>
    <% } else { %>
      <div>
        <form action="/login">
          <button type="submit">Login</button>
        </form>
      </div>
    <% } %>
  </body>
</html>

```

Next, modify the `routes/index.js` file to pass the user object to the view.

```javascript title="routes/index.js" {6}

var express = require('express');
var router = express.Router();

/* GET home page. */
router.get('/', function(req, res, next) {
  res.render('index', { title: 'Express', user: req.user });
});

module.exports = router;

```

Update the `routes/auth.js` file by adding following code at the end. This code creates two routes to handle login and request and response, and also configure Passport to manage the login session by adding serializeUser and deserializeUser functions.

```javascript title="routes/auth.js"

passport.serializeUser(function (user, cb) {
    process.nextTick(function () {
        cb(null, {
            id: user?.uiProfile?.id,
            username: user?.uiProfile?._json?.username,
        });
    });
});

passport.deserializeUser(function (user, cb) {
    process.nextTick(function () {
        return cb(null, user);
    });
});



var express = require("express");
var qs = require("querystring");
var router = express.Router();

router.get("/login", passport.authenticate("asgardeo"));

router.get(
    "/oauth2/redirect",
    passport.authenticate("asgardeo", {
        successRedirect: "/",
        failureRedirect: "/",
    })
);

router.post("/logout", function (req, res, next) {
    req.logout(function (err) {
        if (err) {
            return next(err);
        }
        var params = {
            post_logout_redirect_uri: "http://localhost:3000/",
            client_id: process.env.CLIENT_ID,
        };
        res.redirect(
            BASE_URL +
            "/oidc/logout?" +
            qs.stringify(params)
        );
    });
});

module.exports = router;

```

Finally, add these routes to our app by modifying the `app.js` file with the following highlighted code. This code defines a new auth router and add it to the app, and also configure session support for the app.

```javascript title="app.js" {7,8,12,25-32,36}

require("dotenv").config();
var createError = require('http-errors');
var express = require('express');
var path = require('path');
var cookieParser = require('cookie-parser');
var logger = require('morgan');
var session = require("express-session");
var passport = require("passport");

var indexRouter = require('./routes/index');
var usersRouter = require('./routes/users');
var authRouter = require("./routes/auth");

var app = express();

// view engine setup
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'ejs');

app.use(logger('dev'));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname, 'public')));
app.use(
  session({
    secret: "keyboard cat",
    resave: false,
    saveUninitialized: false,
  })
);
app.use(passport.authenticate("session"));

app.use('/', indexRouter);
app.use('/users', usersRouter);
app.use("/", authRouter);


// catch 404 and forward to error handler
app.use(function(req, res, next) {
  next(createError(404));
});

// error handler
app.use(function(err, req, res, next) {
  // set locals, only providing error in development
  res.locals.message = err.message;
  res.locals.error = req.app.get('env') === 'development' ? err : {};

  // render the error page
  res.status(err.status || 500);
  res.render('error');
});

module.exports = app;


```

Visit your app's homepage at [http://localhost:3000](http://localhost:3000)

:::warning


You need to create a test user in WSO2 Identity Server by following this [guide](../guides/users/manage-users.md#onboard-single-user) to tryout login and logout features.

:::

## Display logged in user details

Modify the code as below to see logged-in user details.

```html title="views/index.ejs" {11}

<!DOCTYPE html>
<html>
  <head>
    <title><%= title %></title>
    <link rel='stylesheet' href='/stylesheets/style.css' />
  </head>
  <body>
    <h1><%= title %></h1>
    <p>Welcome to <%= title %></p>
    <% if (locals.user) { %>
      <p>Hello <%= user.username %></p>
      <div>
        <form action="/logout" method="post">
          <button type="submit">Logout</button>
        </form>
      </div>
    <% } else { %>
      <div>
        <form action="/login">
          <button type="submit">Login</button>
        </form>
      </div>
    <% } %>
  </body>
</html>

```




:::tip[Tip]


In WSO2 Identity Server, the default certificate is a self signed certificate. This certificate needs to be added to the runtime path in order to avoid SSL errors.

Excute the below commands before running `npm start`

Naviate to the &lt;IS_HOME>/repository/resources/security directory and execute the following

```bash
keytool -export -alias wso2carbon -file carbon_public2.crt -keystore wso2carbon.p12 -storetype PKCS12 -storepass wso2carbon
```

Convert the certificate to X509 format.

```bash
openssl x509 -in carbon_public2.crt -inform der -outform pem -out certificate.pem
```

Navigate to the passport-wso2-sample home and execute the following
```bash
export NODE_EXTRA_CA_CERTS=./<PATH_TO_CERTIFICATE_FILE>/certificate.pem
```

:::
