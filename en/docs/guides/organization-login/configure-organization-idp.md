# Configure organization IdP

Let's create an organization IdP for any given organization to be able to add SSO login and other features to their applications.

## Create the organization IdP

Follow the steps given below to register your organization's business apps in the root organziation.

1.  Sign in to the WSO2 Identity Server Management Console as a super admin user: `https://<SERVER_HOST>:9443/console`.

    !!! info
        The default credentials for a administrative user is as follows:

        -   Username: `admin`
        -   Password: `admin`

2.  Use the **Organization Switcher** to switch to the root organization.

3.  Go to **Develop > Identity Providers** and click **New Identity Provider** to create an IdP.

4.  Select the **Organization SSO** template, specify the organization details, and click **Finish**.

You are directed to the identity provider view where you can do the needed configuration to the IDP.

## What's next?

You can now enable organization login for the applications in your root organization. [Learn more]().