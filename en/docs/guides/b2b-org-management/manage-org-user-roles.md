# Manage User Roles

You can create roles using the WSO2 Identity Server Console or the Management API. The roles can be used with the API Authorization Core feature set.

## Prerequisites

-   You need to have the required permissions to create and manage new organizations.
-   Sign in to the relevant organization from the Management Console.

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

## Edit a user role

Follow the instructions given below to edit a user role.

1. On the Management Console, use the **Organization Switcher** to select the relevant organization.
2. Go to **Manage > Roles** to view the list of roles.
3. Select the role you want to edit and click the pencil icon to open the role profile.

    <img src="../../../assets/img/guides/org-management/manage-user-roles/edit_role.png" alt="Edit a role" width="700" style="border:1px solid grey">

4. Change the basic info, permissions, groups and users of the role.

    <img src="../../../assets/img/guides/org-management/manage-user-roles/edit_role_details.png" alt="Edit role details" width="700" style="border:1px solid grey">

## Delete a role

Follow the instructions given below to delete a role.

1. On the Management Console, use the **Organization Switcher** to select the relevant organization.
2. Go to **Manage > Roles** to view the list of roles.
3. Select the role you want to edit and click the pencil icon to open the role profile.
4. Go to the danger zone and click **Delete role**.
5. In the dialog box that opens, confirm if you want to delete the role.

    <img src="../../../assets/img/guides/org-management/manage-user-roles/delete_role.png" alt="Delete a role" width="400" style="border:1px solid grey">
