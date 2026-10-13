---
title: JavaScript Quickstart
mkdocs_template: quick-start
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/quick-starts/javascript.md
quick_start:
  what_you_will_learn:
    - Create new single-page JavaScript app
    - Install WSO2 Identity Platform JavaScript SDK
    - Add user login and logout
    - Display user profile information
  prerequisites:
    - About 15 minutes
    - <a href='{{ base_path }}/get-started/create-identity-platform-account/'>WSO2 Identity Platform account</a>
    - Install <a href='https://nodejs.org/en/download/package-manager' target='_blank' rel='noopener noreferrer'>Node.js</a> on your system.
    - Make sure you have a JavaScript package manager like <code>npm</code>, <code>yarn</code>, or <code>pnpm</code>.
    - A favorite text editor or IDE
  source_code: <a href='https://github.com/dasuni-30/asgardeo-javascript-vite-app/tree/master' target='_blank' class='github-icon'>JavaScript App Sample</a>
---

# JavaScript Quickstart

Welcome to the JavaScript Quickstart guide! In this document, you will learn to build a single-page JavaScript app, add user login and display user profile information using WSO2 Identity Platform.



## Configure an Application in WSO2 Identity Platform

- Sign into WSO2 Identity Platform console and navigate to **Applications > New Application**.
- Select **Single Page Application** and complete the wizard popup by providing a suitable name and an authorized redirect URL.

:::note

**name:** <DeploymentValue cloud="asgardeo" selfHosted="is" />-javascript

**Authorized redirect URL:** http://localhost:5173

:::

Note down the following values from the **Protocol** tab of the registered application. You will need them to configure  WSO2 Identity Platform JavaScript SDK.

- **`client-id`** from the **Protocol** tab.
- **The name of your WSO2 Identity Platform organization**

:::info


The authorized redirect URL determines where WSO2 Identity Platform should send users after they successfully log in. Typically, this will be the web address where your app is hosted. For this guide, we'll use`http://localhost:5173`, as the sample app will be accessible at this URL.

:::

## Create a JavaScript app using Vite

Create (a.k.a scaffold) your new JavaScript app using Vite.

<Tabs>
<TabItem value="tab-0" label="npm">


```bash
npm create vite@latest <PRODUCT>-javascript -- --template vanilla

cd <PRODUCT>-javascript

npm install

npm run dev
```

</TabItem>
<TabItem value="tab-1" label="yarn">


```bash
yarn create vite@latest <PRODUCT>-javascript -- --template vanilla

cd <PRODUCT>-javascript

yarn install

yarn dev
```

</TabItem>
<TabItem value="tab-2" label="pnpm">


```bash
pnpm create vite@latest <PRODUCT>-javascript -- --template vanilla

cd <PRODUCT>-javascript

pnpm install

pnpm dev
```

</TabItem>
</Tabs>

## Install @asgardeo/auth-spa

WSO2 Identity Platform JavaScript SDK provides all the components and hooks you need to integrate WSO2 Identity Platform into your app. To get started, simply add the WSO2 Identity Platform JavaScript SDK to the project. Make sure to stop the dev server started in the previous step.

<Tabs>
<TabItem value="tab-0" label="npm">


```bash
npm install @asgardeo/auth-spa

```

</TabItem>
<TabItem value="tab-1" label="yarn">


```bash
yarn add @asgardeo/auth-spa
```

</TabItem>
<TabItem value="tab-2" label="pnpm">


```bash
pnpm add @asgardeo/auth-spa
```

</TabItem>
</Tabs>

## Initialize @asgardeo/auth-spa

Replace the existing code of the `main.jsx` file with the following code to initialize `AuthSPAClient`.

:::warning


Replace below placeholders with your registered organization name in WSO2 Identity Platform and the generated`client-id` from the app you registered in WSO2 Identity Platform.

- `<your-app-client-id>`
- `<CONTENT_SDKCONFIG_BASEURL>`

:::

```javascript title="src/main.js"

import { AsgardeoSPAClient } from "@asgardeo/auth-spa";

const auth = AsgardeoSPAClient.getInstance();

await auth.initialize({
  signInRedirectURL: "http://localhost:5173",
  signOutRedirectURL: "http://localhost:5173",
  clientID: "<your-app-client-id>",
  baseUrl: "<CONTENT_SDKCONFIG_BASEURL>",
  scope: ["openid", "profile"]
});

```

## Add login and logout link to your app

The `AsgardeoSPAClient` provides `signIn` and `signOut` methods and access to the authentication state. Add the following code to the `main.js` file to conditionally render a login or logout button based on whether the user is authenticated.

```javascript title="src/main.js" {1,14-30,32-41,43-49}

import { AsgardeoSPAClient, SPAUtils } from "@asgardeo/auth-spa";

const auth = AsgardeoSPAClient.getInstance();

await auth.initialize({
  signInRedirectURL: "http://localhost:5173",
  signOutRedirectURL: "http://localhost:5173",
  clientID: "<your-app-client-id>",
  baseUrl: "<CONTENT_SDKCONFIG_BASEURL>",
  scope: ["openid", "profile"]
});

(async () => {
  let user = undefined;

  if (SPAUtils.hasAuthSearchParamsInURL()) {
    user = await auth.signIn({ callOnlyOnRedirect: true });
  } else {
    user = await auth.trySignInSilently();
  }

  if (user) {
    document.getElementById("authenticated-view").style.display = "block";
    document.getElementById("unauthenticated-view").style.display = "none";
  } else {
    document.getElementById("authenticated-view").style.display = "none";
    document.getElementById("unauthenticated-view").style.display = "block";
  }
})();

document.querySelector('#app').innerHTML = `
  <div>
    <div id="authenticated-view" style="display: none">
      <button id="logout">Log Out</button>
    </div>
    <div id="unauthenticated-view" style="display: none">
      <button id="login">Log In</button>
    </div>
  </div>
`;

document.getElementById("login").addEventListener("click", async () => {
  auth.signIn();
});

document.getElementById("logout").addEventListener("click", async () => {
  auth.signOut();
});

```

Visit your app's homepage at [http://localhost:5173](http://localhost:5173).

:::warning


You need to create a test user in WSO2 Identity Platform by following this [guide](../guides/users/manage-users.md#onboard-single-user) to tryout login and logout features.

:::

## Display logged in user details

Modify the code as below to see logged in user details.

```javascript title="src/main.js" {26,36}

import { AsgardeoSPAClient, SPAUtils } from "@asgardeo/auth-spa";

const auth = AsgardeoSPAClient.getInstance();

await auth.initialize({
  signInRedirectURL: "http://localhost:5173",
  signOutRedirectURL: "http://localhost:5173",
  clientID: "<your-app-client-id>",
  baseUrl: "<CONTENT_SDKCONFIG_BASEURL>",
  scope: ["openid", "profile"]
});


(async () => {
  let user = undefined;

  if (SPAUtils.hasAuthSearchParamsInURL()) {
    user = await auth.signIn({ callOnlyOnRedirect: true });
  } else {
    user = await auth.trySignInSilently();
  }

  if (user) {
    document.getElementById("authenticated-view").style.display = "block";
    document.getElementById("unauthenticated-view").style.display = "none";
    document.getElementById("username").innerHTML = "Welcome " + user.username;
  } else {
    document.getElementById("authenticated-view").style.display = "none";
    document.getElementById("unauthenticated-view").style.display = "block";
  }
})();

document.querySelector('#app').innerHTML = `
  <div>
    <div id="authenticated-view" style="display: none">
      <p id="username"></p>
      <button id="logout">Log Out</button>
    </div>
    <div id="unauthenticated-view" style="display: none">
      <button id="login">Log In</button>
    </div>
  </div>
`;

document.getElementById("login").addEventListener("click", async () => {
  auth.signIn();
});

document.getElementById("logout").addEventListener("click", async () => {
  auth.signOut();
});


```
