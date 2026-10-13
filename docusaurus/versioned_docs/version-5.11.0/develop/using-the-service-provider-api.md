---
title: Using the Service Provider API
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/5.11.0/docs/develop/using-the-service-provider-api.md
---

# Using the Service Provider API

This section guides you through using the Identity Application Management API and its operations.

## About Identity Application Management API

The Identity Application Management API enables creating a service provider, updating it, deleting it. and the different operations you can use to work with it.  

## API operations

:::tip[Before you begin]


-   The service contract of this admin service can be found at the following URL:

    ```tab
    https://<IS_HOST>:<IS_PORT>/services/IdentityApplicationManagementService?wsdl
    ```

    ```tab
    https://localhost:9443/services/IdentityApplicationManagementService?wsdl
    ```

-   To enable the admin service, follow the instructions given in [Calling Admin Services](../../develop/calling-admin-services).  

:::


:::info[About creating applications]


Creating an application via the Identity Application Management Service is a two-step process.

1.  Create a service provider for the given application name and the description using the **`createApplication`** operation. It returns a `200 OK` response.  

    The service provider's application ID is required to use the **`updateApplication`** operation. You can include an application ID for the new service provider within the
    same SOAP request when calling the `createApplication` operation. If you do not include an application ID in the request, you can retrieve the auto-generated application ID value by calling the `getApplication` service method with the application name.

2.  Update the service provider with other configurations using the `updateApplication` operation. The service provider's application ID is required for this request.

:::
    

### createApplication

<table><tbody><tr><th>{"Description"}</th><td><p>{"Creating an application via the Identity Application Management Service is a two-step process."}</p><ol><li>{"Create a service provider for the given application name and the description using the "}<b><code>{"createApplication"}</code></b>{" operation. It returns a "}<code>{"200 OK"}</code>{" response. "}<br />{"The service provider's application ID is required to use the "}<b><code>{"updateApplication"}</code></b>{" operation. You can include an application ID for the new service provider within the same SOAP request when calling the "}<code>{"createApplication"}</code>{" operation. If you do not include an application ID in the request, you can retrieve the auto-generated application ID value by calling the "}<b><code>{"getApplication"}</code></b>{" service method with the application name."}</li><li>{"Update the service provider with other configurations using the "}<code>{"updateApplication"}</code>{" operation. The service provider's application ID is required for this request."}</li></ol></td></tr><tr><th>{"Permission Level"}</th><td>{"/permission/admin/manage"}</td></tr><tr><th>{"Input Parameters"}</th><td><ul><li><code>{"applicationID"}</code>{" "}<code>{"[Integer]"}</code>{": This uniquely identifies the service provider application. This is an optional parameter, if you have not included this value in the SOAP request, WSO2 Identity Server assigns a unique application Id."}</li><li><p><code>{"applicationName "}</code>{" "}<code>{"[String]"}</code>{": This is the desired service provider name."}</p><p></p><div className={"admonition note"}><p className={"admonition-title"}>{"Note"}</p><p>{"Adding a service provider creates an internal application role for the given application name in the following format: "}<code>{"Internal/"}<applicationname></applicationname></code>{". Therefore, creating another service provider for the same application name is not possible and will throw an "}<code>{"IdentityApplicationManagementException"}</code>{"."}</p></div><p></p></li><li><code>{"description"}</code>{" "}<code>{"[String]"}</code>{": This is a brief text description of the service provider."}</li></ul></td></tr><tr><th>{"Request"}</th><td>{"See below"}</td></tr><tr><th>{"Response"}</th><td>{"See below"}</td></tr></tbody></table>

<details>
<summary>Click to view request and response</summary>


```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://org.apache.axis2/xsd" xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
   <soapenv:Header/>
   <soapenv:Body>
      <xsd:createApplication>
         <!--Optional:-->
         <xsd:serviceProvider>
            <!--Optional:-->
            <xsd1:applicationName>?</xsd1:applicationName>
            <!--Optional:-->
            <xsd1:description>?</xsd1:description>
         </xsd:serviceProvider>
      </xsd:createApplication>
   </soapenv:Body>
</soapenv:Envelope>
```


```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://org.apache.axis2/xsd" xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
   <soapenv:Header/>
   <soapenv:Body>
      <xsd:createApplication>
         <!--Optional:-->
         <xsd:serviceProvider>
            <!--Optional:-->
            <xsd1:applicationName>travelocity.com</xsd1:applicationName>
            <!--Optional:-->
            <xsd1:description>sample service provider</xsd1:description>
         </xsd:serviceProvider>
      </xsd:createApplication>
   </soapenv:Body>
</soapenv:Envelope>
``` 

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
   <soapenv:Body>
      <ns:createApplicationResponse xmlns:ns="http://org.apache.axis2/xsd">
         <ns:return xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"/>
      </ns:createApplicationResponse>
   </soapenv:Body>
</soapenv:Envelope>
```

</details>

### updateApplication

<table><tbody><tr className={"even"}><th>{"Description"}</th><td><p>{"After creating the service provider, it can be configured and updated with the following configurations:"}</p><ul><li>{"Claim configuration"}</li><li>{"Role/Permission configuration"}</li><li>{"Inbound and Outbound authentication configuration"}</li><li>{"Inbound and Outbound provisioning configuration"}</li><li>{"Get application ID: The service provider is updated based on its application Id. If you have not provided an application ID when creating the service provider, you can use the "}<a href={"#getapplication"}>{"getApplication"}</a>{" operation to retrieve the application Id value from WSO2 Identity Server."}</li><li><p>{"Get certificate reference ID: The certificate of the service provider is updated based on its certificate reference Id. Use the "}<a href={"#getapplication"}>{"getApplication"}</a>{" operation to retrieve the certificate reference Id value from WSO2 Identity Server and include it in the "}<code>{"updateApplication"}</code>{" SOAP request to update the same certificate. The code block below shows the certificate reference ID value included in the "}<code>{"getApplication"}</code>{" response."}</p><p></p><div><pre><code>{"<ax2140:spProperties xsi:type=\"ax2140:ServiceProviderProperty\">\n          <ax2140:displayName>CERTIFICATE</ax2140:displayName>\n          <ax2140:name>CERTIFICATE</ax2140:name>\n          <ax2140:value>2</ax2140:value>\n        </ax2140:spProperties>"}</code></pre></div><p></p><p>{"To update the same certificate, include the certificate reference ID you retrieved in the "}<code>{"updateApplication"}</code>{" SOAP request as follows."}</p><p></p><div><pre><code>{"<xsd1:spProperties>\n      <!--Optional:-->\n      <xsd1:displayName>CERTIFICATE</xsd1:displayName>\n      <!--Optional:-->\n      <xsd1:name>CERTIFICATE</xsd1:name>\n      <!--Optional:-->\n      <xsd1:value>2</xsd1:value>\n    </xsd1:spProperties>"}</code></pre></div><p></p></li></ul></td></tr><tr className={"odd"}><th>{"Permission Level"}</th><td>{"/permission/admin/manage"}</td></tr><tr className={"even"}><th>{"Input Parameters"}</th><td><p>{"Service provider level parameters:"}</p><ul><li><code>{"applicationID"}</code>{" "}<code>{"[Integer]"}</code>{": This is the Application ID of the service provider. This is mandatory when updating the SP."}</li><li><code>{"applicationName"}</code>{" "}<code>{"[String]"}</code>{": This is the Service provider name."}</li><li><code>{"claimConfig"}</code>{" "}<code>{"[ClaimConfig]"}</code>{": These are Claims that are related configurations."}</li><li><code>{"description"}</code>{" "}<code>{"[String]"}</code>{": This is the description of the SP."}</li><li><code>{"inboundAuthenticationConfig"}</code>{" "}<code>{"[InboundAuthenticationConfig]"}</code>{": This is an "}<a href={"../../learn/configuring-inbound-authentication-for-a-service-provider"}>{"Inbound authentication"}</a>{" related configurations."}</li><li><code>{"inboundProvisioningConfig"}</code>{" "}<code>{"[InboundProvisioningConfig]"}</code>{": This is an inbound provisioning related configurations."}</li><li><code>{"localAndOutBoundAuthenticationConfig"}</code>{" "}<code>{"[LocalAndOutboundAuthenticationConfig]"}</code>{": This is for local and outbound authentication."}</li><li><code>{"outboundProvisioningConfig"}</code>{" "}<code>{"[OutboundProvisioningConfig]"}</code>{": This is for outbound provisioning related configurations."}</li><li><code>{"owner"}</code>{" "}<code>{"[User]"}</code>{": This is the applicationn owner."}</li><li><code>{"permissionAndRoleConfig"}</code>{" "}<code>{"[PermissionsAndRoleConfig]"}</code>{": These are permission and role related configurations."}</li><li><code>{"requestPathAuthenticatorConfigs"}</code>{" "}<code>{"[RequestPathAuthenticatorConfig]"}</code>{": These are request patch authenticator related configurationsr."}</li><li><code>{"saasApp"}</code>{": This is optional. This parameter allows you to determine whether the service provider is a SaaS application ("}<code>{"true"}</code>{") or not ("}<code>{"false"}</code>{")."}<br />{"If no value is passed for this parameter, the service provider is marked as SaaS disabled by default. Thus, the web application is not shared among tenants so only users in the current tenant (the one you are logged in when creating the service provider) are allowed to log into the web application. Alternatively, if you enabled SaaS application, that means this web application is shared among tenants so users from any tenant are allowed to log into the web application."}</li></ul></td></tr><tr><th>{"Request"}</th><td>{"See below"}</td></tr><tr><th>{"Response"}</th><td>{"See below"}</td></tr></tbody></table>


<details>
<summary>Click to view request and response formats</summary>


```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://org.apache.axis2/xsd" xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
   <soapenv:Header/>
   <soapenv:Body>
      <xsd:updateApplication>
         <!--Optional:-->
         <xsd:serviceProvider>
            <!--Optional:-->
            <xsd1:applicationID>?</xsd1:applicationID>
            <!--Optional:-->
            <xsd1:applicationName>?</xsd1:applicationName>
            <!--Optional:-->
            <xsd1:certificateContent>?</xsd1:certificateContent>
            <!--Optional:-->
            <xsd1:claimConfig>
            </xsd1:claimConfig>
            <!--Optional:-->
            <xsd1:description>?</xsd1:description>
            <!--Optional:-->
            <xsd1:inboundAuthenticationConfig>...</xsd1:inboundAuthenticationConfig>
            <!--Optional:-->
            <xsd1:inboundProvisioningConfig>...</xsd1:inboundProvisioningConfig>
            <!--Optional:-->
            <xsd1:localAndOutBoundAuthenticationConfig>...</xsd1:localAndOutBoundAuthenticationConfig>
            <!--Optional:-->
            <xsd1:outboundProvisioningConfig>...</xsd1:outboundProvisioningConfig>
            <!--Optional:-->
            <xsd1:owner>...</xsd1:owner>
            <!--Optional:-->
            <xsd1:permissionAndRoleConfig>...</xsd1:permissionAndRoleConfig>
            <!--Zero or more repetitions:-->
            <xsd1:requestPathAuthenticatorConfigs>...</xsd1:requestPathAuthenticatorConfigs>
            <!--Optional:-->
            <xsd1:saasApp>?</xsd1:saasApp>
            <xsd1:spProperties>
            <!--Optional:-->
            <xsd1:displayName>CERTIFICATE</xsd1:displayName>
            <!--Optional:-->
            <xsd1:name>CERTIFICATE</xsd1:name>
            <!--Optional:-->
            <xsd1:value>2</xsd1:value>
            </xsd1:spProperties>
         </xsd:serviceProvider>
      </xsd:updateApplication>
   </soapenv:Body>
</soapenv:Envelope>
```

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://org.apache.axis2/xsd" xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
   <soapenv:Header/>
   <soapenv:Body>
      <xsd:updateApplication>
         <!--Optional:-->
         <xsd:serviceProvider>
            <!--Optional:-->
            <xsd1:applicationID>2</xsd1:applicationID>
            <!--Optional:-->
            <xsd1:applicationName>travelocity.com</xsd1:applicationName>
            <!--Optional:-->
            <xsd1:claimConfig>
               <!--Optional:-->
               <xsd1:alwaysSendMappedLocalSubjectId>false</xsd1:alwaysSendMappedLocalSubjectId>
               <!--Optional:-->
               <xsd1:localClaimDialect>true</xsd1:localClaimDialect>
            </xsd1:claimConfig>
            <!--Optional:-->
            <xsd1:description>sample service provider</xsd1:description>
            <!--Optional:-->
            <xsd1:inboundAuthenticationConfig></xsd1:inboundAuthenticationConfig>
            <!--Optional:-->
            <xsd1:inboundProvisioningConfig>
               <!--Optional:-->
               <xsd1:provisioningEnabled>false</xsd1:provisioningEnabled>
               <!--Optional:-->
               <xsd1:provisioningUserStore>PRIMARY</xsd1:provisioningUserStore>
            </xsd1:inboundProvisioningConfig>
            <!--Optional:-->
            <xsd1:localAndOutBoundAuthenticationConfig>
               <!--Optional:-->
               <xsd1:alwaysSendBackAuthenticatedListOfIdPs>false</xsd1:alwaysSendBackAuthenticatedListOfIdPs>
               <!--Optional:-->
               <xsd1:authenticationStepForAttributes></xsd1:authenticationStepForAttributes>
               <!--Optional:-->
               <xsd1:authenticationStepForSubject></xsd1:authenticationStepForSubject>
               <xsd1:authenticationType>default</xsd1:authenticationType>
               <!--Optional:-->
               <xsd1:subjectClaimUri>http://wso2.org/claims/fullname</xsd1:subjectClaimUri>
            </xsd1:localAndOutBoundAuthenticationConfig>
            <!--Optional:-->
            <xsd1:outboundProvisioningConfig>
               <!--Zero or more repetitions:-->
               <xsd1:provisionByRoleList></xsd1:provisionByRoleList>
            </xsd1:outboundProvisioningConfig>
            <!--Optional:-->
            <xsd1:permissionAndRoleConfig></xsd1:permissionAndRoleConfig>
            <!--Optional:-->
            <xsd1:saasApp>false</xsd1:saasApp>
         </xsd:serviceProvider>
      </xsd:updateApplication>
   </soapenv:Body>
</soapenv:Envelope>
```

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://org.apache.axis2/xsd" xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
   <soapenv:Header/>
   <soapenv:Body>
      <xsd:updateApplication>
         <!--Optional:-->
         <xsd:serviceProvider>
            <!--Optional:-->
            <xsd1:applicationID>5</xsd1:applicationID>
            <!--Optional:-->
            <xsd1:applicationName>SampleApplication</xsd1:applicationName>
            <!--Optional:-->
            <xsd1:claimConfig>
               <!--Optional:-->
               <xsd1:alwaysSendMappedLocalSubjectId>false</xsd1:alwaysSendMappedLocalSubjectId>
               <!--Optional:-->
               <xsd1:localClaimDialect>true</xsd1:localClaimDialect>
            </xsd1:claimConfig>
            <!--Optional:-->
            <xsd1:description>oauth application</xsd1:description>
            <!--Optional:-->
            <xsd1:inboundAuthenticationConfig>
               <!--Zero or more repetitions:-->
               <xsd1:inboundAuthenticationRequestConfigs>
                  <!--Optional:-->
                  <xsd1:inboundAuthKey>CLIENT_ID</xsd1:inboundAuthKey>
                  <!--Optional:-->
                  <xsd1:inboundAuthType>oauth2</xsd1:inboundAuthType>
                  <!--Zero or more repetitions:-->
                  <xsd1:properties>
                     <!--Optional:-->
                     <xsd1:advanced>false</xsd1:advanced>
                     <!--Optional:-->
                     <xsd1:confidential>false</xsd1:confidential>
                     <!--Optional:-->
                     <xsd1:defaultValue></xsd1:defaultValue>
                     <!--Optional:-->
                     <xsd1:description></xsd1:description>
                     <!--Optional:-->
                     <xsd1:displayName></xsd1:displayName>
                     <!--Optional:-->
                     <xsd1:name>oauthConsumerSecret</xsd1:name>
                     <!--Optional:-->
                     <xsd1:required>false</xsd1:required>
                     <!--Optional:-->
                     <xsd1:type></xsd1:type>
                     <!--Optional:-->
                     <xsd1:value>CLIENT_SECRET</xsd1:value>
                  </xsd1:properties>
               </xsd1:inboundAuthenticationRequestConfigs>
            </xsd1:inboundAuthenticationConfig>
            <!--Optional:-->
            <xsd1:inboundProvisioningConfig>
               <!--Optional:-->
               <xsd1:provisioningEnabled>false</xsd1:provisioningEnabled>
               <!--Optional:-->
               <xsd1:provisioningUserStore>PRIMARY</xsd1:provisioningUserStore>
            </xsd1:inboundProvisioningConfig>
            <!--Optional:-->
            <xsd1:localAndOutBoundAuthenticationConfig>
               <!--Optional:-->
               <xsd1:alwaysSendBackAuthenticatedListOfIdPs>false</xsd1:alwaysSendBackAuthenticatedListOfIdPs>
               <!--Optional:-->
               <xsd1:authenticationStepForAttributes></xsd1:authenticationStepForAttributes>
               <!--Optional:-->
               <xsd1:authenticationStepForSubject></xsd1:authenticationStepForSubject>
               <xsd1:authenticationType>default</xsd1:authenticationType>
               <!--Optional:-->
               <xsd1:subjectClaimUri>http://wso2.org/claims/fullname</xsd1:subjectClaimUri>
            </xsd1:localAndOutBoundAuthenticationConfig>
            <!--Optional:-->
            <xsd1:outboundProvisioningConfig>
               <!--Zero or more repetitions:-->
               <xsd1:provisionByRoleList></xsd1:provisionByRoleList>
            </xsd1:outboundProvisioningConfig>
            <!--Optional:-->
            <xsd1:permissionAndRoleConfig></xsd1:permissionAndRoleConfig>
            <!--Optional:-->
            <xsd1:saasApp>false</xsd1:saasApp>
         </xsd:serviceProvider>
      </xsd:updateApplication>
   </soapenv:Body>
</soapenv:Envelope>
```

```java
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
   <soapenv:Body>
      <ns:updateApplicationResponse xmlns:ns="http://org.apache.axis2/xsd">
         <ns:return xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"/>
      </ns:updateApplicationResponse>
   </soapenv:Body>
</soapenv:Envelope>
```

</details>

#### Claims 

The `<claimConfig>` element  defines all claim configuration level inputs. This element can have zero or more `          <claimMappings>         ` elements that specify claims
referred by this service provider. A `          <claimMappings>         ` element includes two elements; `          <localClaim>         ` and `          <remoteClaim>         `
where each is represented by a claimId and a claimURI.  The `          <localClaim>         ` denotes a standard claim which is local to the WSO2 Identity Server and the
`          <remoteClaim>         ` denotes some remote claim value that maps to the local claim under the same [claim mapping](../../learn/claim-management). Remote
claims are specifically used with identity federation scenarios to map claims received from the federated Identity Provider to local claims.   

<table><thead><tr className={"header"}><th><p>{"Parameter"}</p></th><th><p>{"Type"}</p></th><th><p>{"Description"}</p></th></tr></thead><tbody><tr className={"odd"}><td><p>{"alwaysSendMappedLocalSubjectId"}</p></td><td><p>{"Boolean"}</p></td><td>{"This configuration specifies whether the subject attribute that returns to the service provider is taken from the locally mapped user or from the federated user."}</td></tr><tr className={"even"}><td><p>{"localClaimDialect"}</p></td><td><p>{"Boolean"}</p></td><td><p>{"This is a boolean that specifies whether this service provider is using the local claim dialect or a custom claim dialect."}</p><p>{"true - using the local claim dialect"}</p><p>{"false - using the custom claim dialect"}</p><br /><p>{"If it is using the custom claim dialect, the local claim should map with a remote claim in each "}<a href={"../../learn/claim-management"}>{"claim mapping"}</a>{" otherwise, both the local claim URI and the remote claim URI should be the same (i.e. a URI defined under a dialect local to the WSO2 Identity Server)."}</p></td></tr><tr className={"odd"}><td><p>{"claimMappings.localClaim.claimId"}</p><p>{"claimMappings.remoteClaim.claimId"}</p></td><td><p>{"Integer"}</p></td><td><p>{"Integer value that identifies the claim. Applies to both "}<code>{" localClaim "}</code>{" and "}<code>{" remoteClaim "}</code>{" elements."}</p></td></tr><tr className={"even"}><td><p>{"claimMappings.localClaim.claimUri"}</p><p>{"claimMappings.remoteClaim.claimUri"}</p></td><td><p>{"String"}</p></td><td><p>{"URI specific to the claim. It applies to both "}<code>{" localClaim "}</code>{" and "}<code>{" remoteClaim "}</code>{" elements. When defined under "}<code>{" localClaim "}</code>{", this is a URI defined under the dialect specific to the claim. If defined under the "}<code>{" remoteClaim "}</code>{", this is a remote claim URI which maps with the local claim defined under the same parent claimMappings element. If only the local claim dialect is used, the same claimURI in localClaim should be used with claimURI in "}<code>{" remoteClaim "}</code>{", since there are no explicit local to remote claim mappings."}</p></td></tr><tr className={"odd"}><td><p>{"claimMappings.requested"}</p></td><td><p>{"Boolean"}</p></td><td><p>{"This is a boolean that marks a mapped claim as a requested claim which ensures that the service provider definitely sends this claim to the Identity Server."}</p><p>{"true - mark as requested"}</p><p>{"false - mark as not requested"}</p></td></tr><tr className={"even"}><td><p>{"roleClaimURI"}</p></td><td><p>{"String"}</p></td><td><p>{"Role claim URI is used to identify the claim that equates to the role of the user. This is linked to the permissions that you can apply for specific user roles. This is a remote claim URI mapped via claim mappings."}</p></td></tr><tr className={"odd"}><td><p>{"userClaimURI"}</p></td><td><p>{"String"}</p></td><td><p>{"User claim URI is also referred to as Subject claim URI in the management console. It is the claim that is used to uniquely identiy a user. For example, mapping the claims to the users email or ID attribute."}</p></td></tr></tbody></table>

<details>
<summary>Click to view request</summary>


```xml
<xsd1:claimConfig>
    <!--Optional:-->
    <xsd1:alwaysSendMappedLocalSubjectId>?</xsd1:alwaysSendMappedLocalSubjectId>
    <!--Zero or more repetitions:-->
    <xsd1:claimMappings>
        <!--Optional:-->
        <xsd1:defaultValue>?</xsd1:defaultValue>
        <!--Optional:-->
        <xsd1:localClaim>
            <!--Optional:-->
            <xsd1:claimId>?</xsd1:claimId>
            <!--Optional:-->
            <xsd1:claimUri>?</xsd1:claimUri>
        </xsd1:localClaim>
        <!--Optional:-->
        <xsd1:mandatory>?</xsd1:mandatory>
        <!--Optional:-->
        <xsd1:remoteClaim>
            <!--Optional:-->
            <xsd1:claimId>?</xsd1:claimId>
            <!--Optional:-->
            <xsd1:claimUri>?</xsd1:claimUri>
        </xsd1:remoteClaim>
        <!--Optional:-->
        <xsd1:requested>?</xsd1:requested>
    </xsd1:claimMappings>
    <!--Zero or more repetitions:-->
    <xsd1:idpClaims>
        <!--Optional:-->
        <xsd1:claimId>?</xsd1:claimId>
        <!--Optional:-->
        <xsd1:claimUri>?</xsd1:claimUri>
    </xsd1:idpClaims>
    <!--Optional:-->
    <xsd1:localClaimDialect>?</xsd1:localClaimDialect>
    <!--Optional:-->
    <xsd1:roleClaimURI>?</xsd1:roleClaimURI>
    <!--Optional:-->
    <xsd1:userClaimURI>?</xsd1:userClaimURI>
</xsd1:claimConfig>
```

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://org.apache.axis2/xsd" xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
   <soapenv:Header/>
   <soapenv:Body>
      <xsd:updateApplication>
         <!--Optional:-->
         <xsd:serviceProvider>
            <!--Optional:-->
            <xsd1:applicationID>2</xsd1:applicationID>
            <!--Optional:-->
            <xsd1:applicationName>travelocity.com</xsd1:applicationName>
            <!--Optional:-->
            <xsd1:claimConfig>
               <!--Optional:-->
               <xsd1:alwaysSendMappedLocalSubjectId>false</xsd1:alwaysSendMappedLocalSubjectId>
               <!--Zero or more repetitions:-->
               <xsd1:claimMappings>
                  <!--Optional:-->
                  <xsd1:localClaim>
                     <!--Optional:-->
                     <xsd1:claimUri>http://wso2.org/claims/givenname</xsd1:claimUri>
                  </xsd1:localClaim>
                  <!--Optional:-->
                  <xsd1:mandatory>true</xsd1:mandatory>
                  <!--Optional:-->
                  <xsd1:remoteClaim>
                     <!--Optional:-->
                     <xsd1:claimUri>name</xsd1:claimUri>
                  </xsd1:remoteClaim>
                  <!--Optional:-->
                  <xsd1:requested>true</xsd1:requested>
               </xsd1:claimMappings>
               <xsd1:claimMappings>
                  <!--Optional:-->
                  <xsd1:localClaim>
                     <!--Optional:-->
                     <xsd1:claimUri>http://wso2.org/claims/role</xsd1:claimUri>
                  </xsd1:localClaim>
                  <!--Optional:-->
                  <xsd1:mandatory>true</xsd1:mandatory>
                  <!--Optional:-->
                  <xsd1:remoteClaim>
                     <!--Optional:-->
                     <xsd1:claimUri>role</xsd1:claimUri>
                  </xsd1:remoteClaim>
                  <!--Optional:-->
                  <xsd1:requested>true</xsd1:requested>
               </xsd1:claimMappings>
               <!--Optional:-->
               <xsd1:localClaimDialect>false</xsd1:localClaimDialect>
               <!--Optional:-->
               <xsd1:roleClaimURI>role</xsd1:roleClaimURI>
               <!--Optional:-->
               <xsd1:userClaimURI>user</xsd1:userClaimURI>
            </xsd1:claimConfig>
            <!--Optional:-->
            <xsd1:description>sample service provider</xsd1:description>
            <!--Optional:-->
            <xsd1:inboundAuthenticationConfig></xsd1:inboundAuthenticationConfig>
            <!--Optional:-->
            <xsd1:inboundProvisioningConfig>
               <!--Optional:-->
               <xsd1:provisioningEnabled>false</xsd1:provisioningEnabled>
               <!--Optional:-->
               <xsd1:provisioningUserStore>PRIMARY</xsd1:provisioningUserStore>
            </xsd1:inboundProvisioningConfig>
            <!--Optional:-->
            <xsd1:localAndOutBoundAuthenticationConfig>
               <!--Optional:-->
               <xsd1:alwaysSendBackAuthenticatedListOfIdPs>false</xsd1:alwaysSendBackAuthenticatedListOfIdPs>
               <!--Optional:-->
               <xsd1:authenticationStepForAttributes></xsd1:authenticationStepForAttributes>
               <!--Optional:-->
               <xsd1:authenticationStepForSubject></xsd1:authenticationStepForSubject>
               <xsd1:authenticationType>default</xsd1:authenticationType>
               <!--Optional:-->
               <xsd1:subjectClaimUri>name</xsd1:subjectClaimUri>
            </xsd1:localAndOutBoundAuthenticationConfig>
            <!--Optional:-->
            <xsd1:outboundProvisioningConfig>
               <!--Zero or more repetitions:-->
               <xsd1:provisionByRoleList></xsd1:provisionByRoleList>
            </xsd1:outboundProvisioningConfig>
            <!--Optional:-->
            <xsd1:permissionAndRoleConfig></xsd1:permissionAndRoleConfig>
            <!--Optional:-->
            <xsd1:saasApp>false</xsd1:saasApp>
         </xsd:serviceProvider>
      </xsd:updateApplication>
   </soapenv:Body>
</soapenv:Envelope>
```

</details>

#### Roles and permissions

The `          <permissionAndRoleConfig>         ` element defines all permission and role configuration level inputs. Under this element, specific permissions can be specified via zero or more
`          <permissions>         ` blocks.

  

| Parameter         | Type   | Description                                                                                                                                                                                                                                    |
|-------------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| permissions.value | String | A string value that defines a service provider specific permission. This permission is added under `               /permission/applications/<service-provider-name>/<given-permission-name>              ` and is available when adding roles. |

Once the permissions are specified, the roles specific to the service provider can be mapped to local roles defined in the Identity Server via zero or more `           <roleMappings>          ` blocks. A `           <roleMappings>          ` block includes a `           <localRole>          ` element and a `           <remoteRole>          ` element. The
`           <localRole>          ` represents a local role defined in the identity server and the `           <remoteRole>          ` represents the service provider specific role that you want to map to the local role.   

<table><thead><tr className={"header"}><th><p>{"Parameter"}</p></th><th><p>{"Type"}</p></th><th><p>{"Description"}</p></th></tr></thead><tbody><tr className={"odd"}><td><p>{"localRole.localRoleName"}</p></td><td><p>{"String"}</p></td><td><p>{"This is the name of the local role which is defined in Identity Server."}</p></td></tr><tr className={"even"}><td><p>{"localRole.userStoreId"}</p></td><td><p>{"String"}</p></td><td><p>{"This is the key of the userstore used by Identity Server."}<br /></p></td></tr><tr className={"odd"}><td><p>{"remoteRole"}</p></td><td><p>{"String"}</p></td><td><p>{"Role specific to the service provider"}</p></td></tr></tbody></table>

<details>
<summary>Click to view request</summary>


```xml
<xsd1:permissionAndRoleConfig>
    <!--Zero or more repetitions:-->
    <xsd1:idpRoles>?</xsd1:idpRoles>
    <!--Zero or more repetitions:-->
    <xsd1:permissions>
        <!--Optional:-->
        <xsd1:value>?</xsd1:value>
    </xsd1:permissions>
    <!--Zero or more repetitions:-->
    <xsd1:roleMappings>
        <!--Optional:-->
        <xsd1:localRole>
            <!--Optional:-->
            <xsd1:localRoleName>?</xsd1:localRoleName>
            <!--Optional:-->
            <xsd1:userStoreId>?</xsd1:userStoreId>
        </xsd1:localRole>
        <!--Optional:-->
        <xsd1:remoteRole>?</xsd1:remoteRole>
    </xsd1:roleMappings>
</xsd1:permissionAndRoleConfig>
```

```xml
<soapenv:Envelope
    xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
    xmlns:xsd="http://org.apache.axis2/xsd"
    xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
    <soapenv:Header/>
    <soapenv:Body>
        <xsd:updateApplication>
            <!--Optional:-->
            <xsd:serviceProvider>
                <!--Optional:-->
                <xsd1:applicationID>2</xsd1:applicationID>
                <!--Optional:-->
                <xsd1:applicationName>travelocity.com</xsd1:applicationName>
                <!--Optional:-->
                <xsd1:claimConfig>
                    <!--Optional:-->
                    <xsd1:alwaysSendMappedLocalSubjectId>false</xsd1:alwaysSendMappedLocalSubjectId>
                    <!--Optional:-->
                    <xsd1:localClaimDialect>true</xsd1:localClaimDialect>
                </xsd1:claimConfig>
                <!--Optional:-->
                <xsd1:description>sample service provider</xsd1:description>
                <!--Optional:-->
                <xsd1:inboundAuthenticationConfig></xsd1:inboundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:inboundProvisioningConfig>
                    <!--Optional:-->
                    <xsd1:provisioningEnabled>false</xsd1:provisioningEnabled>
                    <!--Optional:-->
                    <xsd1:provisioningUserStore>PRIMARY</xsd1:provisioningUserStore>
                </xsd1:inboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:localAndOutBoundAuthenticationConfig>
                    <!--Optional:-->
                    <xsd1:alwaysSendBackAuthenticatedListOfIdPs>false</xsd1:alwaysSendBackAuthenticatedListOfIdPs>
                    <!--Optional:-->
                    <xsd1:authenticationStepForAttributes></xsd1:authenticationStepForAttributes>
                    <!--Optional:-->
                    <xsd1:authenticationStepForSubject></xsd1:authenticationStepForSubject>
                    <xsd1:authenticationType>default</xsd1:authenticationType>
                    <!--Optional:-->
                    <xsd1:subjectClaimUri>http://wso2.org/claims/fullname</xsd1:subjectClaimUri>
                </xsd1:localAndOutBoundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:outboundProvisioningConfig>
                    <!--Zero or more repetitions:-->
                    <xsd1:provisionByRoleList></xsd1:provisionByRoleList>
                </xsd1:outboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:permissionAndRoleConfig>
                    <!--Zero or more repetitions:-->
                    <xsd1:permissions>
                        <!--Optional:-->
                        <xsd1:value>/sample/permission</xsd1:value>
                    </xsd1:permissions>
                    <!--Zero or more repetitions:-->
                    <xsd1:roleMappings>
                        <!--Optional:-->
                        <xsd1:localRole>
                            <!--Optional:-->
                            <xsd1:localRoleName>tester</xsd1:localRoleName>
                        </xsd1:localRole>
                        <!--Optional:-->
                        <xsd1:remoteRole>app-tester</xsd1:remoteRole>
                    </xsd1:roleMappings>
                </xsd1:permissionAndRoleConfig>
                <!--Optional:-->
                <xsd1:saasApp>false</xsd1:saasApp>
            </xsd:serviceProvider>
        </xsd:updateApplication>
    </soapenv:Body>
</soapenv:Envelope>
```

</details>

#### Inbound authentication

[Inbound Authentication](../../learn/configuring-inbound-authentication-for-a-service-provider) Configuration defines the protocol that the service provider and the
Identity Server uses to communicate. You can add a common set of configurations for the service provider for any protocol such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation (passive) that is supported by WSO2 Identity Server.

The `          <inboundAuthenticationConfig>         ` element consists of zero or more `<inboundAuthenticationRequestConfigs\>` elements. The `<inboundAuthenticationRequestConfigs\>` element has following elements (Note: Only the required element are mentioned).

:::note[Important]


You need to create inbound authenticator configurations
accessing the appropriate services(Ex: OAuthAdminService,
IdentitySAMLSSOConfigService, etc.), before updating service provider
with inbound authenticator configurations.

:::

  

| Parameter                                  | Type     | Description                                                                |
|--------------------------------------------|----------|----------------------------------------------------------------------------|
| inboundAuthKey                             | String   | Specify an identifier for the service provider as the authentication key.  |
| inboundAuthType                            | String   | Specify the authentication type. ex: samlsso, oauth2, wstrust, passivests, |
| properties                                 | Property | Inbound authentication request properties                                  |
| [properties.name](http://properties.name/) | String   | Specify the property name                                                  |
| properties.value                           | String   | Specify the property value                                                 |


<details>
<summary>Click to view request</summary>


```xml
<xsd1:inboundAuthenticationConfig>
    <!--Zero or more repetitions:-->
    <xsd1:inboundAuthenticationRequestConfigs>
        <!--Optional:-->
        <xsd1:friendlyName>?</xsd1:friendlyName>
        <!--Optional:-->
        <xsd1:inboundAuthKey>?</xsd1:inboundAuthKey>
        <!--Optional:-->
        <xsd1:inboundAuthType>?</xsd1:inboundAuthType>
        <!--Optional:-->
        <xsd1:inboundConfigType>?</xsd1:inboundConfigType>
        <!--Zero or more repetitions:-->
        <xsd1:properties>
            <!--Optional:-->
            <xsd1:advanced>?</xsd1:advanced>
            <!--Optional:-->
            <xsd1:confidential>?</xsd1:confidential>
            <!--Optional:-->
            <xsd1:defaultValue>?</xsd1:defaultValue>
            <!--Optional:-->
            <xsd1:description>?</xsd1:description>
            <!--Optional:-->
            <xsd1:displayName>?</xsd1:displayName>
            <!--Optional:-->
            <xsd1:displayOrder>?</xsd1:displayOrder>
            <!--Optional:-->
            <xsd1:name>?</xsd1:name>
            <!--Optional:-->
            <xsd1:required>?</xsd1:required>
            <!--Optional:-->
            <xsd1:type>?</xsd1:type>
            <!--Optional:-->
            <xsd1:value>?</xsd1:value>
        </xsd1:properties>
    </xsd1:inboundAuthenticationRequestConfigs>
</xsd1:inboundAuthenticationConfig>
```

```xml
<soapenv:Envelope
    xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
    xmlns:xsd="http://org.apache.axis2/xsd"
    xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
    <soapenv:Header/>
    <soapenv:Body>
        <xsd:updateApplication>
            <!--Optional:-->
            <xsd:serviceProvider>
                <!--Optional:-->
                <xsd1:applicationID>2</xsd1:applicationID>
                <!--Optional:-->
                <xsd1:applicationName>travelocity.com</xsd1:applicationName>
                <!--Optional:-->
                <xsd1:claimConfig>
                    <!--Optional:-->
                    <xsd1:alwaysSendMappedLocalSubjectId>false</xsd1:alwaysSendMappedLocalSubjectId>
                    <!--Optional:-->
                    <xsd1:localClaimDialect>true</xsd1:localClaimDialect>
                </xsd1:claimConfig>
                <!--Optional:-->
                <xsd1:description>sample service provider</xsd1:description>
                <!--Optional:-->
                <xsd1:inboundAuthenticationConfig>
                    <!--Zero or more repetitions:-->
                    <xsd1:inboundAuthenticationRequestConfigs>
                        <!--Optional:-->
                        <xsd1:inboundAuthKey>li6JMbjW6WDMKTWsRnGcjp5zcGhi</xsd1:inboundAuthKey>
                        <!--Optional:-->
                        <xsd1:inboundAuthType>oauth2</xsd1:inboundAuthType>
                        <!--Zero or more repetitions:-->
                        <xsd1:properties>
                            <!--Optional:-->
                            <xsd1:name>oauthConsumerSecret</xsd1:name>
                            <!--Optional:-->
                            <xsd1:value>NMB3EAfxh4YvSTqbb3iMkongAHjW</xsd1:value>
                        </xsd1:properties>
                    </xsd1:inboundAuthenticationRequestConfigs>
                    <xsd1:inboundAuthenticationRequestConfigs>
                        <!--Optional:-->
                        <xsd1:inboundAuthKey>travelocity.com</xsd1:inboundAuthKey>
                        <!--Optional:-->
                        <xsd1:inboundAuthType>samlsso</xsd1:inboundAuthType>
                        <!--Zero or more repetitions:-->
                        <xsd1:properties>
                            <!--Optional:-->
                            <xsd1:name>attrConsumServiceIndex</xsd1:name>
                            <!--Optional:-->
                            <xsd1:value>202240762</xsd1:value>
                        </xsd1:properties>
                    </xsd1:inboundAuthenticationRequestConfigs>
                </xsd1:inboundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:inboundProvisioningConfig>
                    <!--Optional:-->
                    <xsd1:provisioningEnabled>false</xsd1:provisioningEnabled>
                    <!--Optional:-->
                    <xsd1:provisioningUserStore>PRIMARY</xsd1:provisioningUserStore>
                </xsd1:inboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:localAndOutBoundAuthenticationConfig>
                    <!--Optional:-->
                    <xsd1:alwaysSendBackAuthenticatedListOfIdPs>false</xsd1:alwaysSendBackAuthenticatedListOfIdPs>
                    <!--Optional:-->
                    <xsd1:authenticationStepForAttributes></xsd1:authenticationStepForAttributes>
                    <!--Optional:-->
                    <xsd1:authenticationStepForSubject></xsd1:authenticationStepForSubject>
                    <xsd1:authenticationType>default</xsd1:authenticationType>
                    <!--Optional:-->
                    <xsd1:subjectClaimUri>http://wso2.org/claims/fullname</xsd1:subjectClaimUri>
                </xsd1:localAndOutBoundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:outboundProvisioningConfig>
                    <!--Zero or more repetitions:-->
                    <xsd1:provisionByRoleList></xsd1:provisionByRoleList>
                </xsd1:outboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:permissionAndRoleConfig></xsd1:permissionAndRoleConfig>
                <!--Optional:-->
                <xsd1:saasApp>false</xsd1:saasApp>
            </xsd:serviceProvider>
        </xsd:updateApplication>
    </soapenv:Body>
</soapenv:Envelope>
```

</details>

#### Inbound provisioning

The inbound provisioning of the service provider can be configured.   

| Parameter             | Type    | Description                                     |
|-----------------------|---------|-------------------------------------------------|
| provisioningEnabled   | Boolean | Specify whether inbound provisioning is enabled |
| provisioningUserStore | String  | User store domain name                          |

<details>
<summary>Click to view request</summary>


```xml
<xsd1:inboundProvisioningConfig>
    <!--Optional:-->
    <xsd1:dumbMode>?</xsd1:dumbMode>
    <!--Optional:-->
    <xsd1:provisioningEnabled>?</xsd1:provisioningEnabled>
    <!--Optional:-->
    <xsd1:provisioningUserStore>?</xsd1:provisioningUserStore>
</xsd1:inboundProvisioningConfig>
```

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://org.apache.axis2/xsd" xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
   <soapenv:Header/>
   <soapenv:Body>
      <xsd:updateApplication>
         <!--Optional:-->
         <xsd:serviceProvider>
            <!--Optional:-->
            <xsd1:applicationID>2</xsd1:applicationID>
            <!--Optional:-->
            <xsd1:applicationName>travelocity.com</xsd1:applicationName>
            <!--Optional:-->
            <xsd1:claimConfig>
               <!--Optional:-->
               <xsd1:alwaysSendMappedLocalSubjectId>false</xsd1:alwaysSendMappedLocalSubjectId>
               <!--Optional:-->
               <xsd1:localClaimDialect>true</xsd1:localClaimDialect>
            </xsd1:claimConfig>
            <!--Optional:-->
            <xsd1:description>sample service provider</xsd1:description>
            <!--Optional:-->
            <xsd1:inboundAuthenticationConfig></xsd1:inboundAuthenticationConfig>
            <!--Optional:-->
            <xsd1:inboundProvisioningConfig>
               <!--Optional:-->
               <xsd1:provisioningEnabled>true</xsd1:provisioningEnabled>
               <!--Optional:-->
               <xsd1:provisioningUserStore>PRIMARY</xsd1:provisioningUserStore>
            </xsd1:inboundProvisioningConfig>
            <!--Optional:-->
            <xsd1:localAndOutBoundAuthenticationConfig>
               <!--Optional:-->
               <xsd1:alwaysSendBackAuthenticatedListOfIdPs>false</xsd1:alwaysSendBackAuthenticatedListOfIdPs>
               <!--Optional:-->
               <xsd1:authenticationStepForAttributes></xsd1:authenticationStepForAttributes>
               <!--Optional:-->
               <xsd1:authenticationStepForSubject></xsd1:authenticationStepForSubject>
               <xsd1:authenticationType>default</xsd1:authenticationType>
               <!--Optional:-->
               <xsd1:subjectClaimUri>http://wso2.org/claims/fullname</xsd1:subjectClaimUri>
            </xsd1:localAndOutBoundAuthenticationConfig>
            <!--Optional:-->
            <xsd1:outboundProvisioningConfig>
               <!--Zero or more repetitions:-->
               <xsd1:provisionByRoleList></xsd1:provisionByRoleList>
            </xsd1:outboundProvisioningConfig>
            <!--Optional:-->
            <xsd1:permissionAndRoleConfig></xsd1:permissionAndRoleConfig>
            <!--Optional:-->
            <xsd1:saasApp>false</xsd1:saasApp>
         </xsd:serviceProvider>
      </xsd:updateApplication>
   </soapenv:Body>
</soapenv:Envelope>
```  

</details>

#### Local and outbound authentication  

<table><thead><tr className={"header"}><th><p>{"Parameter"}</p></th><th><p>{"Type"}</p></th><th><p>{"Description"}</p></th></tr></thead><tbody><tr className={"odd"}><td><p>{"alwaysSendBackAuthenticatedListOfIdPs"}</p></td><td><p>{"boolean"}</p></td><td><p>{"Always send back the authenticated list of identity providers."}</p><p><code>{"true"}</code>{" - send authenticated list of IdPs"}</p><p><code>{"false"}</code>{" - do not send authenticated list of IdPs"}</p></td></tr><tr className={"even"}><td><p>{"authenticationSteps"}</p></td><td><p>{"AuthenticationStep"}</p></td><td><p>{"Zero or more authentication steps. This can be used for subjects and attributes as well."}</p></td></tr><tr className={"odd"}><td><p>{"authenticationSteps.attributeStep"}</p></td><td><p>{"boolean"}</p></td><td><p>{"true - Use attributes from the current step"}</p></td></tr><tr className={"even"}><td><p>{"authenticationSteps.federatedIdentityProviders"}</p></td><td><p>{"IdentityProvider"}</p></td><td><div className={"content-wrapper"}><p>{"To configure federated IdPs, there should be one or more registered IdPs with at least one "}<a href={"https://docs.wso2.com/display/IS550/Configuring+Federated+Authentication"}>{"federated authenticator"}</a>{" enabled."}</p><p>{"With the request, it is necessary to include the IdP name and the federated authenticator name."}</p><p>{"The federated authenticator should be enabled in the IdP. If a federated authenticator is not mentioned, the default federated authenticator for the IdP will be used."}</p></div></td></tr><tr className={"odd"}><td><p>{"authenticationSteps.localAuthenticatorConfigs"}</p></td><td><p>{"LocalAuthenticatorConfigs"}</p></td><td><p>{"Local authentication related configs for the authentication step. For example, you can specify whether to use a basic or an IWA authenticator."}</p><br /><p>{"To use basic, "}<a href={"http://localauthenticatorconfigs.name/"}>{"localAuthenticatorConfigs.name"}</a>{" should be 'BasicAuthenticator' while 'IWAAuthenticator' for iwa."}</p></td></tr><tr className={"even"}><td><p>{"authenticationSteps.stepOrder"}</p></td><td><p>{"int"}</p></td><td><p>{"Execution order of the step"}</p></td></tr><tr className={"odd"}><td><p>{"authenticationSteps.subjectStep"}</p></td><td><p>{"boolean"}</p></td><td><p>{"true - Use subject identifier from this step"}</p></td></tr><tr className={"even"}><td><p>{"authenticationType"}</p></td><td><p>{"String"}</p></td><td><p>{"Depending on the requirement, the authentication type can be specified. The available types are: "}<a href={"#UsingtheServiceProviderAPI-authtype_D"}>{"default"}</a>{", "}<a href={"#UsingtheServiceProviderAPI-authtype_L"}>{"local"}</a>{", "}<a href={"#UsingtheServiceProviderAPI-authtype_F"}>{"federated"}</a>{", "}<a href={"#UsingtheServiceProviderAPI-authtype_A"}>{"flow"}</a>{" ."}</p><br /><p>{"Refer the sample requests below on each authentication type configuration."}</p></td></tr><tr className={"odd"}><td><p>{"subjectClaimUri"}</p></td><td><p>{"String"}</p></td><td><p>{"Subject claim URI"}</p></td></tr></tbody></table>

  
<details>
<summary>Click to view default request</summary>


```xml
<xsd1:localAndOutBoundAuthenticationConfig>
    <!--Optional:-->
    <xsd1:alwaysSendBackAuthenticatedListOfIdPs>false</xsd1:alwaysSendBackAuthenticatedListOfIdPs>
    <!--Optional:-->
    <xsd1:authenticationType>default</xsd1:authenticationType>
    <!--Optional:-->
    <xsd1:subjectClaimUri>http://wso2.org/claims/fullname</xsd1:subjectClaimUri>
</xsd1:localAndOutBoundAuthenticationConfig>
```

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://org.apache.axis2/xsd" xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
   <soapenv:Header/>
   <soapenv:Body>
      <xsd:updateApplication>
         <!--Optional:-->
         <xsd:serviceProvider>
            <!--Optional:-->
            <xsd1:applicationID>2</xsd1:applicationID>
            <!--Optional:-->
            <xsd1:applicationName>travelocity.com</xsd1:applicationName>
            <!--Optional:-->
            <xsd1:claimConfig>
               <!--Optional:-->
               <xsd1:alwaysSendMappedLocalSubjectId>false</xsd1:alwaysSendMappedLocalSubjectId>
               <!--Optional:-->
               <xsd1:localClaimDialect>true</xsd1:localClaimDialect>
            </xsd1:claimConfig>
            <!--Optional:-->
            <xsd1:description>sample service provider</xsd1:description>
            <!--Optional:-->
            <xsd1:inboundAuthenticationConfig></xsd1:inboundAuthenticationConfig>
            <!--Optional:-->
            <xsd1:inboundProvisioningConfig>
               <!--Optional:-->
               <xsd1:provisioningEnabled>false</xsd1:provisioningEnabled>
               <!--Optional:-->
               <xsd1:provisioningUserStore>PRIMARY</xsd1:provisioningUserStore>
            </xsd1:inboundProvisioningConfig>
            <!--Optional:-->
            <xsd1:localAndOutBoundAuthenticationConfig>
               <!--Optional:-->
               <xsd1:alwaysSendBackAuthenticatedListOfIdPs>false</xsd1:alwaysSendBackAuthenticatedListOfIdPs>
               <!--Optional:-->
               <xsd1:authenticationType>default</xsd1:authenticationType>
               <!--Optional:-->
               <xsd1:subjectClaimUri>http://wso2.org/claims/fullname</xsd1:subjectClaimUri>
            </xsd1:localAndOutBoundAuthenticationConfig>
            <!--Optional:-->
            <xsd1:outboundProvisioningConfig>
               <!--Zero or more repetitions:-->
               <xsd1:provisionByRoleList></xsd1:provisionByRoleList>
            </xsd1:outboundProvisioningConfig>
            <!--Optional:-->
            <xsd1:permissionAndRoleConfig></xsd1:permissionAndRoleConfig>
            <!--Optional:-->
            <xsd1:saasApp>false</xsd1:saasApp>
         </xsd:serviceProvider>
      </xsd:updateApplication>
   </soapenv:Body>
</soapenv:Envelope>
```

</details>

<details>
<summary>Click to view local request</summary>


As there is only one `          <authenticationSteps>         ` element configured here, there is no need to set the `          authenticationSteps.stepOrder         `, `          authenticationSteps.subjectStep, authenticationSteps.attributeStep         ` attributes.

```xml
<xsd1:localAndOutBoundAuthenticationConfig>
    <!--Zero or more repetitions:-->
    <xsd1:authenticationSteps>
        <!--Zero or more repetitions:-->
        <xsd1:localAuthenticatorConfigs>
            <!--Optional:-->
            <xsd1:displayName>basic</xsd1:displayName>
            <!--Optional:-->
            <xsd1:name>BasicAuthenticator</xsd1:name>
            <!--Optional:-->
            <xsd1:valid>true</xsd1:valid>
            <!--Zero or more repetitions:-->
        </xsd1:localAuthenticatorConfigs>
        <!--Optional:-->
        <xsd1:stepOrder>1</xsd1:stepOrder>
        <!--Optional:-->
        <xsd1:subjectStep>false</xsd1:subjectStep>
        <!--Optional:-->
    </xsd1:authenticationSteps>
    <xsd1:authenticationType>local</xsd1:authenticationType>
    <!--Optional:-->
    <xsd1:subjectClaimUri>http://wso2.org/claims/fullname</xsd1:subjectClaimUri>
</xsd1:localAndOutBoundAuthenticationConfig>
```

```xml
<soapenv:Envelope
    xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
    xmlns:xsd="http://org.apache.axis2/xsd"
    xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
    <soapenv:Header/>
    <soapenv:Body>
        <xsd:updateApplication>
            <!--Optional:-->
            <xsd:serviceProvider>
                <!--Optional:-->
                <xsd1:applicationID>2</xsd1:applicationID>
                <!--Optional:-->
                <xsd1:applicationName>travelocity.com</xsd1:applicationName>
                <!--Optional:-->
                <xsd1:claimConfig>
                    <!--Optional:-->
                    <xsd1:alwaysSendMappedLocalSubjectId>false</xsd1:alwaysSendMappedLocalSubjectId>
                    <!--Optional:-->
                    <xsd1:localClaimDialect>true</xsd1:localClaimDialect>
                </xsd1:claimConfig>
                <!--Optional:-->
                <xsd1:description>sample service provider</xsd1:description>
                <!--Optional:-->
                <xsd1:inboundAuthenticationConfig></xsd1:inboundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:inboundProvisioningConfig>
                    <!--Optional:-->
                    <xsd1:provisioningEnabled>false</xsd1:provisioningEnabled>
                    <!--Optional:-->
                    <xsd1:provisioningUserStore>PRIMARY</xsd1:provisioningUserStore>
                </xsd1:inboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:localAndOutBoundAuthenticationConfig>
                    <!--Zero or more repetitions:-->
                    <xsd1:authenticationSteps>
                        <!--Zero or more repetitions:-->
                        <xsd1:localAuthenticatorConfigs>
                            <!--Optional:-->
                            <xsd1:displayName>basic</xsd1:displayName>
                            <!--Optional:-->
                            <xsd1:name>BasicAuthenticator</xsd1:name>
                            <!--Optional:-->
                            <xsd1:valid>true</xsd1:valid>
                            <!--Zero or more repetitions:-->
                        </xsd1:localAuthenticatorConfigs>
                        <!--Optional:-->
                        <xsd1:stepOrder>1</xsd1:stepOrder>
                        <!--Optional:-->
                        <xsd1:subjectStep>false</xsd1:subjectStep>
                        <!--Optional:-->
                    </xsd1:authenticationSteps>
                    <xsd1:authenticationType>local</xsd1:authenticationType>
                    <!--Optional:-->
                    <xsd1:subjectClaimUri>http://wso2.org/claims/fullname</xsd1:subjectClaimUri>
                </xsd1:localAndOutBoundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:outboundProvisioningConfig>
                    <!--Zero or more repetitions:-->
                    <xsd1:provisionByRoleList></xsd1:provisionByRoleList>
                </xsd1:outboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:permissionAndRoleConfig></xsd1:permissionAndRoleConfig>
                <!--Optional:-->
                <xsd1:saasApp>false</xsd1:saasApp>
            </xsd:serviceProvider>
        </xsd:updateApplication>
    </soapenv:Body>
</soapenv:Envelope>
```

</details>

<details>
<summary>Click to view federated request</summary>


As there is only one `          <authenticationSteps>         `
configured here, there is no need to set the
`          authenticationSteps.stepOrder, authenticationSteps.subjectStep, authenticationSteps.attributeStep         `
attributes.

```xml
<xsd1:localAndOutBoundAuthenticationConfig>
    <!--Zero or more repetitions:-->
    <xsd1:authenticationSteps>
        <!--Zero or more repetitions:-->
        <xsd1:federatedIdentityProviders>
            <!--Zero or more repetitions:-->
            <xsd1:federatedAuthenticatorConfigs>
                <!--Optional:-->
                <xsd1:displayName>samlsso</xsd1:displayName>
                <!--Optional:-->
                <xsd1:name>SAMLSSOAuthenticator</xsd1:name>
                <!--Optional:-->
                <xsd1:valid>true</xsd1:valid>
            </xsd1:federatedAuthenticatorConfigs>
            <!--Optional:-->
            <xsd1:identityProviderName>TrustedIdP</xsd1:identityProviderName>
        </xsd1:federatedIdentityProviders>
        <!--Optional:-->
        <xsd1:stepOrder>1</xsd1:stepOrder>
        <!--Optional:-->
        <xsd1:subjectStep>false</xsd1:subjectStep>
        <!--Optional:-->
    </xsd1:authenticationSteps>
    <xsd1:authenticationType>federated</xsd1:authenticationType>
    <!--Optional:-->
    <xsd1:subjectClaimUri>http://wso2.org/claims/fullname</xsd1:subjectClaimUri>
</xsd1:localAndOutBoundAuthenticationConfig>
```

```xml
<soapenv:Envelope
    xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
    xmlns:xsd="http://org.apache.axis2/xsd"
    xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
    <soapenv:Header/>
    <soapenv:Body>
        <xsd:updateApplication>
            <!--Optional:-->
            <xsd:serviceProvider>
                <!--Optional:-->
                <xsd1:applicationID>2</xsd1:applicationID>
                <!--Optional:-->
                <xsd1:applicationName>travelocity.com</xsd1:applicationName>
                <!--Optional:-->
                <xsd1:claimConfig>
                    <!--Optional:-->
                    <xsd1:alwaysSendMappedLocalSubjectId>false</xsd1:alwaysSendMappedLocalSubjectId>
                    <!--Optional:-->
                    <xsd1:localClaimDialect>true</xsd1:localClaimDialect>
                </xsd1:claimConfig>
                <!--Optional:-->
                <xsd1:description>sample service provider</xsd1:description>
                <!--Optional:-->
                <xsd1:inboundAuthenticationConfig></xsd1:inboundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:inboundProvisioningConfig>
                    <!--Optional:-->
                    <xsd1:provisioningEnabled>false</xsd1:provisioningEnabled>
                    <!--Optional:-->
                    <xsd1:provisioningUserStore>PRIMARY</xsd1:provisioningUserStore>
                </xsd1:inboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:localAndOutBoundAuthenticationConfig>
                    <!--Zero or more repetitions:-->
                    <xsd1:authenticationSteps>
                        <!--Zero or more repetitions:-->
                        <xsd1:federatedIdentityProviders>
                            <!--Zero or more repetitions:-->
                            <xsd1:federatedAuthenticatorConfigs>
                                <!--Optional:-->
                                <xsd1:displayName>samlsso</xsd1:displayName>
                                <!--Optional:-->
                                <xsd1:name>SAMLSSOAuthenticator</xsd1:name>
                                <!--Optional:-->
                                <xsd1:valid>true</xsd1:valid>
                            </xsd1:federatedAuthenticatorConfigs>
                            <!--Optional:-->
                            <xsd1:identityProviderName>TrustedIdP</xsd1:identityProviderName>
                        </xsd1:federatedIdentityProviders>
                        <!--Optional:-->
                        <xsd1:stepOrder>1</xsd1:stepOrder>
                        <!--Optional:-->
                        <xsd1:subjectStep>false</xsd1:subjectStep>
                        <!--Optional:-->
                    </xsd1:authenticationSteps>
                    <xsd1:authenticationType>federated</xsd1:authenticationType>
                    <!--Optional:-->
                    <xsd1:subjectClaimUri>http://wso2.org/claims/fullname</xsd1:subjectClaimUri>
                </xsd1:localAndOutBoundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:outboundProvisioningConfig>
                    <!--Zero or more repetitions:-->
                    <xsd1:provisionByRoleList></xsd1:provisionByRoleList>
                </xsd1:outboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:permissionAndRoleConfig></xsd1:permissionAndRoleConfig>
                <!--Optional:-->
                <xsd1:saasApp>false</xsd1:saasApp>
            </xsd:serviceProvider>
        </xsd:updateApplication>
    </soapenv:Body>
</soapenv:Envelope>
```

</details>


<details>
<summary>Click to view the advanced format</summary>


Multiple `          <authenticationSteps>         ` can be configured here.
Therefore, in each `          <authenticationSteps>         `, the
stepOrder and whether the subject identifiers and attributes should be
used from that particular step.   

```xml
<xsd1:localAndOutBoundAuthenticationConfig>
    <!--Zero or more repetitions:-->
    <xsd1:authenticationSteps>
        <!--Zero or more repetitions:-->
        <xsd1:federatedIdentityProviders>
            <!--Zero or more repetitions:-->
            <xsd1:federatedAuthenticatorConfigs>
                <!--Optional:-->
                <xsd1:displayName>samlsso</xsd1:displayName>
                <!--Optional:-->
                <xsd1:name>SAMLSSOAuthenticator</xsd1:name>
                <!--Optional:-->
                <xsd1:valid>true</xsd1:valid>
            </xsd1:federatedAuthenticatorConfigs>
            <!--Optional:-->
            <xsd1:identityProviderName>TrustedIdP</xsd1:identityProviderName>
        </xsd1:federatedIdentityProviders>
        <!--Zero or more repetitions:-->
        <xsd1:localAuthenticatorConfigs>
            <!--Optional:-->
            <xsd1:displayName>basic</xsd1:displayName>
            <!--Optional:-->
            <xsd1:name>BasicAuthenticator</xsd1:name>
            <!--Optional:-->
            <xsd1:valid>true</xsd1:valid>
            <!--Zero or more repetitions:-->
        </xsd1:localAuthenticatorConfigs>
        <!--Optional:-->
        <xsd1:stepOrder>1</xsd1:stepOrder>
        <!--Optional:-->
        <xsd1:subjectStep>false</xsd1:subjectStep>
        <!--Optional:-->
    </xsd1:authenticationSteps>
    <xsd1:authenticationType>flow</xsd1:authenticationType>
    <!--Optional:-->
    <xsd1:subjectClaimUri>http://wso2.org/cla
```

```xml
<soapenv:Envelope
    xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
    xmlns:xsd="http://org.apache.axis2/xsd"
    xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
    <soapenv:Header/>
    <soapenv:Body>
        <xsd:updateApplication>
            <!--Optional:-->
            <xsd:serviceProvider>
                <!--Optional:-->
                <xsd1:applicationID>2</xsd1:applicationID>
                <!--Optional:-->
                <xsd1:applicationName>travelocity.com</xsd1:applicationName>
                <!--Optional:-->
                <xsd1:claimConfig>
                    <!--Optional:-->
                    <xsd1:alwaysSendMappedLocalSubjectId>false</xsd1:alwaysSendMappedLocalSubjectId>
                    <!--Optional:-->
                    <xsd1:localClaimDialect>true</xsd1:localClaimDialect>
                </xsd1:claimConfig>
                <!--Optional:-->
                <xsd1:description>sample service provider</xsd1:description>
                <!--Optional:-->
                <xsd1:inboundAuthenticationConfig></xsd1:inboundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:inboundProvisioningConfig>
                    <!--Optional:-->
                    <xsd1:provisioningEnabled>false</xsd1:provisioningEnabled>
                    <!--Optional:-->
                    <xsd1:provisioningUserStore>PRIMARY</xsd1:provisioningUserStore>
                </xsd1:inboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:localAndOutBoundAuthenticationConfig>
                    <!--Zero or more repetitions:-->
                    <xsd1:authenticationSteps>
                        <!--Zero or more repetitions:-->
                        <xsd1:federatedIdentityProviders>
                            <!--Zero or more repetitions:-->
                            <xsd1:federatedAuthenticatorConfigs>
                                <!--Optional:-->
                                <xsd1:displayName>samlsso</xsd1:displayName>
                                <!--Optional:-->
                                <xsd1:name>SAMLSSOAuthenticator</xsd1:name>
                                <!--Optional:-->
                                <xsd1:valid>true</xsd1:valid>
                            </xsd1:federatedAuthenticatorConfigs>
                            <!--Optional:-->
                            <xsd1:identityProviderName>TrustedIdP</xsd1:identityProviderName>
                        </xsd1:federatedIdentityProviders>
                        <!--Zero or more repetitions:-->
                        <xsd1:localAuthenticatorConfigs>
                            <!--Optional:-->
                            <xsd1:displayName>basic</xsd1:displayName>
                            <!--Optional:-->
                            <xsd1:name>BasicAuthenticator</xsd1:name>
                            <!--Optional:-->
                            <xsd1:valid>true</xsd1:valid>
                            <!--Zero or more repetitions:-->
                        </xsd1:localAuthenticatorConfigs>
                        <!--Optional:-->
                        <xsd1:stepOrder>1</xsd1:stepOrder>
                        <!--Optional:-->
                        <xsd1:subjectStep>false</xsd1:subjectStep>
                        <!--Optional:-->
                    </xsd1:authenticationSteps>
                    <xsd1:authenticationType>flow</xsd1:authenticationType>
                    <!--Optional:-->
                    <xsd1:subjectClaimUri>http://wso2.org/claims/fullname</xsd1:subjectClaimUri>
                </xsd1:localAndOutBoundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:outboundProvisioningConfig>
                    <!--Zero or more repetitions:-->
                    <xsd1:provisionByRoleList></xsd1:provisionByRoleList>
                </xsd1:outboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:permissionAndRoleConfig></xsd1:permissionAndRoleConfig>
                <!--Optional:-->
                <xsd1:saasApp>false</xsd1:saasApp>
            </xsd:serviceProvider>
        </xsd:updateApplication>
    </soapenv:Body>
</soapenv:Envelope>            
```

</details>

#### Request path authenticator

Specify configurations related to zero or more request path authenticators.   

<table><thead><tr className={"header"}><th><p>{"Parameter"}</p></th><th><p>{"Type"}</p></th><th><p>{"Description"}</p></th></tr></thead><tbody><tr className={"odd"}><td><p>{"displayName"}</p></td><td><p>{"String"}</p></td><td><p>{"The name that displays"}</p></td></tr><tr className={"even"}><td><p>{"enabled"}</p></td><td><p>{"Boolean"}</p></td><td><p>{"true - enable"}</p><p>{"false - deisable"}</p></td></tr><tr className={"odd"}><td><p>{"name"}</p></td><td><p>{"String"}</p></td><td><p>{"OAuthRequestPathAuthenticator"}</p><p>{"BasicAuthRequestPathAuthenticator"}</p></td></tr><tr className={"even"}><td><p>{"valid"}</p></td><td><p>{"boolean"}</p></td><td><p>{"true - valid"}</p><p>{"false - invalid"}</p></td></tr><tr className={"odd"}><td><p>{"properties"}</p></td><td><p>{"Property"}</p></td><td><p>{"List of properties in a array"}</p></td></tr></tbody></table>


<details>
<summary>Click to view request</summary>


```xml
<xsd1:requestPathAuthenticatorConfigs>
    <!--Optional:-->
    <xsd1:name>BasicAuthRequestPathAuthenticator</xsd1:name>
    <!--Optional:-->
    <xsd1:valid>true</xsd1:valid>
</xsd1:requestPathAuthenticatorConfigs>
<xsd1:requestPathAuthenticatorConfigs>
    <!--Optional:-->
    <xsd1:name>OAuthRequestPathAuthenticator</xsd1:name>
    <!--Optional:-->
    <xsd1:valid>true</xsd1:valid>
</xsd1:requestPathAuthenticatorConfigs>
```

```xml
<soapenv:Envelope
    xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
    xmlns:xsd="http://org.apache.axis2/xsd"
    xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
    <soapenv:Header/>
    <soapenv:Body>
        <xsd:updateApplication>
            <!--Optional:-->
            <xsd:serviceProvider>
                <!--Optional:-->
                <xsd1:applicationID>2</xsd1:applicationID>
                <!--Optional:-->
                <xsd1:applicationName>travelocity.com</xsd1:applicationName>
                <!--Optional:-->
                <xsd1:claimConfig>
                    <!--Optional:-->
                    <xsd1:alwaysSendMappedLocalSubjectId>false</xsd1:alwaysSendMappedLocalSubjectId>
                    <!--Optional:-->
                    <xsd1:localClaimDialect>true</xsd1:localClaimDialect>
                </xsd1:claimConfig>
                <!--Optional:-->
                <xsd1:description>sample service provider</xsd1:description>
                <!--Optional:-->
                <xsd1:inboundAuthenticationConfig></xsd1:inboundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:inboundProvisioningConfig>
                    <!--Optional:-->
                    <xsd1:provisioningEnabled>false</xsd1:provisioningEnabled>
                    <!--Optional:-->
                    <xsd1:provisioningUserStore>PRIMARY</xsd1:provisioningUserStore>
                </xsd1:inboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:localAndOutBoundAuthenticationConfig>
                    <!--Optional:-->
                    <xsd1:alwaysSendBackAuthenticatedListOfIdPs>false</xsd1:alwaysSendBackAuthenticatedListOfIdPs>
                    <!--Optional:-->
                    <xsd1:authenticationStepForAttributes></xsd1:authenticationStepForAttributes>
                    <!--Optional:-->
                    <xsd1:authenticationStepForSubject></xsd1:authenticationStepForSubject>
                    <xsd1:authenticationType>default</xsd1:authenticationType>
                    <!--Optional:-->
                    <xsd1:subjectClaimUri>http://wso2.org/claims/fullname</xsd1:subjectClaimUri>
                </xsd1:localAndOutBoundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:outboundProvisioningConfig>
                    <!--Zero or more repetitions:-->
                    <xsd1:provisionByRoleList></xsd1:provisionByRoleList>
                </xsd1:outboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:permissionAndRoleConfig></xsd1:permissionAndRoleConfig>
                <!--Zero or more repetitions:-->
                <xsd1:requestPathAuthenticatorConfigs>
                    <!--Optional:-->
                    <xsd1:name>BasicAuthRequestPathAuthenticator</xsd1:name>
                    <!--Optional:-->
                    <xsd1:valid>true</xsd1:valid>
                </xsd1:requestPathAuthenticatorConfigs>
                <xsd1:requestPathAuthenticatorConfigs>
                    <!--Optional:-->
                    <xsd1:name>OAuthRequestPathAuthenticator</xsd1:name>
                    <!--Optional:-->
                    <xsd1:valid>true</xsd1:valid>
                </xsd1:requestPathAuthenticatorConfigs>
                <!--Optional:-->
                <xsd1:saasApp>false</xsd1:saasApp>
            </xsd:serviceProvider>
        </xsd:updateApplication>
    </soapenv:Body>
</soapenv:Envelope>      
```

</details>

#### Outbound provisioning 

To configure the outbound provisioning of the service provider, use the following parameters.    

<table><thead><tr className={"header"}><th><p>{"Parameter"}</p></th><th><p>{"Type"}</p></th><th><p>{"Description"}</p></th></tr></thead><tbody><tr className={"odd"}><td><p>{"provisionByRoleList"}</p></td><td><p>{"String"}</p></td><td><p>{"-"}</p></td></tr><tr className={"even"}><td><p>{"provisioningIdentityProviders"}</p></td><td><p>{"IdentityProvider"}</p></td><td><p>{"To configure provisioning IdPs, there should be one or more registered IdPs, with at least one outbound provisioning connector enabled."}</p><p>{"Include the IdP name and provisioning connector name and specify whether to enable JiT provisioning with the request."}</p></td></tr></tbody></table>

<details>
<summary>Click to view request</summary>


```xml
<xsd1:outboundProvisioningConfig>
    <!--Zero or more repetitions:-->
    <xsd1:provisionByRoleList></xsd1:provisionByRoleList>
    <!--Zero or more repetitions:-->
    <xsd1:provisioningIdentityProviders>
        <!--Optional:-->
        <xsd1:defaultProvisioningConnectorConfig>
            <!--Optional:-->
            <xsd1:blocking>false</xsd1:blocking>
            <!--Optional:-->
            <xsd1:enabled>false</xsd1:enabled>
            <!--Optional:-->
            <xsd1:name>scim</xsd1:name>
            <!--Optional:-->
        </xsd1:defaultProvisioningConnectorConfig>
        <!--Optional:-->
        <xsd1:identityProviderName>TrustedIdP</xsd1:identityProviderName>
        <!--Optional:-->
        <xsd1:justInTimeProvisioningConfig>
            <!--Optional:-->
            <xsd1:dumbMode>false</xsd1:dumbMode>
            <!--Optional:-->
            <xsd1:provisioningEnabled>true</xsd1:provisioningEnabled>
        </xsd1:justInTimeProvisioningConfig>
    </xsd1:provisioningIdentityProviders>
</xsd1:outboundProvisioningConfig>
```

```xml
<soapenv:Envelope
    xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
    xmlns:xsd="http://org.apache.axis2/xsd"
    xmlns:xsd1="http://model.common.application.identity.carbon.wso2.org/xsd">
    <soapenv:Header/>
    <soapenv:Body>
        <xsd:updateApplication>
            <!--Optional:-->
            <xsd:serviceProvider>
                <!--Optional:-->
                <xsd1:applicationID>2</xsd1:applicationID>
                <!--Optional:-->
                <xsd1:applicationName>travelocity.com</xsd1:applicationName>
                <!--Optional:-->
                <xsd1:claimConfig>
                    <!--Optional:-->
                    <xsd1:alwaysSendMappedLocalSubjectId>false</xsd1:alwaysSendMappedLocalSubjectId>
                    <!--Zero or more repetitions:-->
                    <xsd1:claimMappings>
                        <!--Optional:-->
                        <xsd1:localClaim>
                            <!--Optional:-->
                            <xsd1:claimUri>http://wso2.org/claims/givenname</xsd1:claimUri>
                        </xsd1:localClaim>
                        <!--Optional:-->
                        <xsd1:mandatory>true</xsd1:mandatory>
                        <!--Optional:-->
                        <xsd1:remoteClaim>
                            <!--Optional:-->
                            <xsd1:claimUri>name</xsd1:claimUri>
                        </xsd1:remoteClaim>
                        <!--Optional:-->
                        <xsd1:requested>true</xsd1:requested>
                    </xsd1:claimMappings>
                    <xsd1:claimMappings>
                        <!--Optional:-->
                        <xsd1:localClaim>
                            <!--Optional:-->
                            <xsd1:claimUri>http://wso2.org/claims/role</xsd1:claimUri>
                        </xsd1:localClaim>
                        <!--Optional:-->
                        <xsd1:mandatory>true</xsd1:mandatory>
                        <!--Optional:-->
                        <xsd1:remoteClaim>
                            <!--Optional:-->
                            <xsd1:claimUri>role</xsd1:claimUri>
                        </xsd1:remoteClaim>
                        <!--Optional:-->
                        <xsd1:requested>true</xsd1:requested>
                    </xsd1:claimMappings>
                    <!--Optional:-->
                    <xsd1:localClaimDialect>false</xsd1:localClaimDialect>
                    <!--Optional:-->
                    <xsd1:roleClaimURI>role</xsd1:roleClaimURI>
                    <!--Optional:-->
                    <xsd1:userClaimURI>user</xsd1:userClaimURI>
                </xsd1:claimConfig>
                <!--Optional:-->
                <xsd1:description>sample service provider</xsd1:description>
                <!--Optional:-->
                <xsd1:inboundAuthenticationConfig></xsd1:inboundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:inboundProvisioningConfig>
                    <!--Optional:-->
                    <xsd1:provisioningEnabled>false</xsd1:provisioningEnabled>
                    <!--Optional:-->
                    <xsd1:provisioningUserStore>PRIMARY</xsd1:provisioningUserStore>
                </xsd1:inboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:localAndOutBoundAuthenticationConfig>
                    <!--Optional:-->
                    <xsd1:alwaysSendBackAuthenticatedListOfIdPs>false</xsd1:alwaysSendBackAuthenticatedListOfIdPs>
                    <!--Optional:-->
                    <xsd1:authenticationStepForAttributes></xsd1:authenticationStepForAttributes>
                    <!--Optional:-->
                    <xsd1:authenticationStepForSubject></xsd1:authenticationStepForSubject>
                    <xsd1:authenticationType>default</xsd1:authenticationType>
                    <!--Optional:-->
                    <xsd1:subjectClaimUri>name</xsd1:subjectClaimUri>
                </xsd1:localAndOutBoundAuthenticationConfig>
                <!--Optional:-->
                <xsd1:outboundProvisioningConfig>
                    <!--Zero or more repetitions:-->
                    <xsd1:provisionByRoleList></xsd1:provisionByRoleList>
                    <!--Zero or more repetitions:-->
                    <xsd1:provisioningIdentityProviders>
                        <!--Optional:-->
                        <xsd1:defaultProvisioningConnectorConfig>
                            <!--Optional:-->
                            <xsd1:blocking>false</xsd1:blocking>
                            <!--Optional:-->
                            <xsd1:enabled>false</xsd1:enabled>
                            <!--Optional:-->
                            <xsd1:name>scim</xsd1:name>
                            <!--Optional:-->
                        </xsd1:defaultProvisioningConnectorConfig>
                        <!--Optional:-->
                        <xsd1:identityProviderName>TrustedIdP</xsd1:identityProviderName>
                        <!--Optional:-->
                        <xsd1:justInTimeProvisioningConfig>
                            <!--Optional:-->
                            <xsd1:dumbMode>false</xsd1:dumbMode>
                            <!--Optional:-->
                            <xsd1:provisioningEnabled>true</xsd1:provisioningEnabled>
                        </xsd1:justInTimeProvisioningConfig>
                    </xsd1:provisioningIdentityProviders>
                </xsd1:outboundProvisioningConfig>
                <!--Optional:-->
                <xsd1:permissionAndRoleConfig></xsd1:permissionAndRoleConfig>
                <!--Optional:-->
                <xsd1:saasApp>false</xsd1:saasApp>
            </xsd:serviceProvider>
        </xsd:updateApplication>
    </soapenv:Body>
</soapenv:Envelope>
```

</details>

### deleteApplication

<table><tbody><tr className={"even"}><th>{"Description"}</th><td>{"A service provider is deleted based on the application name. The input parameters and the format of the request should be as follows."}</td></tr><tr className={"odd"}><th>{"Permission Level"}</th><td>{"/permission/admin/manage"}</td></tr><tr className={"even"}><th>{"Input Parameters"}</th><td><ul><li><code>{"applicationName"}</code>{" "}<code>{"[String]"}</code>{": This is the application name."}</li></ul></td></tr><tr><th>{"Request"}</th><td><div><pre><code>{"<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\" xmlns:xsd=\"http://org.apache.axis2/xsd\">\n <soapenv:Header/>\n <soapenv:Body>\n    <xsd:deleteApplication>\n       <!--Optional:-->\n       <xsd:applicationName>TestSP</xsd:applicationName>\n    </xsd:deleteApplication>\n </soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr><tr><th>{"Response"}</th><td><div><pre><code>{"<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\">\n <soapenv:Body>\n    <ns:deleteApplicationResponse xmlns:ns=\"http://org.apache.axis2/xsd\">\n       <ns:return xsi:nil=\"true\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\"/>\n    </ns:deleteApplicationResponse>\n </soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr></tbody></table>

### getAllApplicationBasicInfo

<table><tbody><tr className={"even"}><th>{"Description"}</th><td>{"This operation can use to get all available service provider names and their descriptions."}</td></tr><tr className={"odd"}><th>{"Permission Level"}</th><td>{"/permission/admin/manage"}</td></tr><tr><th>{"Request"}</th><td><div><pre><code>{"<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\" xmlns:xsd=\"http://org.apache.axis2/xsd\">\n <soapenv:Header/>\n <soapenv:Body>\n    <xsd:getAllApplicationBasicInfo/>\n </soapenv:Body>\n<</soapenv:Envelope>"}</code></pre></div></td></tr><tr><th>{"Response"}</th><td><div><pre><code>{"<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\">\n <soapenv:Body>\n    <ns:getAllApplicationBasicInfoResponse xmlns:ns=\"http://org.apache.axis2/xsd\" xmlns:ax2115=\"http://core.carbon.wso2.org/xsd\" xmlns:ax2114=\"http://mgt.application.identity.carbon.wso2.org/xsd\" xmlns:ax2120=\"http://common.application.identity.carbon.wso2.org/xsd\" xmlns:ax2117=\"http://model.common.application.identity.carbon.wso2.org/xsd\">\n <ns:return xsi:type=\"ax2117:ApplicationBasicInfo\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\">\n          <ax2117:applicationName>TestSP1</ax2117:applicationName>\n          <ax2117:description>Test Service Provider-1</ax2117:description>\n       </ns:return>\n    </ns:getAllApplicationBasicInfoResponse>\n </soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr></tbody></table>

### getAllIdentityProviders

<table><tbody><tr className={"even"}><th>{"Description"}</th><td>{"This operation retrieves the available identity providers."}</td></tr><tr className={"odd"}><th>{"Permission Level"}</th><td>{"/permission/admin/manage"}</td></tr><tr><th>{"Request"}</th><td><div><pre><code>{"<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\" xmlns:xsd=\"http://org.apache.axis2/xsd\">\n <soapenv:Header/>\n <soapenv:Body>\n    <xsd:getAllIdentityProviders/>\n <</soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr><tr><th>{"Response"}</th><td><div><pre><code>{"<soapenv:Envelope\n    xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\">\n  <soapenv:Body>\n      <ns:getAllIdentityProvidersResponse\n          xmlns:ns=\"http://org.apache.axis2/xsd\"\n          xmlns:ax2115=\"http://core.carbon.wso2.org/xsd\"\n          xmlns:ax2114=\"http://mgt.application.identity.carbon.wso2.org/xsd\"\n          xmlns:ax2120=\"http://common.application.identity.carbon.wso2.org/xsd\"\n          xmlns:ax2117=\"http://model.common.application.identity.carbon.wso2.org/xsd\">\n          <ns:return xsi:type=\"ax2117:IdentityProvider\"\n              xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\">\n              <ax2117:alias xsi:nil=\"true\"/>\n              <ax2117:certificate xsi:nil=\"true\"/>\n              <ax2117:claimConfig xsi:nil=\"true\"/>\n              <ax2117:defaultAuthenticatorConfig xsi:nil=\"true\"/>\n              <ax2117:defaultProvisioningConnectorConfig xsi:nil=\"true\"/>\n              <ax2117:displayName xsi:nil=\"true\"/>\n              <ax2117:enable>true</ax2117:enable>\n              <ax2117:federatedAuthenticatorConfigs xsi:type=\"ax2117:FederatedAuthenticatorConfig\">\n          ...</ax2117:federatedAuthenticatorConfigs>\n  <<ax2117:federationHub>false</ax2117:federationHub>\n              <ax2117:homeRealmId xsi:nil=\"true\"/>\n              <ax2117:identityProviderDescription xsi:nil=\"true\"/>\n              <ax2117:identityProviderName>TestIdP</ax2117:identityProviderName>\n              <ax2117:justInTimeProvisioningConfig xsi:nil=\"true\"/>\n              <ax2117:permissionAndRoleConfig xsi:nil=\"true\"/>\n              <ax2117:primary>false</ax2117:primary>\n              <ax2117:provisioningConnectorConfigs xsi:type=\"ax2117:ProvisioningConnectorConfig\">...\n          </ax2117:provisioningConnectorConfigs>\n              <ax2117:provisioningRole xsi:nil=\"true\"/>\n          </ns:return>\n      </ns:getAllIdentityProvidersResponse>\n  </soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr></tbody></table>

### getAllLocalAuthenticators

<table><tbody><tr className={"even"}><th>{"Description"}</th><td>{"This operation retrieves the available local authenticators."}</td></tr><tr className={"odd"}><th>{"Permission Level"}</th><td>{"/permission/admin/manage"}</td></tr><tr><th>{"Request"}</th><td><div><pre><code>{"<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\" xmlns:xsd=\"http://org.apache.axis2/xsd\">\n <soapenv:Header/>\n <<soapenv:Body>\n    <xsd:getAllLocalAuthenticators/>\n </soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr><tr><th>{"Response"}</th><td><div><pre><code>{"<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\">\n <soapenv:Body>\n    <ns:getAllLocalAuthenticatorsResponse xmlns:ns=\"http://org.apache.axis2/xsd\" xmlns:ax2115=\"http://core.carbon.wso2.org/xsd\" xmlns:ax2114=\"http://mgt.application.identity.carbon.wso2.org/xsd\" xmlns:ax2120=\"http://common.application.identity.carbon.wso2.org/xsd\" xmlns:ax2117=\"http://model.common.application.identity.carbon.wso2.org/xsd\">\n       <ns:return xsi:type=\"ax2117:LocalAuthenticatorConfig\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\">\n          <ax2117:displayName>basic</ax2117:displayName>\n          <ax2117:enabled>false</ax2117:enabled>\n          <ax2117:name>BasicAuthenticator</ax2117:name>\n          <ax2117:valid>true</ax2117:valid>\n       </ns:return>\n       <ns:return xsi:type=\"ax2117:LocalAuthenticatorConfig\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\">\n          <ax2117:displayName>iwa</ax2117:displayName>\n          <ax2117:enabled>false</ax2117:enabled>\n          <ax2117:name>IWAAuthenticator</ax2117:name>\n          <ax2117:valid>true</ax2117:valid>\n       </ns:return>\n    </ns:getAllLocalAuthenticatorsResponse>\n </soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr></tbody></table>


### getAllLocalClaimUris

<table><tbody><tr className={"even"}><th>{"Description"}</th><td>{"This operation retrieves the available claim URI values that are in "}<code>{"http://wso2.org/claims"}</code>{" dialect."}</td></tr><tr className={"odd"}><th>{"Permission Level"}</th><td>{"/permission/admin/manage"}</td></tr><tr><th>{"Request"}</th><td><div><pre><code>{"<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\" xmlns:xsd=\"http://org.apache.axis2/xsd\">\n <soapenv:Header/>\n <<soapenv:Body>\n    <xsd:getAllLocalClaimUris/>\n </soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr><tr><th>{"Response"}</th><td><div><pre><code>{"<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\">\n <soapenv:Body>\n    <ns:getAllLocalClaimUrisResponse xmlns:ns=\"http://org.apache.axis2/xsd\" xmlns:ax2115=\"http://core.carbon.wso2.org/xsd\" xmlns:ax2114=\"http://mgt.application.identity.carbon.wso2.org/xsd\" xmlns:ax2120=\"http://common.application.identity.carbon.wso2.org/xsd\" xmlns:ax2117=\"http://model.common.application.identity.carbon.wso2.org/xsd\">\n       <ns:return>http://wso2.org/claims/otherphone</ns:return>\n       <ns:return>http://wso2.org/claims/dob</ns:return>\n       <ns:return>http://wso2.org/claims/primaryChallengeQuestion</ns:return>\n       <ns:return>http://wso2.org/claims/role</ns:return>\n       <ns:return>http://wso2.org/claims/challengeQuestion1</ns:return>\n       <ns:return>http://wso2.org/claims/telephone</ns:return>\n       <ns:return>http://wso2.org/claims/mobile</ns:return>\n       <ns:return>http://wso2.org/claims/country</ns:return>\n       <ns:return>http://wso2.org/claims/challengeQuestionUris</ns:return>\n       <ns:return>http://wso2.org/claims/postalcode</ns:return>\n       <ns:return>http://wso2.org/claims/challengeQuestion2</ns:return>\n       <ns:return>http://wso2.org/claims/identity/accountLocked</ns:return>\n       <ns:return>http://wso2.org/claims/nickname</ns:return>\n       <ns:return>http://wso2.org/claims/streetaddress</ns:return>\n       <ns:return>http://wso2.org/claims/url</ns:return>\n       <ns:return>http://wso2.org/claims/givenname</ns:return>\n       <ns:return>http://wso2.org/claims/emailaddress</ns:return>\n       <ns:return>http://wso2.org/claims/oneTimePassword</ns:return>\n       <ns:return>http://wso2.org/claims/region</ns:return>\n       <ns:return>http://wso2.org/claims/gender</ns:return>\n       <ns:return>http://wso2.org/claims/fullname</ns:return>\n       <ns:return>http://wso2.org/claims/passwordTimestamp</ns:return>\n       <ns:return>http://wso2.org/claims/title</ns:return>\n       <ns:return>http://wso2.org/claims/locality</ns:return>\n       <ns:return>http://wso2.org/claims/stateorprovince</ns:return>\n       <ns:return>http://wso2.org/claims/im</ns:return>\n       <ns:return>http://wso2.org/claims/organization</ns:return>\n       <ns:return>http://wso2.org/claims/lastname</ns:return>\n    </ns:getAllLocalClaimUrisResponse>\n </soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr></tbody></table>

### getAllRequestPathAuthenticators

<table><tbody><tr className={"even"}><th>{"Description"}</th><td>{"This operation retrieves the available request patch authenticators."}</td></tr><tr className={"odd"}><th>{"Permission Level"}</th><td>{"/permission/admin/manage"}</td></tr><tr><th>{"Request"}</th><td><div><pre><code>{"<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\" xmlns:xsd=\"http://org.apache.axis2/xsd\">\n <soapenv:Header/>\n <soapenv:Body>\n    <xsd:getAllRequestPathAuthenticators/>\n </soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr><tr><th>{"Response"}</th><td><div><pre><code>{"<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\">\n <soapenv:Body>\n    <ns:getAllRequestPathAuthenticatorsResponse xmlns:ns=\"http://org.apache.axis2/xsd\" xmlns:ax2115=\"http://core.carbon.wso2.org/xsd\" xmlns:ax2114=\"http://mgt.application.identity.carbon.wso2.org/xsd\" xmlns:ax2120=\"http://common.application.identity.carbon.wso2.org/xsd\" xmlns:ax2117=\"http://model.common.application.identity.carbon.wso2.org/xsd\">\n       <ns:return xsi:type=\"ax2117:RequestPathAuthenticatorConfig\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\">\n          <ax2117:displayName>basic-auth</ax2117:displayName>\n          <ax2117:enabled>false</ax2117:enabled>\n          <ax2117:name>BasicAuthRequestPathAuthenticator</ax2117:name>\n          <ax2117:valid>true</ax2117:valid>\n       </ns:return>\n       <ns:return xsi:type=\"ax2117:RequestPathAuthenticatorConfig\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\">\n          <ax2117:displayName>oauth-bearer</ax2117:displayName>\n          <ax2117:enabled>false</ax2117:enabled>\n          <ax2117:name>OAuthRequestPathAuthenticator</ax2117:name>\n          <ax2117:valid>true</ax2117:valid>\n       </ns:return>\n    </ns:getAllRequestPathAuthenticatorsResponse>\n </soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr></tbody></table>
 

### getApplication

<table><tbody><tr className={"even"}><th>{"Description"}</th><td>{"This operation retrieves the the service provider information while passing the application name."}</td></tr><tr className={"odd"}><th>{"Permission Level"}</th><td>{"/permission/admin/manage"}</td></tr><tr className={"even"}><th>{"Input Parameters"}</th><td><ul><li><code>{"applicationName"}</code>{" "}<code>{"[String]"}</code>{": This is the application name."}</li></ul></td></tr><tr><th>{"Request"}</th><td><div><pre><code>{"<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\" xmlns:xsd=\"http://org.apache.axis2/xsd\">\n <soapenv:Header/>\n <soapenv:Body>\n    <xsd:getApplication>\n       <!--Optional:-->\n       <xsd:applicationName>TestSP</xsd:applicationName>\n    </xsd:getApplication>\n <</soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr><tr><th>{"Response"}</th><td><div><pre><code>{"<soapenv:Envelope\n    xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\">\n    <soapenv:Body>\n        <ns:getApplicationResponse\n            xmlns:ns=\"http://org.apache.axis2/xsd\">\n            <ns:return xsi:type=\"ax2117:ServiceProvider\"\n                xmlns:ax2115=\"http://core.carbon.wso2.org/xsd\"\n                xmlns:ax2114=\"http://mgt.application.identity.carbon.wso2.org/xsd\"\n                xmlns:ax2120=\"http://common.application.identity.carbon.wso2.org/xsd\"\n                xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\"\n                xmlns:ax2117=\"http://model.common.application.identity.carbon.wso2.org/xsd\">\n                <ax2117:applicationID>4</ax2117:applicationID>\n                <ax2117:applicationName>TestSP</ax2117:applicationName>\n                <ax2117:claimConfig xsi:type=\"ax2117:ClaimConfig\">...\n            </ax2117:claimConfig>\n                <ax2117:description>Description</ax2117:description>\n                <ax2117:inboundAuthenticationConfig xsi:type=\"ax2117:InboundAuthenticationConfig\">\n            ...\n            </ax2117:inboundAuthenticationConfig>\n                <ax2117:localAndOutBoundAuthenticationConfig xsi:type=\"ax2117:LocalAndOutboundAuthenticationConfig\">\n            ...</ax2117:localAndOutBoundAuthenticationConfig>\n                <ax2117:outboundProvisioningConfig xsi:type=\"ax2117:OutboundProvisioningConfig\">\n            ..    \n            </ax2117:outboundProvisioningConfig>\n                <ax2117:owner xsi:type=\"ax2117:User\">\n                ...\n            </ax2117:owner>\n                <ax2117:permissionAndRoleConfig xsi:type=\"ax2117:PermissionsAndRoleConfig\"/>\n                <ax2117:saasApp>true</ax2117:saasApp>\n            </ns:return>\n        </ns:getApplicationResponse>\n    </soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr></tbody></table>

### getIdentityProvider

<table><tbody><tr className={"even"}><th>{"Description"}</th><td>{"This operation retrieves the identity provider information while passing the identity provider name."}</td></tr><tr className={"odd"}><th>{"Permission Level"}</th><td>{"/permission/admin/manage"}</td></tr><tr className={"even"}><th>{"Input Parameters"}</th><td><ul><li><code>{"federatedIdPName"}</code>{" "}<code>{"[String]"}</code>{": This is the identity provider name."}</li></ul></td></tr><tr><th>{"Request"}</th><td><div><pre><code>{"<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\" xmlns:xsd=\"http://org.apache.axis2/xsd\">\n <soapenv:Header/>\n <soapenv:Body>\n    <xsd:getIdentityProvider>\n       <!--Optional:-->\n       <xsd:federatedIdPName>TestIdP</xsd:federatedIdPName>\n    </xsd:getIdentityProvider>\n </soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr><tr><th>{"Response"}</th><td><div><pre><code>{"<soapenv:Envelope\n    xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\">\n  <soapenv:Body>\n      <ns:getIdentityProvidersResponse\n          xmlns:ns=\"http://org.apache.axis2/xsd\"\n          xmlns:ax2115=\"http://core.carbon.wso2.org/xsd\"\n          xmlns:ax2114=\"http://mgt.application.identity.carbon.wso2.org/xsd\"\n          xmlns:ax2120=\"http://common.application.identity.carbon.wso2.org/xsd\"\n          xmlns:ax2117=\"http://model.common.application.identity.carbon.wso2.org/xsd\">\n          <ns:return xsi:type=\"ax2117:IdentityProvider\"\n              xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\">\n              <ax2117:alias xsi:nil=\"true\"/>\n              <ax2117:certificate xsi:nil=\"true\"/>\n              <ax2117:claimConfig xsi:nil=\"true\"/>\n              <ax2117:defaultAuthenticatorConfig xsi:nil=\"true\"/>\n              <ax2117:defaultProvisioningConnectorConfig xsi:nil=\"true\"/>\n              <ax2117:displayName xsi:nil=\"true\"/>\n              <ax2117:enable>true</ax2117:enable>\n              <ax2117:federatedAuthenticatorConfigs xsi:type=\"ax2117:FederatedAuthenticatorConfig\">\n          ...</ax2117:federatedAuthenticatorConfigs>\n              <ax2117:federationHub>false</ax2117:federationHub>\n              <ax2117:homeRealmId xsi:nil=\"true\"/>\n              <ax2117:identityProviderDescription xsi:nil=\"true\"/>\n              <ax2117:identityProviderName>TestIdP</ax2117:identityProviderName>\n              <ax2117:justInTimeProvisioningConfig xsi:nil=\"true\"/>\n              <ax2117:permissionAndRoleConfig xsi:nil=\"true\"/>\n              <ax2117:primary>false</ax2117:primary>\n              <ax2117:provisioningConnectorConfigs xsi:type=\"ax2117:ProvisioningConnectorConfig\">...\n          </ax2117:provisioningConnectorConfigs>\n              <ax2117:provisioningRole xsi:nil=\"true\"/>\n          </ns:return>\n      </ns:getIdentityProvidersResponse>\n  </soapenv:Body>\n</soapenv:Envelope>"}</code></pre></div></td></tr></tbody></table>
