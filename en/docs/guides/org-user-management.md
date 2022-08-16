# User management

You can create users using the WSO2 Identity Server Console or the Management API.

## Prerequisites

-   You need to have the required permissions to create and manage users in an organization.
-   Sign in to the relevant organization from the Management Console:
    
    <table>
        <tr>
            <th>Root organization</th>
            <td><code>https://<SERVER_HOST>:9443/console</code></td>
        </tr>
        <tr>
            <th>suborganization</th>
            <td><code>https://<SERVER_HOST>:9443/o/<organization id>/console</code></td>
        </tr>
    </table>

## Add new users

Follow the steps given below to add new users to an organization.

1.  On the Management Console, use the **Organization Switcher** to select the relevant organization.

2.  Go to **Manage > Users** and click **New User**.

    <img src="../../../assets/img/guides/user-management/add_new_user.png" alt="Add New User" width="700" style="border:1px solid grey">

3.  Enter the user’s basic information and click **Next**.

    <img src="../../../assets/img/guides/user-management/new_user_details.png" alt="New User Details" width="400" style="border:1px solid grey">

4.  Select the user groups that should be assigned to the user.

    <img src="../../../assets/img/guides/user-management/new_user_usergroup.png" alt="New User - User Group" width="400" style="border:1px solid grey">

5.  Select the user roles that should be assigned to the user.

    <img src="../../../assets/img/guides/user-management/new_user_userrole.png" alt="New User - User Role" width="400" style="border:1px solid grey">

6.  Review the details and click **Finish** to finalize user creation.

    <img src="../../../assets/img/guides/user-management/created_new_user.png" alt="Created New User" width="400" style="border:1px solid grey">
