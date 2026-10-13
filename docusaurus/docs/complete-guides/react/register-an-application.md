---
title: Configure an application
mkdocs_template: complete-guide
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/complete-guides/react/register-an-application.md
---

<Applies to="WSO2 Cloud">

First unless you already have done that, you need to create an organization in WSO2 Identity Platform and register your application as a single page application.

* Sign up for a [free WSO2 Identity Platform account](../../get-started/create-identity-platform-account.md)

* Sign into the WSO2 Identity Platform console and navigate to **Applications > New Application.**
* Select React Application

![Select React Application](../../../assets/img/complete-guides/react/image5.png)  


Next, complete the wizard popup by providing a suitable name and an authorized redirect URL.

:::note

name: asgardeo-react

Authorized redirect URL: http://localhost:5173

:::

![Register a new application](../../../assets/img/complete-guides/react/image8.png)

:::info


The authorized redirect URL determines where WSO2 Identity Platform should send users after they successfully log in. Typically, this will be the web address where your app is hosted. For this guide, we'll use [http://localhost:5173](http://localhost:5173), as the sample app will be accessible at this URL.

:::


You will need the following information available in the Quick Start tab of your app or the Quickstart guide under the React SDK for the `AuthProvider` config.

* Client ID
* Base URL
* Redirect URL

![Quick start guide](../../../assets/img/complete-guides/react/image9.png)



In this step, we have registered our React app as an application in the WSO2 Identity Platform console and generated the required metadata. Next, we will create a React app using Vite.

</Applies>



<Applies to="Self-hosted">

First unless you already have done that, you need to register your application as a single page application.

* Download and [setup WSO2 Identity Server](../../get-started/quick-set-up.md)
* Sign into the WSO2 Identity Server console and navigate to **Applications > New Application.**
* Select Single Page Application

![Select Single Page Application](../../../assets/img/complete-guides/react/image5.png)  


Next, complete the wizard popup by providing a suitable name and an authorized redirect URL.

:::note

name: is-react

Authorized redirect URL: http://localhost:5173

:::

![Register a new application](../../../assets/img/complete-guides/react/image8.png)

:::info


The authorized redirect URL determines where WSO2 Identity Server should send users after they successfully log in. Typically, this will be the web address where your app is hosted. For this guide, we'll use [http://localhost:5173](http://localhost:5173), as the sample app will be accessible at this URL.

:::


You need the following information.

* Client ID - You can find this from the application's **Protocol** tab.
* Base URL - `https://localhost:9443`
* Redirect URL - `http://localhost:5173` or the custom redirect URL you specified when creating the application.


In this step, we have registered our React app as an application in the WSO2 Identity Server console and generated the required metadata. Next, we will create a React app using Vite.

</Applies>
