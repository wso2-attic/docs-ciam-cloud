# Quickstart with WSO2 Private CIAM Cloud

Let's get started with customer identity and access management for your B2B organizations using the WSO2 Private CIAM Cloud.

## Step 1: Get started!

WSO2 CIAM Cloud is a fully managed private cloud deployment. To get started, go to the [WSO2 CIAM Cloud website](https://wso2.com/ciam-suite/private-ciam-cloud/b2b-ciam/) and follow the instructions.

Once your account is created, you will receive an email with the following details to access the Management Console of your private CIAM Cloud instance:

-   URL of the Management Console
-   Credentials that should be used to sign in

## Step 2: Set up your organization

Once your CIAM Cloud instance is set up, you can access the Management Console and sign in to your root organization using the details you received during sign-up.

As the first administrator of your root organization, you can then start defining the hierarchy of your B2B organizations.

See the instructions on [managing organizations](../../guides/b2b-org-management/manage-organizations).

## Step 3: Add organization admins

Once your organizations are set up, you can onboard users to each of the organizations and **delegate administration** capabilities to those users. This allows other organization admins to manage their own organization, its child organizations, and its users.

See the instructions on [managing users in organizations](../../guides/org-user-management).

## Step 4: Share organization details

Once the organization admins are defined, you (as the super administrator) need to share the access URL of the suborganizations with the relevant administrators in each suborganization.

You can get an organization's access URL by switching to the organization on the Management Console. The format of a suborganization URL is as follows:

``` bash
https://{SERVER_HOST}:{PORT}/o/{ORGANIZATION_ID}/console
```

Note that the `ORGANIZATION_ID` is generated at the time of creating the organization.

## What's next?

See the [guides](../../guides/guides-overview) for detailed instructions on how to manage organizations and to enable login from each organization to applications of your business.