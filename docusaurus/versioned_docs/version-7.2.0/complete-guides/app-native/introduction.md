---
title: Complete Guide (App-Native)
mkdocs_template: complete-guide
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/complete-guides/app-native/introduction.md
---

In modern web applications, seamless authentication is a critical factor in delivering a smooth user experience. Traditional authentication methods often require users to be redirected to an external browser, which can disrupt the flow of an application. App-native authentication solves this by enabling authentication within the application's environment, eliminating unnecessary redirects and ensuring users remain engaged within the app.

This guide will walk you through integrating app-native authentication with WSO2 Identity Server in a Next.js application. Next.js, a powerful React framework, offers features such as Server-Side Rendering (SSR), Static Site Generation (SSG), and API routes, making it an ideal choice for building scalable, high-performance applications. By leveraging Next.js's capabilities and WSO2 Identity Server's authentication mechanisms, we can implement a secure, seamless login system that enhances user experience and ensures compliance with industry standards.

Whether you're looking to improve user engagement, protect sensitive data, or simplify authentication workflows, this guide will provide step-by-step instructions to help you integrate WSO2 Identity Server's app-native authentication into your Next.js application efficiently.

### Learning objectives

This guide will provide you with a comprehensive understanding of how to implement app-native authentication in a Next.js application using WSO2 Identity Server. You will learn how to integrate authentication seamlessly within your application, ensuring a secure and smooth login experience without external browser redirection. Additionally, you will gain insights into securing API calls, managing authentication tokens, and protecting user data.

By the end of this guide, you will be able to:

- Register an application in WSO2 Identity Server to enable authentication.
- Set up a Next.js application with authentication capabilities.
- Install and configure the WSO2 Identity Platform SDK, enabling seamless authentication.
- Implement login and logout functionality to allow users to authenticate within the app using app native authentication.
- Retrieve and display user details after a successful login.
- Add Multi Factor Authentication with app native authentication
- Add Social Login with app native authentication
- Manage authentication tokens effectively within the application to maintain session security.

By following this step-by-step guide, you will be equipped to integrate WSO2 Identity Server app-native authentication into your Next.js app, ensuring a secure and streamlined user experience.
