---
title: Complete Guide
mkdocs_template: complete-guide
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/complete-guides/expressjs/introduction.md
---

In this guide, we will be using Express.js, which is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications. It is designed for building single-page, multi-page, and hybrid web applications. Express.js is widely used for building APIs and web applications.

Implementing login functionality in your Express.js app is essential for managing user access, personalizing user experiences, and securing the app. It enhances user experience, protects user data, boosts engagement, and helps ensure regulatory compliance.

## Learning objectives

This guide will walk you through everything you need to know about securing Express.js apps, including implementing user login, integrating it with an Identity Provider (IdP) to make the login process simple and secure, and general guidelines to protect your end users. It also covers how to make secure API calls to an OAuth2-protected API within your Express.js app.

In this guide, you will:

* Register an application in WSO2 Identity Server
* Create an Express.js app from the template
* Install passport.js and other dependencies
* Add login and logout to your app
* Display logged in user detail
* Secure routes within the app
* Access protected APIs from your app
* Manage tokens in your app

:::tip[Tip]


This guide takes approximately 60 minutes to complete and covers everything required to add user login and secure your Express.js apps.

:::


:::tip[Tip]


If you are already familiar with the concepts discussed in the guide, you can clone the sample Express.js application configured with WSO2 Identity Server from the [repository](https://github.com/asgardeo-samples/asgardeo-javascript-samples/tree/main/passport-asgardeo-sample). All you need to do is registering a **Traditional Web Application** in WSO2 Identity Server and updating the environment variables in the `.env` file as explained in the **README.md** file.

:::
