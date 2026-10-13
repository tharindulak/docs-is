---
title: Applications
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.0.0/docs/guides/applications/index.md
---

# Applications

Registering your application is the first step towards unlocking the full spectrum of features offered by WSO2 Identity Server.

## Register an application

WSO2 Identity Server supports integrating five application types. Once registered, WSO2 Identity Server sets the default configurations for your application which can easily be customized according to your requirements.

### Single-page applications

Single-page applications (SPAs) run on the browser and dynamically update the content as the user interacts with it. As the user does not need to wait page reloads, users have a seamless experience with high responsiveness. JavaScript frameworks and libraries such as React, Angular and Vue.js are some popular technologies adopted to build SPAs. 

- [Register a single-page application](register-single-page-app.md)

### Web applications

Web applications (web apps) are the most common type of applications in use. They are usually hosted on a web server and accessed by a browser. Web applications require authentication as they offer functionality specific to logged-in users. 

- [Register a web application with OIDC](register-oidc-web-app.md)
- [Register a web application with SAML](register-saml-web-app.md)

### Mobile applications

Mobile applications are apps that run on mobile devices. Android and iOS are some of the popular technologies adopted to build mobile applications.

- [Register a mobile application](register-mobile-app.md)

### Standard-based applications

Standard-based applications allow you to configure the application protocol settings (OIDC or SAML) from scratch. 

- [Register a standard-based application](register-standard-based-app.md)


### Machine-to-Machine (M2M) applications

Machine-to-Machine (M2M) applications are designed for automated communication and interaction between devices or services without direct human intervention. Unlike user-centric applications, M2M applications cater to non-interactive scenarios, including command-line tools, daemons, IoT (Internet of Things) devices, or services running on the backend. 

- [Register a machine-to-machine application](register-machine-to-machine-app.md)


## Make an application discoverable

Discoverable applications appear in the users' [My Account portal](../user-self-service/configure-self-service-portal.md), making it easy for users to see and access the applications that they can use. When users click on an application, they get redirected to the application's access URL.

To enable application discovery:

1. On the WSO2 Identity Server Console, navigate to **Applications**.
2. Select the application you want users in the organization to discover and go to the **General** tab. (This option is not available for M2M applications.)
3. Scroll down to the **Discoverable application** section.
4. Select the checkbox to enable and configure an access URL to make the application discoverable to everyone in the organization.


To learn how users can discover applications through the **My Account** portal, see [Discover applications](../user-self-service/discover-applications.md).



## Delete an application

To delete an application,

1. On the WSO2 Identity Server Console, go to **Applications**.

2. Select the application you wish to delete and go to its **General** tab.

3. Scroll down to the **Danger Zone**. 

4. Click Delete under **Delete application** and confirm your action.
