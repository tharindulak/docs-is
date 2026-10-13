---
title: Configure an application
mkdocs_template: complete-guide
deployment_options:
  - WSO2 Cloud
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/asgardeo/docs/complete-guides/expressjs/register-an-application.md
---

<Applies to="WSO2 Cloud">

First unless you already have done that, you need to create an organization in WSO2 Identity Platform and register your application as a Traditional Web Application.

* Sign up for a [free WSO2 Identity Platform account](../../get-started/create-identity-platform-account.md)


* Sign into WSO2 Identity Platform console and navigate to **Applications > New Application.**
* Select Traditional Web Application

![Select Traditional Web Application](../../../assets/img/complete-guides/nodejs/image5.png)  

Next, complete the wizard popup by providing a suitable name and following authorized redirect URLs. Keep OpenID Connect selected as the protocol.

:::note

**name:** asgardeo-expressjs

**Authorized redirect URLs:** http://localhost:3000/oauth2/redirect,http://localhost:3000

:::

![Register a new application](../../../assets/img/complete-guides/nodejs/image8.png)

:::info


The authorized redirect URL determines where WSO2 Identity Platform should send users after they successfully log in. Typically, this will be the web address where your app is hosted. For this guide, we'll use [http://localhost:3000/oauth2/redirect](http://localhost:3000/oauth2/redirect) and [http://localhost:3000](http://localhost:3000).

:::

You will need the following information available in the Quick Start tab of your app.

* Client ID
* Client Secret

![Quick start guide](../../../assets/img/complete-guides/nodejs/image9.png)

After creating the application, navigate to **User Management > Users** and [create a new user](../../guides/users/manage-users.md#onboard-users). We will use this user to log in to the Express.js app.

In this step, we have registered our Express.js app as an application in the WSO2 Identity Platform console and generated the required metadata. Next, we will create a Express.js app using the Express.js framework.

</Applies>



<Applies to="Self-hosted">

* Sign into WSO2 Identity Server console and navigate to **Applications > New Application.**
* Select Traditional Web Application

![Select Traditional Web Application](../../../assets/img/complete-guides/nodejs/image5.png)  

Next, complete the wizard popup by providing a suitable name and following authorized redirect URLs. Keep OpenID Connect selected as the protocol.

:::note

**name:** is-expressjs

**Authorized redirect URLs:** http://localhost:3000/oauth2/redirect,http://localhost:3000

:::

![Register a new application](../../../assets/img/complete-guides/nodejs/image8.png)

:::info


The authorized redirect URL determines where WSO2 Identity Server should send users after they successfully log in. Typically, this will be the web address where your app is hosted. For this guide, we'll use [http://localhost:3000/oauth2/redirect](http://localhost:3000/oauth2/redirect) and [http://localhost:3000](http://localhost:3000).

:::

You will need the following information available in the Quick Start tab of your app.

* Client ID
* Client Secret

![Quick start guide](../../../assets/img/complete-guides/nodejs/image9.png)

After creating the application, navigate to **User Management > Users** and [create a new user](../../guides/users/manage-users.md#onboard-users). We will use this user to log in to the Express.js app.

In this step, we have registered our Express.js app as an application in the WSO2 Identity Server console and generated the required metadata. Next, we will create a Express.js app using the Express.js framework.

</Applies>
