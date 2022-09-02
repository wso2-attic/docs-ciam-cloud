# Try Organizational Login Flow

Let's try organization login using a sample scenario.

## Scenario

**Guardio** is an auto insurance service company that has many employees who use different credentials to sign in to many internal applications.  To manage logins to its many applications, Guardio uses the WSO2 Identity Server B2B Private CIAM Solution where Guardio is configured as a super organization. **Guardio-SaaS-App** is one such application.

<img src="../../../assets/img/guides/organization-login/try-it-out/scenario_diagram.png" alt="Scenario Diagram" width="700">

The administrators of the organizations are as follows:

- Guardio (super organization): `Larry`
- **Best Auto Mart**: `Alex`
- **Car Traders**: `Sam`

Larry wants to perform the following tasks:

- Register a user in each sub-organization
- Provide a login option for the users to log in to the respective sub-organization IdP. 

## Step 1: Create the organizations

To create the sub-organizations:
1. Sign in to the super organization (`https://{SERVER_HOST}:{PORT}/console`).

2. On the console, [create sub-organizations](../b2b-org-management/manage-organizations.md/#create-organizations) with the following names:

    - **Best Auto Mart**
    - **Car Traders**

    <img src="../../../assets/img/guides/organization-login/try-it-out/created_sub_organizations.png" alt="Created suborganizations" width="700" style="border:1px solid grey">

!!! note "Create the users"
    Create new users on the sub-organizations with the required permissions of an administrator.
    
    - To create a user for **Best Auto Mart**:
        1. Use the **Organization Switcher** to change the organization to **Best Auto Mart**.
        2. Create a user named `Alex` on the **Best Auto Mart** organization.
        3. Create a **Role** with the [required permissions](../../b2b-org-management/b2b-org-permissions) to create an Identity Provider. 
        4. Assign `Alex` to this newly created **Role**.
    - To create a user for **Car Traders**:
        1. Use the **Organization Switcher** to change the organization to **Car Traders**.
        2. Create a user named `Sam` on the **Car Traders** organization.
        3. Create a **Role** with the [required permissions](../../b2b-org-management/b2b-org-permissions) for an administrator. 
        4. Assign `Sam` to this newly created **Role**.

## Step 2: Configure the business apps

To configure the business applications:

1. On the CIAM Private Cloud console, go to **Develop > Applications**.
2. Click **+ New Application** and select **Standard-Based Application**.
3. Enter `Guardio-SaaS-app` as the application name and select `OAuth2.0 / OpenID Connect` as the **Protocol**.
4. Select **Management Application**, to allow the application to use Management APIs.
5. Click **Register** to create the new application.

    !!! note
        Note the OAuth client key and OAuth client secret that is generated, you will need them to set up the sample application.

    <img src="../../../assets/img/guides/organization-login/try-it-out/app_oidc_config.png" alt="App OIDC Configurations" width="700" style="border:1px solid grey">

6. On the Protocol tab, select [`Organization Switch`](../../../references/org-domains-urls) and `Code` on the **Allowed Grant types**, and enter the following details:
    - Authorized redirect URLs: `http://localhost:3000/api/auth/callback/wso2is`
    - Allowed origin: `http://localhost:3000`


7. Click **Update** to save the configurations.

8.  Go to **User Attributes** and click on **+ Add User Attributes**.

9.  Select `Email`, `First Name`, `Last Name`, and `Username` from the list of attributes.

    <img src="../../../assets/img/guides/organization-login/try-it-out/app_add_user_attributes.png" alt="App User Attributes Configurations" width="700" style="border:1px solid grey">

10.  Click **Save** to add the user attributes and click **Update** to save all the configurations.

    <img src="../../../assets/img/guides/organization-login/try-it-out/app_after_adding_user_attributes.png" alt="App after adding User Attributes Configurations" width="700" style="border:1px solid grey">

## Step 3: Share the business app

Share the `Guardio-SaaS-app` business application with the other sub-organizations using the [Share Application](../organization-login/share-the-business-app/#share-the-application) option.

<img src="../../../assets/img/guides/organization-login/try-it-out/share_app_with_sub_orgs.png" alt="Share App with suborganizations" width="600" style="border:1px solid grey">

## Step 4: Configure the Sign-in method

After you share the application with the sub-organizations, an **Organization SSO** IdP named `Organization Login` will be automatically created and assigned as a sign-in method for the application.

To check if the IdP is assigned to the application:

1. On the CIAM Private Cloud console, go to **Develop > Applications** and select `Guardio-SaaS-App`.
2. On the **Sign-in Method** tab, check if the generated **Organization Login** IdP has been assigned.
    
    <img src="../../../assets/img/guides/organization-login/try-it-out/organization-login-idp.png" alt="Share App with suborganizations" style="border:1px solid grey">

By default the **Username & Password** authentication step is added to the Sign-in flow. You can remove it from the sign-in flow of the application. By doing so, you will be directed to the created organization IdP for authentication.


!!! tip "Add additional authentication steps"
    
    For sub-organizational logins, it is compulsory to use the **Organization SSO** IdP, as the user should select the organization that they wish to log in to.

    In cases where the application is configured with two or more first-step authentication methods, the application must prompt the Organization SSO IdP authenticator for sub-organization users.

    To enable this add the following script for conditional authentication and update the `<ORG IDP NAME>`.
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

## Step 5: Onboard sub-organization IdPs

- On the [Asgardeo console](https://asgardeo.io/signup):
    
    1. Create an [OAuth 2.0 / OpenID Connect standard-based app](https://wso2.com/asgardeo/docs/guides/applications/register-standard-based-app/).
    
    2. Obtain the `client id` and `client secret`. This is needed to create an IdP on the **Best Auto Mart** organization.

    !!! info
        Use the details on the **Info** tab of the application, to create an OIDC-based IdP on the Private CIAM Cloud.
        
        <img src="../../../assets/img/guides/organization-login/try-it-out/asgardeo_app_info.png" alt="Asgardeo App Info" width="700" style="border:0px solid grey">

- On Private CIAM Cloud Console:

    1. Log in to the console as `Alex`.

        Use `https://localhost:9443/o/<organization-id>/console` as the Organization URL template to log in to the sub-organization.

    2. Create an **OIDC standard-based IdP** named `Asgardeo`, for the users of the **Best Auto Mart** organization.
        
        !!! info
            Use the details from the **Info** tab of the application made on Asgardeo, to fill the required fields when creating the IdP.

    3. Go to the **Develop > Applications** and select `Guardio-SaaS-app` which was shared in Step 3.

    4. On the **Sign-in Method** tab, select the created `Asgardeo` IdP as the first authentication method.
  
        <img src="../../../assets/img/guides/organization-login/try-it-out/asgardeo_idp_in_fragment_app.png" alt="Asgardeo IdP in Fragment App" width="700" style="border:1px solid grey">

    5. Click **Update** to save the configurations.

## Step 6: Deploy the sample app

To set up the sample application:

1. Download the [sample application](https://github.com/wso2/samples-is/tree/master/b2b-sample), and extract the content of the zip file.

2. Open the `config.json` file found in the `<SAMPLE_APP_HOME>/guardio-insurance-sample-application-main` directory and update the following properties:

    | Property  | Description   |
    |-----------|---------------|
    | WSO2IS_HOST   | The URL of the Identity Server.    |
    | WSO2IS_TENANT_NAME   | ID of the organization where the created application resides. <br> Default value for this property is `carbon.super`.   |
    | WSO2IS_CLIENT_ID  | The client ID obtained when creating an application on the Identity Server Console.    |
    | WSO2IS_CLIENT_SECRET  | The client secret obtained when creating an application on the Identity Server Console.   |
    | SAMPLE_ORGS   | The details of the organization. <br> `id`: ID of the sub-organizations using this shared application. |

    ``` json
    "WSO2IS_HOST": <Identity Server URL>,
    "WSO2IS_TENANT_NAME": carbon.super,
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

    !!! info
        If the created application resides in a different organization, replace the `WSO2IS_TENANT_NAME` value with the respective organization ID.

## Step 7: Add CORS configurations

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
