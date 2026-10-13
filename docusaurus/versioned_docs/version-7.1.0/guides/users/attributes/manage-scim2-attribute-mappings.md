---
title: Manage SCIM 2.0 attribute mappings
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/7.1.0/docs/guides/users/attributes/manage-scim2-attribute-mappings.md
---

# Manage SCIM 2.0 attribute mappings

Attributes in your organization are mapped to the following SCIM 2.0 schema mappings:

<details>
<summary>Core schema</summary>


The core schema defines a set of common attributes that are included in every SCIM resource, such as unique identifiers and resource metadata. Core schema attributes are an integral part of every base resource schema. Unlike other schemas, the core schema does not have its own URI and is inherently included in every resource definition.

Read about core schema in the [SCIM2 specification](https://datatracker.ietf.org/doc/html/rfc7643#section-3.1).

</details>

<details>
<summary>User schema</summary>


The user schema defines attributes specific to user resources, in addition to the core schema attributes. This schema is identified by the URI `urn:ietf:params:scim:schemas:core:2.0:User`. Attributes in the user schema include details such as the user's name, email addresses, phone numbers, roles, and other identity-related properties.

Read about user schema in the [SCIM2 specification](https://datatracker.ietf.org/doc/html/rfc7643#section-4.1).

</details>

<details>
<summary>Enterprise schema</summary>


The enterprise schema extends the user schema to include attributes commonly used for representing users in business or enterprise environments. This schema is identified by the URI `urn:ietf:params:scim:schemas:extension:enterprise:2.0:User`. Attributes in the enterprise schema include details such as the user’s department, manager, cost center, and other organization-specific properties.

Read about enterprise schema in the [SCIM2 specification](https://datatracker.ietf.org/doc/html/rfc7643#section-4.3).

</details>



<details>
<summary>System schema</summary>


The system schema is a user extension provided by WSO2 Identity Server to support attributes related to the product features and functionalities. It includes user attributes that are essential for Identity Server-specific operations, as well as general user attributes not covered in the standard SCIM specification.

</details>



<details>
<summary>Custom schema</summary>


Custom schema attributes provide the flexibility to extend standard SCIM schemas with additional fields to fit the needs of your organization. While other attribute schemas cannot be modified, you can freely add or delete custom schema attributes.




Custom user attributes in WSO2 Identity Server are created under the `urn:scim:schemas:extension:custom:User` schema. 

You can configure this schema in the following ways by adding configuration to `<IS_HOME>/repository/conf/deployment.toml`

- To disable this schema,
     
    ```toml
    [scim2]
    enable_custom_schema_extension = false
    ```

- To rename this schema,

    ```toml
    [scim2]
    custom_user_schema_uri = "urn:scim:custom:schema:new"
    ```

</details>
    



## View SCIM 2.0 attributes
To view the SCIM 2 attributes mapped to user attributes in your organization:

1. On the WSO2 Identity Server Console, go to **User Attributes & Stores** > **Attributes**.
2. Under **Manage Attribute Mappings**, click **SCIM 2.0**.

    ![View SCIM2 attributes](../../../../../assets/img/guides/organization/attributes/attribute-mappings/view-scim2-attributes.png)

## Add a SCIM 2.0 custom schema attribute
You can add new SCIM 2.0 custom schema attributes as follows:

1. On the WSO2 Identity Server Console, go to **User Attributes & Stores** >  **Attributes**.
2. Under **Manage Attribute Mappings**, click **SCIM 2.0**.
3. Click **New Attribute** and enter values for the following properties:

    ![Add OpenID Connect attributes](../../../../../assets/img/guides/organization/attributes/attribute-mappings/add-scim2-attribute-mapping.png)

    <table>
          <tbody>
            <tr>
                <td>**SCIM Attribute**</td>
                <td>The SCIM attribute name that will be shared with applications.</td>
             </tr>
             <tr>
                <td>**User attribute to map to**</td>
                <td>Select the default attribute that should be mapped to the new SCIM attribute.</td>
             </tr>
          </tbody>
       </table>

4. Click **Save**.

## Delete a SCIM 2.0 custom schema attribute
To delete the SCIM 2.0 custom schema attributes available in your organization:

1. On the WSO2 Identity Server Console, go to **User Attributes & Stores** > **Attributes**.
2. Under **Manage Attribute Mappings**, click **SCIM 2.0**.
3. Navigate to the **Custom Schema** tab and select the attribute to delete.
3. Click **Delete** and select the checkbox to confirm you action.
4. Click **Confirm**.

:::note

Only custom attributes can be deleted.

:::
