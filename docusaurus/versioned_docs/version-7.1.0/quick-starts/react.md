---
title: React Quickstart
mkdocs_template: quick-start
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/quick-starts/react.md
quick_start:
  what_you_will_learn:
    - Create new React app using Vite
    - Install <a href='https://www.npmjs.com/package/@asgardeo/auth-react' target='_blank' rel='noopener noreferrer'>@asgardeo/auth-react</a> package
    - Add user login and logout
    - Display user profile information
  prerequisites:
    - About 15 minutes
    - <a href='{{ base_path }}/get-started/quick-set-up/'>Set-up {{ product_name }}</a>
    - Install <a href='https://nodejs.org/en/download/package-manager' target='_blank' rel='noopener noreferrer'>Node.js</a> on your system.
    - Make sure you have a JavaScript package manager like <code>npm</code>, <code>yarn</code>, or <code>pnpm</code>.
    - A favorite text editor or IDE
  source_code: <a href='https://github.com/asgardeo/asgardeo-auth-react-sdk/tree/main/samples/asgardeo-react-app' target='_blank' class='github-icon'>React Vite App Sample</a>
  whats_next:
    - Try out <a href='{{ base_path }}/complete-guides/react/introduction/' target='_blank'>{{ product_name }} complete React guide</a>
    - Try out {{ product_name }} user onboarding complete guide for React
    - Read security best practices for React app guide
---

# React Quickstart

Welcome to the React Quickstart guide! In this document, you will learn to build a React app, add user sign-in and display user profile information using WSO2 Identity Server.



## Configure an Application in WSO2 Identity Server

- Sign into the WSO2 Identity Server Console and navigate to **Applications > New Application**.
- Select **React** and complete the wizard by providing a suitable name and an authorized redirect URL.

:::note

**Name:** `is-react`

**Authorized redirect URL:** `http://localhost:5173`

:::

Once you finish creating the application, note down the following values from its **Guide** tab. You will need them to configure WSO2 Identity Platform React SDK.

- **Client ID** - The unique identifier for your application.
- **Base URL** - The base URL of your WSO2 Identity Server organization. This typically follows the format `https://localhost:9443`

:::info


The authorized redirect URL determines where WSO2 Identity Server should send users after they successfully log in. Typically, this will be the web address where your app is hosted. For this guide, we'll use `http://localhost:5173`, as the sample app will be accessible at this URL.

:::

## Create a React app using Vite

Create (scaffold) your new React app using [Vite](https://vite.dev/).

<Tabs>
<TabItem value="tab-0" label="npm">


```bash
npm create vite@latest is-react -- --template react
cd is-react
npm install
npm run dev
```

</TabItem>
<TabItem value="tab-1" label="yarn">


```bash
yarn create vite@latest is-react -- --template react
cd is-react
yarn install
yarn dev
```

</TabItem>
<TabItem value="tab-2" label="pnpm">


```bash
pnpm create vite@latest is-react -- --template react
cd is-react
pnpm install
pnpm dev
```

</TabItem>
</Tabs>

## Install `@asgardeo/react`

WSO2 Identity Platform React SDK provides all the components and hooks you need to integrate WSO2 Identity Server into your app. To get started, simply add the WSO2 Identity Platform React SDK to the project. Make sure to stop the dev server you started in the previous step.

<Tabs>
<TabItem value="tab-0" label="npm">


```bash
npm install @asgardeo/react
```

</TabItem>
<TabItem value="tab-1" label="yarn">


```bash
yarn add @asgardeo/react
```

</TabItem>
<TabItem value="tab-2" label="pnpm">


```bash
pnpm add @asgardeo/react
```

</TabItem>
</Tabs>

## Add `<AsgardeoProvider />` to your app

The `<AsgardeoProvider />` serves as a context provider for the SDK. You can integrate this provider to your app by wrapping the root component.

Add the following changes to the `main.jsx` file.

:::warning


Replace below placeholders with your registered organization name in WSO2 Identity Server and the generated `client-id` from the app you registered in WSO2 Identity Server.

- `<your-app-client-id>`
- `https://localhost:9443`

:::

```javascript title="src/main.jsx" {5,9-12,14}
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'
import { AsgardeoProvider } from '@asgardeo/react'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <AsgardeoProvider
      clientId="<your-app-client-id>"
      baseUrl="https://localhost:9443"
    >
      <App />
    </AsgardeoProvider>
  </StrictMode>
)
```

## Add sign-in and sign-out to your app

WSO2 Identity Platform SDK provides `SignInButton`, `SignOutButton` components to handle user sign-in and sign-out. You can use these components along side `SignedIn` and `SignedOut` components to conditionally render content based on the user's logged in state.

Replace the existing content of the `App.jsx` file with following content.

```javascript title="src/App.jsx" {1,7-12}
import { SignedIn, SignedOut, SignInButton, SignOutButton } from '@asgardeo/react'
import './App.css'

function App() {
  return (
    <header>
      <SignedIn>
        <SignOutButton />
      </SignedIn>
      <SignedOut>
        <SignInButton />
      </SignedOut>
    </header>
  )
}

export default App
```

## Display signed-in user's profile information

You can use the `User`, `UserProfile`, or `UserDropdown` components to access and display user profile information in a declarative way.

- `User`: The `User` component provides a render prop pattern to access user profile information:
- `UserProfile`: The `UserProfile` component provides a declarative way to display and update user profile information.
- `UserDropdown`: The `UserDropdown` component provides a dropdown menu with built-in user information and sign-out functionality.

```javascript title="src/App.jsx" {1,9,18-25}
import { SignedIn, SignedOut, SignInButton, SignOutButton, User, UserDropdown, UserProfile } from '@asgardeo/react'
import './App.css'

function App() {
  return (
    <>
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
          <User>
            {(user) => (
              <div>
                <p>Welcome back, {user.userName || user.username || user.sub}</p>
              </div>
            )}
          </User>
          <UserProfile />
        </SignedIn>
      </main>
    </>
  )
}

export default App
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


To try out sign-in and sign-out features, create a test user in WSO2 Identity Server by following this [guide](../guides/users/manage-users.md#onboard-single-user).

:::
