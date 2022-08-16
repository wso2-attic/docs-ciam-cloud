# Organization-Specific REST API Routing

## Organization URLs

The Management Console URL in the WSO2 Private CIAM Cloud contains a path parameter to identify the organization. This denotes the specific organization to which requests should be routed.

URL format - `o/{organization id}/…`

Organization-specific routing in WSO2 Private CIAM Cloud supports both basic authentication and OAuth 2.0 flows as explained below.

## Basic Authentication

The `BasicAuthenticationHandler` has been improved to handle authentication when the username has the organization domain(id) appended.

For example, consider the following request to get the organization list:

``` java
curl GET 'https://localhost:9443/o/<org-id>/api/server/v1/organizations' \
--header 'accept: application/json' \
--header 'Authorization: Basic [Base64encode(Username>:<Password>)]'
```

If the username in the `BasicAuthenticationHandler` doesn't have the organization domain, the user is authenticated against the super organization.
It was decided to improve the authentication logic as given below.

<img src="../../../assets/img/references/organization-specific-rest-api-routing/improved_basicauthenticationhandler.png" alt="Improved BasicaAthenticationHandler" width="700">

If the username doesn't have the organization domain, the user is authenticated against `/o/<org>`. Otherwise, you can retrieve the organization domain from the username (note the break with the last `@` in the username) and authenticate the user against that organization.

For example, assume that Mary is a user of `orgA` and she creates `orgB` as a child of `orgA`.

-   `/o/<orgA domain>/....` -> `mary@<orgA domain>` (authentication happens against orgA)
-   `/o/<orgA domain>/....` -> `mary` (authentication happens against orgA)
-   `/o/<orgB domain>/....` -> `mary@<orgA domain>` (authentication happens against orgA)
-   `/o/<orgB domain>/....` -> `mary` (authentication happens against orgB. hence will result in a failure)
-   `/o/<orgB domain>/....` -> `mary@<orgB domain>` (authentication happens against orgB. hence will result in a failure)

## OAuth 2.0 Basic Flow 

<img src="../../../assets/img/references/organization-specific-rest-api-routing/oauth2_basic_flow.png" alt="OAuth 2 Basic Flow" width="700">

You can use several [OAuth2 grant types](https://is.docs.wso2.com/en/latest/learn/oauth-2.0-with-wso2-playground/) to get access tokens for each organization.
With these grant types, we can use `o/<path>` routing for authorization. For example, consider two organizations orgA and orgB.

-   Access Token for OrgA: `/o/<orgA domain>/token`
-   This access token can be used only for the resources related to OrgA.
-   To access the resources of OrgB, you need to get the access token for OrgB as well: `/o/{orgB domain}/token`.

## Organization Switch Grant

According to the OAuth 2.0 flow, to get an access token for a particular organization, you need to authenticate against it by verifying the client and providing user consent. To get an access token for another organization, you need to follow the same process. With this method, WSO2 Private CIAM Cloud is using a customized grant called `organzation_switch`, where the token is used for authorizing another organization's resources without verifying the client or providing user consent for that organization.

<img src="../../../assets/img/references/organization-specific-rest-api-routing/organization_switch_grant.png" alt="Organization Switch Grant" width="700">

For example, use the following cURL command to try out the organization switch grant:

``` java
curl POST 'https://SERVERHOST:9443/oauth2/token' \
--header 'Authorization: Basic [Base64encode(Client-ID>:<ClientSecret>)]' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=organization_switch' \
--data-urlencode 'token=<token>' \
--data-urlencode 'scope=<scopes>' \
--data-urlencode 'switching_organization=<organization-id>'
```

!!! Example
    ```java
    curl POST 'https://localhost:9443/oauth2/token' \
    --header 'Authorization: Basic e3tjbGllbnRfaWR9fTp7e2NsaWVudF9zZWNyZXR9fQ==' \
    --header 'Content-Type: application/x-www-form-urlencoded' \
    --data-urlencode 'grant_type=organization_switch' \
    --data-urlencode 'token=88d53666-be5a-3ec1-a8d5-c0ef9f3614c7' \
    --data-urlencode 'scope=openid+SYSTEM' \
    --data-urlencode 'switching_organization=3bbea6c7-b428-4d95-bf48-8ff2d421c0c6'
    ```

## Organization Domain

The domain of an organization is represented by an organization domain, sometimes called a user email domain.
