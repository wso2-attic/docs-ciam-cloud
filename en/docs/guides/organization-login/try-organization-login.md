# Try Organizational Login Flow

Let's try organization login using a sample scenario.

## Scenario

**Guardio** is an auto insurance service company that has many employees who use different credentials to sign in to different internal organizational applications. **Guardio-SaaS-App** is one such application. Here, Guardio Insurance is using the WSO2 Identity Server B2B Private CIAM Solution, therefore it’s configured as the super organization.

<img src="../../../assets/img/guides/organization-login/try-it-out/scenario_diagram.png" alt="Scenario Diagram" width="700">

The administrators of the organizations are as follows:

- Super organization: `Larry`
- **Best Auto Mart**: `Alex`
- **Car Traders**: `Sam`

Larry wants to register a user in each sub-organization and provide an organization-specific login option for the users to log in to the respective sub-organization IDP.

## Prerequisites

You need to create [an IdP with the organization SSO template](../configure-organization-idp) in the root business (the super organization) as a federated authenticator.

## Step 1: Create the organizations

1. Sign in to the super organization (`https://{SERVER_HOST}:{PORT}/console`).

2. On the console, [create sub-organizations](../b2b-org-management/manage-organizations.md/#create-organizations) with the following names:

    - **Best Auto Mart**
    - **Car Traders**

    <img src="../../../assets/img/guides/organization-login/try-it-out/created_sub_organizations.png" alt="Created suborganizations" width="700" style="border:1px solid grey">

## Step 2: Configure the business apps

1. On the CIAM Private Cloud console, go to **Develop > Applications**.
2. Click **+ New Application** and select **Standard-Based Application**.
3. Enter `Guardio-SaaS-app` as the application name and select `OAuth2 / OpenID Connect` as the **Protocol**.

    !!! note
        Be sure to select **Management Application** when creating the application.

        <img src="../../../assets/img/guides/organization-login/create-business-applications/management_application.png" alt="Management Application" width="300" style="border:1px solid grey">

4. Click **Register** to create the new application.

    !!! note
        Note the OAuth client key and OAuth client secret that is generated, you will need them to set up the sample application.

    <img src="../../../assets/img/guides/organization-login/try-it-out/app_oidc_config.png" alt="App OIDC Configurations" width="700" style="border:1px solid grey">

5. On the Protocol tab, select [`Organization Switch`](../../../references/org-domains-urls) and `Code` on the **Allowed Grant types**, and enter the following details:
    - Authorized redirect URLs: `http://localhost:3000/api/auth/callback/wso2is`
    - Allowed origin: `http://localhost:3000`


6. Click **Update** to save the configurations.

7. On the **Sign-in Method** tab and add **Organization SSO Login** as the method of authentication.

    !!! note
        Remove the **username & password** authentication step from the sign-in flow of the application. By doing so, you will be directed to the selected organization IdP for authentication.

    <img src="../../../assets/img/guides/organization-login/try-it-out/saas_app_sign_in_with_sample_app.png" alt="Saas App Sign-in with Sample App" width="700" style="border:1px solid grey">

    !!! tip "Add authentication method as a script"
        If you are using other authentication methods as well, add the following script for conditional authentication:

            ``` js
            var onLoginRequest = function(context) {
            executeStep(1,
                {
                    authenticationOptions: [{
                        idp: (context.request.params.org && !context.steps[1].idp) ? "<ORG IDP NAME>" : context.steps[1].idp
                    }],
                    authenticatorParams : {
                        common : {
                            'skipIdentifierPreProcess' : "true"
                        }
                    }
                },
                {
                    onSuccess: function (context) {
                        Log.info("User successfully completed initial with IDP : " + context.steps[1].idp);
                        if (context.steps[1].idp === "<ORG IDP NAME>") {
                            return;
                        }
                    }
                });
            };
            ```

6. Click **Update** to save the configurations.

## Step 3: Share the business app

Share the `Guardio-SaaS-app` business application with the other sub-organizations using the [Share Application](../organization-login/share-the-business-app/#share-the-application) option.

<img src="../../../assets/img/guides/organization-login/try-it-out/share_app_with_sub_orgs.png" alt="Share App with suborganizations" width="400">

!!! tip
    If you have not created an **Organization SSO** IdP, before sharing the application; an **Organization SSO** IdP will be created automatically after you successfully share the application with the sub-organizations.

## Step 4: Onboard sub-organization IdPs

- On the [Asgardeo console](https://asgardeo.io/signup), create an [OAuth 2.0 / OpenID Connect standard-based app](https://wso2.com/asgardeo/docs/guides/applications/register-standard-based-app/). Obtain the `client id` and `client secret`, it will be used to create an IdP on the **Best Auto Mart** organization.

    !!! info
        Use the details on the **Info** tab of the application, to create an OIDC-based IdP on the Private CIAM Cloud.
        <img src="../../../assets/img/guides/organization-login/try-it-out/asgardeo_app_info.png" alt="Asgardeo App Info" width="700" style="border:1px solid grey">


- As the administrator, on Private CIAM Cloud Console:

    1. Use the **Organization Switcher** to change the organization to **Best Auto Mart**.

    2. Create a user named `Alex` on the **Best Auto Mart** organization.

    3. Create a **Role** with the [required permissions](../../b2b-org-management/b2b-org-permissions) to create an Identity Provider. Assign `Alex` to this newly created **Role**.

    Use `https://localhost:9443/o/<organization-id>/console`, the Organization URL template to log in to **Best Auto Mart** organization.


- As Alex, on Private CIAM Cloud Console:

    1. Create an **OIDC standard-based IdP** named `Asgardeo`, for the users of the **Best Auto Mart** organization.
        
        !!! info
            Use the details from the **Info** tab of the application made on Asgardeo, to fill the required fields when creating the IdP.

    2. Go to the **Develop > Applications** and select `Guardio-SaaS-app` which was shared in Step 3.

    3. On the **Sign-in Method** tab, select `Asgardeo` IdP as the first authentication method.

In the fragmented SaaS Application of the Best Auto Mart organization, add the created Asgardeo IdP for authentication in the sign-in flow.
  
<img src="../../../assets/img/guides/organization-login/try-it-out/asgardeo_idp_in_fragment_app.png" alt="Asgardeo IdP in Fragment App" width="700" style="border:1px solid grey">

For the Car Traders organization, [create the user](../../org-user-management) Sam with admin [permissions](../../b2b-org-management/b2b-org-permissions) in the user base.

## Step 5: Deploy the sample web application

To set up the sample application:

1. Download the [sample application](https://github.com/Achintha444/guardio-insurance-sample-application/archive/main.zip), and extract the content of the zip file.

2. Open the `config.json` file found in the `<SAMPLE_APP_HOME>/guardio-insurance-sample-application-main` directory and update the following properties:

    | Property  | Description   |
    |-----------|---------------|
    | WSO2IS_HOST   | The URL of the Identity Server.    |
    | WSO2IS_CLIENT_ID  | The client ID obtained when creating an application on the Identity Server Console.    |
    | WSO2IS_CLIENT_SECRET  | The client ID obtained when creating an application on the Identity Server Console.   |
    | SAMPLE_ORGS   | The details of the organization. `id`: ID of the sub-organizations using this application. |

    ``` json
    "WSO2IS_HOST": <Identity Server URL>,
    "WSO2IS_CLIENT_ID": <APPLICATION CLIENT ID>, 
    "WSO2IS_CLIENT_SECRET": <APPLICATION CLIENT SECRET>,
    "SAMPLE_ORGS" : [
        {
            "id" : <Best Auto Mart Organization ID>,
            ...
        },
        {
            "id" : <Car Traders Organization ID>,
            ...
        },
    ]
    ```

## Step 6: Add CORS configurations

Add the following configurations to the `deployment.toml` file found in `<IS_HOME>/repository/conf/` to allow HTTP POST requests:

    ``` toml
    allow_generic_http_requests = true
    allow_any_origin = false
    allowed_origins = [
    "http://localhost:3000"
    ]
    allow_subdomains = false
    supported_methods = [
        "GET",
        "POST",
        "HEAD",
        "OPTIONS",
        "PUT",
        "DELETE"    
    ]
    support_any_header = true
    supported_headers = []
    exposed_headers = []
    supports_credentials = true
    max_age = 3600
    tag_requests = false
    ```

Save the file and restart the Identity Server.

## Try it out

To try out this application:

1. Open a terminal, navigate to `<SAMPLE_APP_HOME>/guardio-insurance-sample-application-main` folder and run the following commands to start the application:
    
    !!! info
        To complete this step, it is required to have a node installed in your machine.
        
    ``` node
    npm install
    npm run dev
    ```

2. Enter `http://localhost:3000` on your browser to access the application.

3. Click **Sign In** to proceed with the application.

4. Select your organization from the list and click **Next**. In this example, we will select `Car Traders` as the organization.

    <img src="../../../assets/img/guides/organization-login/try-it-out/sample_app_org.png" alt="Sample App Orgs" width="700" style="border:0px solid grey">

5. Enter the user credentials and click **Continue** to log in to the application.
    You will be successfully logged in to the sample application.

6. Logout of the application, select `Best Auto Mart` organization and try to log in. You will be redirected to the Asgardeo login page.
