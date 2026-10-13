---
title: Exporting WSO2 Identity Server User Information to Sendgrid
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/guides/identity-lifecycles/sync-with-sendgrid.md
---

# Exporting WSO2 Identity Server User Information to Sendgrid

SendGrid is a cloud-based service that assists businesses with email delivery. 
This topic provides instructions on exporting user data from WSO2 Identity Server (WSO2 IS) to Sendgrid Email Delivery
platform.

Let's get started!

:::tip[Before you begin!]

Create the `users.csv` file by following the instructions in 
[Exporting User Data From WSO2 Identity Server](sync-account-overview.md).

:::

## Try it Out

1. Login to [Sendgrid](https://sendgrid.com/).
2. Click **Contacts** under **Marketing**.
    
3. Click **Upload CSV** under **Add Contacts**.
    
4. Select the **Add Contacts and include in existing list**(ie. This may change according to your requirement) 
radio button and select the CSV file with user data.
    
5. Map **CSV data fields** with **Sendgrid data fields**. **Skip** unwanted data fields.
6. Click **Next: Add Contacts**.
7. Click **Done**. 
8. Now you can view the uploaded user list in the **Contacts** section.
