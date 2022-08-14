# Manage user groups

You can create user groups in any of the organizations to which you have access.

## Prerequisites

-   You need to have the required permissions to create and manage user groups.
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

## Create user groups

Follow the instructions below to create a user group:

1.  On the Management Console, use the **Organization Switcher** to select the relevant organization.

2.  Go to **Manage > Groups** and click **New Group**.

    <img src="../../../assets/img/guides/org-management/manage-user-groups/create_user_group.png" alt="Create User Group" width="700" style="border:1px solid grey">

3.  Enter the group name and select the users that should be assigned to the group. 

    <img src="../../../assets/img/guides/org-management/manage-user-groups/user_group_details.png" alt="User Group Details" width="400" style="border:1px solid grey">

4.  Click **Next** to assign roles.

5.  Link the required user roles to the user group and click **Next**.

    !!! info
        The user roles you assign will determine the permissions granted to the users in the group.

    <img src="../../../assets/img/guides/org-management/manage-user-groups/user_group_roles.png" alt="User Group Roles" width="400" style="border:1px solid grey">

6. Review the details and click **Finish** to finalize the user group.

    <img src="../../../assets/img/guides/org-management/manage-user-groups/created_user_group.png" alt="Created User Group" width="400" style="border:1px solid grey">

