# Quickstart with WSO2 Private CIAM Cloud

Let's get started with customer identity and access management for your B2B organiations using the WSO2 private CIAM cloud.

## Step 1: Create your account

Follow the instructions given below to set up your WSO2 Private CIAM Cloud instance. 

1.  ...
2.  ...
3.  ...

## Step 2: Set up your organizations

Once your private CIAM cloud instance is set up, you can first sign in to the super tenant (root organization) on the Management Console using administrator credentials (`admin:admin`).

Use the following URL to access the Management Console for the super tenant:

``` bash
https://{SERVER_HOST}:9443/console
```

As the administrator of the super tenant organization, you can then start defining the hierarchy of your B2B organization.

See the instructions on [managing organizations](../../guides/b2b-org-management/manage-organizations).

## Step 3: Add organization admins

Once your organizations are set up, you can onboard users to each of the organizations and **delegate administration** capabilities to those users. This allows the organization admins to manage their own organization, its child organizations, and its users.

See the instructions on [managing users in organizations](../../guides/org-user-management).

## Step 4: Access organizations

Users onboarded to each of the organizations can access the Management Console for the specific organization(s) by using the relevant URL:

<table>
    <tr>
        <th>Super tenant organization</th>
        <td><code>https://{SERVER_HOST}:9443/console</code></td>
    </tr>
    <tr>
        <th>Sub organization</th>
        <td><code>https://{SERVER_HOST}:9443/o/{organization id}/console</code></td>
    </tr>
</table>

## What's next?

See the [guides](../../guides/guides-overview) for detailed instructions on how to manage organizations and to enable login from each organization to applications of your business.