---
title: User Federation with Keycloak (OpenID)
layout: default
parent: Identity and Access Management (IAM)
grand_parent: Management & Governance
permalink: /docs/management-and-governance/iam/user-federation-with-keycloak-openid
---
<img width="450px" height="102px" src="https://console-static.huaweicloud.com/static/authui/20210202115135/public/custom/images/logo-en.svg">

# User Federation with Keycloak (OpenID)

V1.0 – October 2024

| **Version**       | **Author**                     | **Description**      |
| ----------------- | ------------------------------ | -------------------- |
| V1.0 – 2024-10-15 | Diogo Hatz d50037923           | Initial Version      |
| V1.0 – 2024-10-15 | Wisley da Silva Paulo 00830850 | Document Review      |

# Objective

This document aims to present the procedures required to implement identity federation configuration in Huawei Cloud (Service Provider) through an identity provider (IdP), such as RedHat SSO or Keycloak. In this example, the protocol used for identity federation will be OpenID, mapping users from the identity provider to virtual users in Huawei Cloud.

In the diagram below, you can see the authentication process flow in Huawei Cloud using an IdP.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image3.png)

# Keycloak

First, you need to configure the identity provider (IdP). To do this, access the IdP (Keycloak) configuration page and navigate to the “Clients” section. Click “Create” to create a new client.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image4.png)

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image5.png)

Select “Client Protocol” as “openid-connect” and enter “hws-oidc” in the “Client ID” field. Once done, click “Save” to create the client.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image6.png)

Navigate to the Huawei Cloud client you created and click “Edit” to edit the client settings.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image7.png)

Enable the “Implicit Flow Enabled” option, change the “Access Type” field to “confidential” and insert the following hyperlink in the “Valid Redirect URIs” field: <https://auth.huaweicloud.com/authui/oidc/post>. Once done, click “Save” to save the changes made.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image8.png)

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image9.png)

Navigate to the “Mappers” section, still in the Huawei Cloud client settings, and click “Create” to create a mapper for the username.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image10.png)

Select the “Mapper Type” as “User Property” and fill in the remaining fields as shown in the image below.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image11.png)

Navigate once again to the “Mappers” section, still in the Huawei Cloud client settings, and click “Create” to create a mapper for the group.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image10.png)

Select the “Mapper Type” as “Group Membership”, disable the “Full group path” option and fill in the remaining fields as shown in the image below.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image12.png)

To perform Huawei Cloud user federation, users must first exist. If there is no user created in Keycloak, create a user. Navigate to the “Realm Settings” section and click on “OpenID Endpoint Configuration” in the “Endpoints” subsection. 

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image13.png) 
![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image14.png) 

Note the following parameters, which will need to be configured on the service provider (Huawei Cloud) side: “authorization\_endpoint” and “jwks\_uri”. 

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image15.png)

In the web browser, navigate to the hyperlink for the
“jwks\_uri” parameter copied above and make a note of the key.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image16.png)

# IAM

Access the IAM service in the Huawei Cloud console and navigate to the
“Identity Providers” section. Click “Create Identity Provider” to create
an identity federation configuration.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image17.png)

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image18.png)

Select the OpenID-Connect protocol and the “SSO Type” as “Virtual User”.

Click the “OK” button to save the IdP creation settings.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image19.png)

Once done, select the “Modify” option next to the created identity provider and fill in the fields as shown in the figure below.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image20.png)

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image21.png)

1. > **<span class="underline">Identity Provider URL:</span>**
> Hyperlink relative to the realm in which the client was configured in
> keycloak. Example: ;

2. **<span class="underline">Client ID:</span>** Same parameter
configured in the “Client ID” field of Keycloak;

3. > **<span class="underline">Authorization Endpoint:</span>**
> Parameter “authorization\_endpoint” present in the Open-ID endpoint
> configuration file in Keycloak;

4. **<span class="underline">Response Mode:</span>** “form\_post”;

5. > **<span class="underline">Signing Key:</span>** Contents of the “jwks\_uri” parameter, present in the Open-ID endpoint
> configuration file in Keycloak.

**<span class="underline">Important:</span>** The Open-ID protocol necessarily requires an SSL certificate to be configured in the identity provider to enable communication via the HTTPS protocol. The SSL certificate can be a self-signed certificate. Finally, in the “Identity Conversion Rules” section, click “Create Rule” to create a rule for converting users and groups from the IdP to the corresponding users and groups in Huawei Cloud. You can use the following example conversion rule. 

**<span class="underline">Important:</span>** The conversion rule below maps **all** Keycloak users to IAM groups in Huawei Cloud that have the same names as the groups configured in Keycloak. For example: In Keycloak, the user “Test” belonging to the “admin” group will be mapped, in Huawei Cloud, to the virtual user “Test” in the “admin” group. It is not necessary for the “Test” user to be previously created in Huawei Cloud. However, it is mandatory for the “admin” group to be previously created in Huawei Cloud with the appropriate access control policies. 

```json
[
    {
        "remote": [
            {
                    "type": "username"
            },
            {
                    "type": "Group"
            }
        ],
        "local": [
            {
                    "user": {
                            "name": "{0}"
                    }
            },
            {
                    "group": {
                            "name": "{1}"
                    }
            }
        ]
    }
]
```

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image22.png)

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image23.png)

Once done, click “OK” to save the changes made to the IdP.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image24.png)

# Example

The following is an example of validating login to the Huawei Cloud console through identity federation.

Accessing the Huawei Cloud console and selecting the option to log in through a federated user.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image25.png)

Entering the account name and selecting the configured IdP from the dropdown.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image26.png)

Logging in to the configured identity provider.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image27.png)

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image28.png)

Authentication successful, redirecting to the Huawei Cloud console.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image29.png)

**<span class="underline">Important:</span>** You can also log in to the console through identity federation using the hyperlink generated in the Identity Provider configuration in the Huawei Cloud console.

![](/huaweicloud-knowledge-base/assets/images/management-and-governance/iam/user-federation-keycloak-openid/image30.png)

# References

- IAM Documentation: <https://support.huaweicloud.com/intl/en-us/usermanual-iam/iam_08_0002.html>

- Huawei Cloud Blog: <https://bbs.huaweicloud.com/blogs/401343>