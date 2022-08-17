# Configure organization IdP

Let's create an organization IdP for any given organization to be able to add SSO login and other features to their applications.

## Create the organization IdP

Follow the steps given below to register your organization's business apps in the root organziation.

1.  Sign in to the WSO2 Identity Server Management Console as a super admin user.

2.  Use the **Organization Switcher** to switch to the root organization.

3.  Go to **Develop > Identity Providers** and click **New Identity Provider** to create an IdP.

    <img src="../../../assets/img/guides/organization-login/configure-the-organization-idp/create_new_idp.png" alt="Create New IdP" width="700" style="border:1px solid grey">

4.  Select the **Organization SSO** template.

    <img src="../../../assets/img/guides/organization-login/configure-the-organization-idp/organization_sso.png" alt="Organization SSO" width="700" style="border:1px solid grey">

5.  Specify the organization details, and click **Finish**.

    <img src="../../../assets/img/guides/organization-login/configure-the-organization-idp/organization_sso_details.png" alt="Organization SSO Details" width="400" style="border:1px solid grey">

You are directed to the identity provider view where you can do the needed configuration to the IDP.

## What's next?

You can now enable organization login for the applications in your root organization. [Learn more](../create-the-business-app#configure-the-login-flow).