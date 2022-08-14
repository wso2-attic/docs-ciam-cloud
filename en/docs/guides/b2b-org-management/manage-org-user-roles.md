# Create user roles

You can create roles using the WSO2 Identity Server Console or the Management API. The roles can be used with the API Authorization Core feature set.

## Prerequisites

-   You need to have the required permissions to create and manage new organizations.
-   Sign in to the relevant organization from the Management Console:
    
    <table>
        <tr>
            <th>Root organization</th>
            <td><code>https://<SERVER_HOST>:9443/console</code></td>
        </tr>
        <tr>
            <th>Sub organization</th>
            <td><code>https://<SERVER_HOST>:9443/o/<organization id>/console</code></td>
        </tr>
    </table>

## Create a user role

Follow the instructions below to create a user role:

1.  On the Management Console, use the **Organization Switcher** to select the relevant organization.

2.  Go to **Manage > Roles** and click **Add Organization Role**.

    !!! info "Organization creator role"
        You will see the list of user roles. The `org-creator` user role is an automatically created user role, which is there to ensure that the organization-creator has access to manage the initial setup of the organization. This role cannot be deleted and edited.

    <img src="../../../assets/img/guides/org-management/manage-user-roles/add_organization_role.png" alt="Add Organization Role" width="700" style="border:1px solid grey">

3.  Provide the details of the user role and click **Next**.

    <img src="../../../assets/img/guides/org-management/manage-user-roles/user_role_details.png" alt="User Role Details" width="400" style="border:1px solid grey">

4.  Select the necessary permissions that should be linked to the user role and click **Next**.  

    !!! info
        See [organization-level permissions](../../b2b-org-management/b2b-org-permissions) for details.

    <img src="../../../assets/img/guides/org-management/manage-user-roles/user_role_permissions.png" alt="User Role Permissions" width="400" style="border:1px solid grey">

5.  Select the user groups or individual users that you want to add this role to and click **Next**.

    <img src="../../../assets/img/guides/org-management/manage-user-roles/user_role_groups.png" alt="User Role Groups" width="400" style="border:1px solid grey">

6.  Review the details and click **Finish** to finalize user role creation.

    <img src="../../../assets/img/guides/org-management/manage-user-roles/created_user_role.png" alt="Created User Role" width="400" style="border:1px solid grey">

