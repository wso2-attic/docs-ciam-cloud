# Organization Specific REST API Routing

## Organization URLs

As a part of the B2B Organization Management feature, incorporated the organization identifier as first-class support for the URLs by introducing a path param to denote the specific organization to which the request should be directed to.

URL format - `o/{organization id}/…`

Organization-specific routing capability is introduced. Here we are supporting both Basic Authentication and OAuth 2.0 flows.

## Basic Authentication

The `BasicAuthenticationHandler` has also been improved to handle authentication when the username has the organization domain(id) appended.

Run the cURL command given below to get the organization list.

``` java
curl GET 'https://localhost:9443/o/<org-id>/api/server/v1/organizations' \
--header 'accept: application/json' \
--header 'Authorization: Basic [Base64encode(Username>:<Password>)]'
```

The current behavior in BasicAuthenticationHandler is that if the username doesn't have the organization domain, the user is authenticated against the super organization.
It was decided to improve the authentication logic as given below.

<img src="../../../assets/img/references/organization-specific-rest-api-routing/improved_basicauthenticationhandler.png" alt="Improved BasicaAthenticationHandler" width="700">

-   If the username doesn't have the organization domain, the user is authenticated against the `/o/<org>`.
-   Else retrieve the organization domain from the username (break from the last @ in the username) and authenticate the user against that organization

Assume that mary is a user of orgA and she creates orgB as a child of orgA.

-   `/o/<orgA domain>/....` -> `mary@<orgA domain>` (authentication happens against orgA)
-   `/o/<orgA domain>/....` -> `mary` (authentication happens against orgA)
-   `/o/<orgB domain>/....` -> `mary@<orgA domain>` (authentication happens against orgA)
-   `/o/<orgB domain>/....` -> `mary` (authentication happens against orgB. hence will result in a failure)
-   `/o/<orgB domain>/....` -> `mary@<orgB domain>` (authentication happens against orgB. hence will result in a failure)

## OAuth 2.0 Basic Flow 

<img src="../../../assets/img/references/organization-specific-rest-api-routing/oauth2_basic_flow.png" alt="OAuth 2 Basic Flow" width="700">

Here we can have several [OAuth2 grant types](https://is.docs.wso2.com/en/latest/learn/oauth-2.0-with-wso2-playground/) like code grant, implicit grant etc. to get access token for Organization A or Organization B accordingly.
With these grant types, we can use `o/<path>` routing for authorization.

-   Access Token for Organization A - /o/<orgA domain>/token
-   This access token can be used only for the resources related to Organization A.
-   But if needed to access the resources of the Organization B, will have to get the access token for organization B as well (`/o/<orgB domain>/token`).

## Organization Switch Grant

<img src="../../../assets/img/references/organization-specific-rest-api-routing/organization_switch_grant.png" alt="Organization Switch Grant" width="700">

Run the cURL command given below for the organization switch grant.

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

For the solution for the above issue we faced during OAuth 2.0 flow, where we needs to access the resources of another organization. Therefore we have used a customized grant called, organzation_switch, where we can use that token for the authorization of another orgnaization resources.

## Organization Domain

The domain of an Organization is represented by an Organization Domain, sometimes called a User Email Domain.
