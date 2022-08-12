# Try organization login

Let's try organization login using a sample scenario.

## Scenario

Pickup is an ambulance service company that has many employees who use different credentials to sign in to different internal enterprise applications. While Robert is an administrator at Pickup and the MedLife Hospital is the root organization while following are the sub-organizations and the respected admins.

-   Greater Hospital - Tom
-   Wellness Hospital - Alice
-   Little Star Clinic - Jerry, Bob 

Robert wants to register a user account in each of the sub-organizations and provide an organization specific login option for the users to log in to the respected sub-organization IDP.

## Prerequisites

Create Organization SSO Login in the SaaS business as a federated authenticator in the MedLife Organization.

## Step 1: Create the organizations

1.  Create the MedLife Root Organization.
2.  Log in to the MedLife Organization.
    -   To log into the super organization of the console `https://<SERVER_HOST>:9443/console`.
    -   To log into another organization space of the console `https://<SERVER_HOST>:9443/o/<organization id>/console`.
3.  Create the following sub-organizations:

    -   Greater Hospital
    -   Wellness Hospital
    -   Little Star Clinic

## Step 2: Configure the business apps

1.  Configuring Pickup Manager application
2.  Create OIDC SaaS application in MedLife Organization.

3.  Replace the consumerKey and consumerSecret values with the OAuth client key and OAuth client secret values that were generated for the newly created service provider.
4.  In the created SaaS Application, under Sign-in Method add Organization SSO Login for authentication. Other than that add the following adaptive script for conditional authentication under organization idp.

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
## Step 3: Share the business app with sub orgs

For the Greater Hospital create a separate Asgardeo IdP for their user base. 

## Step 4: Onboard sub-organization IdPs

Create an application in Asgardeo with OAuth2.0/OpenID Connect protocol and get the client id and secret to create an IDP for Greater Hospital. Also, create the user Tom in the userbase.

Use above information to create the OIDC based idp.

In the fragmented SaaS Application in Greater Hospital, under Sign-in Method add created Asgardeo IdP for authentication.

For the Wellness Hospital create the user Alice in the user base.

For the Little Star Clinic create a separate Asgardeo IdP for their user base as in Greater Hospital. Repeat the Step 9 and Step 10 again for the Little Star Clinic. Create an application in Asgardeo with OAuth2.0/OpenID Connect protocol and get the client id and secret to create an IDP for Greater Hospital. Also, create the user Jerry in the userbase.

In the fragmented SaaS Application in Little Star Clinic, under Sign-in Method add created Asgardeo2 IdP for authentication as well as Username & Password basic authentication, because it has both Asgardeo and their own userbase.

This hospital also has their own userbase as well, therefore create the user Bob in the userbase as in Step 11.

## Try it out

1.  Login to the pickup-manager application: `http://localhost.com:8080/pickup-manager`
2.  Select **Sign in with Enterprise IdP** and enter the sub organization name. 

    !!! info
        Then the login option(s) configured for that sub organization will be displayed.

3.  First provide the organization as Wellness Hospital. 

    !!! info
        You’ll be redirected to basic authentication login page. 

4.  Provide the credentials for user Alice and login.

5.  Then try the Greater Hospital organization and login. 

    !!! info
        You’ll be redirected to the Asgardeo IdP based login page.

6.  Then try the Little Star Clinic organization and login.

