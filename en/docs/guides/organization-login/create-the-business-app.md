# Create business applications

Depending on how your Organization implementation is designed, you have different options when creating Application definitions within your Organization. Whichever option you choose, the Organization behavior is defined at the application level.

## Prerequisites

First, configure the [enterpise SSO IdP]() for your root organization.

## Register the business app

Follow the steps given below to register your organization's business apps in the root organziation.

!!! info
    This application will later be shared among sub organizations, which will allow users of the sub organizations to log in.

1.  Sign in to the WSO2 Identity Server Management Console as a super admin user: `https://<SERVER_HOST>:9443/console`.

    !!! info
        The default credentials for a administrative user is as follows:

        -   Username: `admin`
        -   Password: `admin`

2.  Use the **Organization Switcher** to switch to the root organization.

3.  Go to **Develop > Applications** and click **New Application** to create an application.

    !!! info
        You can use any of the available templates to register a new application.

After registration, you are be directed to the **Application**.

## Configure the login flow

Once you have registered the business application in your root organization, you need to define the login flow as follows:

1.  On the Management Console, go to the application you registered in the previous step.
2.  Go to the **Sign-in Method** tab and add the following IdPs for the first step of the sign-in flow:
    
    - Username & Password (basic authentication)
    - Organization SSO IdP
    
3.  Go to the **Conditional Authentication** section and add the following script:

    !!! info
        -   This conditional authentication script is used to identify the IdP that should be used for user authentication. That is, the user is prompted to specify the organization, based on which, the user is directed to that specific organization's IdP.
        -   Be sure to replace the `“<<ORGANIZATION_LOGIN_IDP_NAME>>”` placeholder in the script.

    ``` js
    var onLoginRequest = function(context) {
    executeStep(1,
        {
            authenticationOptions: [{
                idp: (context.request.params.org && !context.steps[1].idp) ? "<<ORGANIZATION_LOGIN_IDP_NAME>>" : context.steps[1].idp
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
                if (context.steps[1].idp === "<<ORGANIZATION_LOGIN_IDP_NAME>>") {
                    return;
                }
            }
        });
    };
    ```

## What's next?

You can now share this application with the sub organizations in your organization structure. [Learn more]().

