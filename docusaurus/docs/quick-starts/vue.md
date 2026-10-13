---
title: Vue quickstart
mkdocs_template: quick-start
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/quick-starts/vue.md
quick_start:
  what_you_will_learn:
    - Create new Vue app using Vite
    - Install <a href='https://www.npmjs.com/package/@asgardeo/vue' target='_blank' rel='noopener noreferrer'>@asgardeo/vue</a> package
    - Add user sign-in and sign-out
    - Display user profile information
  prerequisites:
    - About 15 minutes
    - <a href='{{ base_path }}/get-started/create-identity-platform-account/'>WSO2 Identity Platform account</a>
    - Install <a href='https://nodejs.org/en/download/package-manager' target='_blank' rel='noopener noreferrer'>Node.js</a> on your system.
    - Make sure you have a JavaScript package manager like <code>npm</code>, <code>yarn</code>, or <code>pnpm</code>.
    - A favorite text editor or IDE
  source_code: <a href='https://github.com/asgardeo/web-ui-sdks/tree/main/samples/vue-sdk-playground' target='_blank' class='github-icon'>Vue Vite App Sample</a>
---

# Vue quickstart

Welcome to the Vue quickstart guide! In this document, you will learn to build a Vue app, add user sign-in, and display user profile information using WSO2 Identity Platform.



## Configure an application in WSO2 Identity Platform

- Sign into the WSO2 Identity Platform Console and navigate to **Applications > New Application**.
- Select **Single-Page Application** and complete the wizard by providing a suitable name and an authorized redirect URL.

:::note

**Name:** `<PRODUCT>-vue`

**Authorized redirect URL:** `http://localhost:5173`

:::

Once you finish creating the application, note down the following values from its **Guide** tab. You will need them to configure the WSO2 Identity Platform Vue SDK.

- **Client ID** - The unique identifier for your application.
- **Base URL** - The base URL of your WSO2 Identity Platform organization. This typically follows the format `<CONTENT_SDKCONFIG_BASEURL>`

:::info


The authorized redirect URL determines where WSO2 Identity Platform should send users after they successfully sign in. Typically, this will be the web address where your app is hosted. For this guide, we'll use `http://localhost:5173`, as the sample app will be accessible at this URL.

:::

## Create a Vue app using Vite

Create (scaffold) your new Vue app using [Vite](https://vite.dev/).

<Tabs>
<TabItem value="tab-0" label="npm">


```bash
npm create vite@latest <PRODUCT>-vue -- --template vue
cd <PRODUCT>-vue
npm install
npm run dev
```

</TabItem>
<TabItem value="tab-1" label="yarn">


```bash
yarn create vite@latest <PRODUCT>-vue -- --template vue
cd <PRODUCT>-vue
yarn install
yarn dev
```

</TabItem>
<TabItem value="tab-2" label="pnpm">


```bash
pnpm create vite@latest <PRODUCT>-vue -- --template vue
cd <PRODUCT>-vue
pnpm install
pnpm dev
```

</TabItem>
</Tabs>

## Install `@asgardeo/vue`

WSO2 Identity Platform Vue SDK provides all the components and composables you need to integrate WSO2 Identity Platform into your app. To get started, simply add the WSO2 Identity Platform Vue SDK to the project. Make sure to stop the dev server you started in the previous step.

<Tabs>
<TabItem value="tab-0" label="npm">


```bash
npm install @asgardeo/vue
```

</TabItem>
<TabItem value="tab-1" label="yarn">


```bash
yarn add @asgardeo/vue
```

</TabItem>
<TabItem value="tab-2" label="pnpm">


```bash
pnpm add @asgardeo/vue
```

</TabItem>
</Tabs>

## Add `AsgardeoPlugin` and `<AsgardeoProvider />` to your app

`AsgardeoPlugin` registers the WSO2 Identity Platform Vue SDK globally with your Vue application. `<AsgardeoProvider />` wraps your app and makes authentication context available to all child components.

Add the following changes to `main.js` to register the plugin.

```javascript title="src/main.js" {3,7}
import { createApp } from 'vue'
import './style.css'
import { AsgardeoPlugin } from '@asgardeo/vue'
import App from './App.vue'

createApp(App)
  .use(AsgardeoPlugin)
  .mount('#app')
```

Then replace the contents of `App.vue` with the following to wrap your app with `<AsgardeoProvider />`.

:::warning


Replace the following placeholders with your registered organization name in WSO2 Identity Platform and the generated `client-id` from the app you registered in WSO2 Identity Platform.

- `<your-app-client-id>`
- `<CONTENT_SDKCONFIG_BASEURL>`

:::

```vue title="src/App.vue" {2-5,7}
<template>
  <AsgardeoProvider
    client-id="<your-app-client-id>"
    base-url="<CONTENT_SDKCONFIG_BASEURL>"
  >
    <!-- Your app content goes here -->
  </AsgardeoProvider>
</template>
```

## Add sign-in and sign-out to your app

WSO2 Identity Platform Vue SDK provides `SignInButton` and `SignOutButton` components to handle user sign-in and sign-out. Use these components alongside `SignedIn` and `SignedOut` to conditionally render content based on the user's sign-in state.

Replace the contents of `App.vue` with the following.

```vue title="src/App.vue" {2,11-16}
<script setup>
import { SignedIn, SignedOut, SignInButton, SignOutButton } from '@asgardeo/vue'
</script>

<template>
  <AsgardeoProvider
    client-id="<your-app-client-id>"
    base-url="<CONTENT_SDKCONFIG_BASEURL>"
  >
    <header>
      <SignedIn>
        <SignOutButton />
      </SignedIn>
      <SignedOut>
        <SignInButton />
      </SignedOut>
    </header>
  </AsgardeoProvider>
</template>
```

## Display the signed-in user's profile information

You can use the `UserProfile` or `UserDropdown` components to display user profile information in a declarative way.

- `UserProfile`: Displays and allows the user to edit their profile information.
- `UserDropdown`: Provides a dropdown menu with built-in user information and sign-out functionality.

```vue title="src/App.vue" {2,12,20-22}
<script setup>
import { SignedIn, SignedOut, SignInButton, SignOutButton, UserDropdown, UserProfile } from '@asgardeo/vue'
</script>

<template>
  <AsgardeoProvider
    client-id="<your-app-client-id>"
    base-url="<CONTENT_SDKCONFIG_BASEURL>"
  >
    <header>
      <SignedIn>
        <UserDropdown />
        <SignOutButton />
      </SignedIn>
      <SignedOut>
        <SignInButton />
      </SignedOut>
    </header>
    <main>
      <SignedIn>
        <UserProfile />
      </SignedIn>
    </main>
  </AsgardeoProvider>
</template>
```

## Run the app

To run the app, use the following command:

<Tabs>
<TabItem value="tab-0" label="npm">


```bash
npm run dev
```

</TabItem>
<TabItem value="tab-1" label="yarn">


```bash
yarn dev
```

</TabItem>
<TabItem value="tab-2" label="pnpm">


```bash
pnpm dev
```

</TabItem>
</Tabs>

Visit your app's homepage at [http://localhost:5173](http://localhost:5173).

:::warning


To try out sign-in and sign-out features, create a test user in WSO2 Identity Platform by following this [guide](../guides/users/manage-users.md#onboard-single-user).

:::
