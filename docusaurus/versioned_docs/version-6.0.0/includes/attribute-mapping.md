---
title: Attribute mapping
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/includes/attribute-mapping.md
---

&lt;!--
When you are using more than one user store, you must map the attributes
correctly by [adding a claim mapping](../../../../guides/dialects/add-claim-mapping/.

Under “Mapped Attribute(s)”, you need to follow the pattern.

![mapped-attributes](../../../../assets/img/fragments/mapped-attributes.png)

However, for the default user store, you do not need to provide the
domain name. As an example, if you have two user stores, one is the
default and another one with domain “DEMO” then the pattern would be as
follows for `http://wso2.org/claims/emailaddress`.

```java
DEMO/mail
```
-->
