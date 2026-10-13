---
title: Quickstart
mkdocs_template: quick-start
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.3.0/docs/quick-starts/expressjs.md
quick_start:
  what_you_will_learn:
    - Create new Express.js app
    - Install Passport Asgardeo strategy <a href='https://www.npmjs.com/package/@asgardeo/passport-asgardeo' target='_blank' rel='noopener noreferrer'>@asgardeo/passport-asgardeo</a>
    - Add user login and logout
    - Display user profile information
  prerequisites:
    - About 15 minutes
    - <a href='{{ base_path }}/get-started/quick-set-up/'>Set-up {{ product_name }}</a>
    - Install <a href='https://nodejs.org/en/download/package-manager' target='_blank' rel='noopener noreferrer'>Node.js</a> on your system.
    - Make sure you have a JavaScript package manager like <code>npm</code>, <code>yarn</code>, or <code>pnpm</code>.
    - A favorite text editor or IDE
  source_code: <a href='https://github.com/asgardeo-samples/asgardeo-javascript-samples/tree/main/passport-asgardeo-sample' target='_blank' class='github-icon'>WSO2 IS Express.js Sample</a>
---

import Expressjs from '../_partials/quick-starts/expressjs.mdx';

<Expressjs />

:::tip[Tip]


In WSO2 Identity Server, the default certificate is a self signed certificate. This certificate needs to be added to the runtime path in order to avoid SSL errors.

Excute the below commands before running `npm start`

Naviate to the &lt;IS_HOME>/repository/resources/security directory and execute the following

```bash
keytool -export -alias wso2carbon -file carbon_public2.crt -keystore wso2carbon.p12 -storetype PKCS12 -storepass wso2carbon
```

Convert the certificate to X509 format.

```bash
openssl x509 -in carbon_public2.crt -inform der -outform pem -out certificate.pem
```

Navigate to the passport-wso2-sample home and execute the following
```bash
export NODE_EXTRA_CA_CERTS=./<PATH_TO_CERTIFICATE_FILE>/certificate.pem
```

:::
