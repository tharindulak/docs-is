---
title: Request user information
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.2.0/docs/guides/authentication/oidc/request-user-info.md
---

# Request user information

User information is encoded inside the ID token returned along with the access token. In addition to that, OpenID Connect provides the userinfo endpoint  to obtain user
information as a payload. The application should send a request with the access token to invoke the userinfo endpoint.

**Userinfo endpoint**

```
https://localhost:9443/oauth2/userinfo
```

**Sample request**

<Tabs>
<TabItem value="tab-0" label="cURL">

```bash
curl --location --request GET 'https://localhost:9443/oauth2/userinfo' \
--header 'Authorization: Bearer {your_access_token}'
```

</TabItem>
<TabItem value="tab-1" label="JavaScript - jQuery">

```js
var settings = {
    "url": "https://localhost:9443/oauth2/userinfo",
    "method": "GET",
    "timeout": 0,
    "headers": {
        "Authorization": "Bearer {your_access_token}"
    },
};

$.ajax(settings).done(function (response) {
    console.log(response);
});
```

</TabItem>
<TabItem value="tab-2" label="Nodejs - Axios">

```js
var axios = require('axios');

var config = {
    method: 'get',
    url: 'https://localhost:9443/oauth2/userinfo',
    headers: {
        'Authorization': 'Bearer {your_access_token}'
    }
};

axios(config)
    .then(function (response) {
        console.log(JSON.stringify(response.data));
    })
    .catch(function (error) {
        console.log(error);
    });
```

</TabItem>
</Tabs>

**Default sample response**  
WSO2 Identity Server returns only the `sub` claim if there are no user attributes shared with the application.

```json
{
  "sub": "e46ffa67-100d-4329-9460-b8251d446518"
}
```

You can customize the user information in the response by [configuring user attributes](../user-attributes/enable-attributes-for-oidc-app.md) on the registered application.
<br />
