# Concepts

Given below are concepts you will use when you work with WSO2 Private CIAM Cloud for your B2B organizational requirements.

## Organizations

An organization represents a grouping of users and other organizations in the WSO2 Private CIAM Cloud. You can maintain multiple organizations within a single organization that depicts a hierarchical or flat organizational structure. 

The WSO2 Private CIAM Cloud can manage a large number of roles and user groups within an organizational boundary. Because organizations are isolated from one another, businesses can maintain their own enterprise structures and identity providers.

Listed below are the types of organizations you work with.

<!--

The following attributes are defined for organization entity attributes:

<table>
    <tr>
        <th>Name</th>
        <td>
            The name of the organization.
        </td>
    </tr>
    <tr>
        <th>Description</th>
        <td>
            Description of the organization.
        </td>
    </tr>
    <tr>
        <th>Type</th>
        <td>
            <p>The type of organization.</p>
            <p><b>Default</b>: TENANT</p>
        </td>
    </tr>
    <tr>
        <th>parentId</th>
        <td>
            <p>The identifier of the organization where suborganizations are created.</p>
            <p><b>Default</b>: Super</p>
        </td>
    </tr>
    <tr>
        <th>Attributes</th>
        <td>
            The attributes of the organization. For example: sector, corporation, industry, etc. 
        </td>
    </tr>
</table>
-->

<table>
    <tr>
        <th>Super organization</th>
        <td>
            The super organization is the default organization of a WSO2 CIAM Cloud instance. All other organizations will be subordinate in structure to the super organization.
        </td>
    </tr>
    <tr>
        <th>Suborganization</th>
        <td>
            A suborganization is an organization that is subordinate to a parent organization. For example, the super organization may have suborganizations at multiple levels in the B2B organization structure. 
        </td>
    </tr>
</table>

Learn more about [managing organizations](../../guides/b2b-org-management/manage-organizations).

<!--

### Root organization
In an organization structure of a B2B business, there may be multiple root organizations. For example, the root of a structure is the organization that holds the business applications that are shared with its child organizations. A root organization may be the super organization or any of the suborganizations that have child organizations.
-->

## Business applications

B2B applications are hosted by the super organization and shared with its suborganizations. Learn more about [managing business applications](../../guides/organization-login/create-the-business-app).

For example, in this [sample use case](../../references/sample-b2b-use-case), **Guardio-SaaS-App** is a business application in **Guardio Insurance**, which is shared with its suborganizations **Best Auto Mart** and **Car Traders**.

<!--

<table>
    <tr>
        <th>System Applications</th>
        <td>
            All the applications/portals are provided by the CIAM Cloud.
        </td>
    </tr>
    <tr>
        <th>Business Applications</th>
        <td>
            B2B applications are hosted by the root organization with its suborganizations. For example: MedConnect, MedStone, MedStar, etc.
        </td>
    </tr>
</table>
-->

## Identity providers

Listed below are the types of federated identity providers used in a B2B business.

<table>
    <tr>
        <th>Organization SSO IdP</th>
        <td>
            <p>This is a federated IdP that is defined in the root organization of the B2B business and enabled for the business applications at the root level. This IdP ensures that suborganization users can be authenticated through their suborganization IdP when they log in to business applications.</p>
            <p>Learn more about <a href="../../guides/organization-login/configure-organization-idp">configuring the organization IdP</a>.</p>
        </td>
    </tr>
    <tr>
        <th>Suborganization</th>
        <td>
            Suborganization in the B2B business will have their own identity providers to authenticate users when they sign in to the B2B business's applications. These suborganization IdPs should be defined as federated IdPs in the application sign-in flow for that specific organization.
        </td>
    </tr>
</table>

<!--

<table>
    <tr>
        <th>Organization SSO IdP</th>
        <td>
            This is a federated IdP that is defined in the root organization of the B2B business and enabled for the business applications at the root level. This IdP ensures that suborganization users can be authenticated through their suborganization IdP when they log in to business applications. 
        </td>
    </tr>
    <tr>
        <th>Suborganization IdP</th>
        <td>
            Suborganization in the B2B business will have their own identity providers to authenticate users when they sign in to the B2B business's applications. These suborganization IdPs should be defined as a sign-in option only for that specific organization.
        </td>
    </tr>
</table>
-->

## User roles

User roles specify the permissions that are granted to a particular user or user group. These may include [permissions](../../guides/b2b-org-management/b2b-org-permissions) to access business applications or to use the Management Console. 

<!--
<table>
    <tr>
        <th>System Roles</th>
        <td>
            Roles that are defined and consumed by system applications. These roles are used to group the permissions of IdP resources.
        </td>
    </tr>
    <tr>
        <th>Platform Roles</th>
        <td>
            Roles that are defined and consumed by business applications. These roles are available across all organizations to manage users and user group assignments. For example, roles that are created for each application to manage access to the respective application such as MEDCONNECT_USER, MEDCONNECT_DIAGNOSTICS_REQUESTOR, MEDCONNECT_REPORT_VIEWER, etc.
        </td>
    </tr>
</table>
-->

## Users/Personas

Listed below are the type of users in the WSO2 CIAM Cloud for B2B businesses. Learn more about [managing users](../../guides/org-user-management).

<table>
    <tr>
        <th>System administrators</th>
        <td>
            Administrators of the super organization who set up and manage the B2B business.
        </td>
    </tr>
    <tr>
        <th>Organization administrators</th>
        <td>
            Administrators of the respective organizations in the B2B business. These administrators are set up by a system administrator and assigned a role with the permissions required.
        </td>
    </tr>
    <tr>
        <th>B2B Consumers</th>
        <td>
            Users within an individual organization who consume the business applications of the B2B business. Consumers are specific to an individual organization. However, they consume business applications of the B2B business through <a href="../../guides/organization-login/org-login-overview">organization login</a>.
        </td>
    </tr>
</table>

<!--
### Collaborators

Consumers that belong to one organization but have access to resources in other organizations.

<table>
    <tr>
        <th>System Administrators</th>
        <td>
            Administrators of the super tenant organization who set up and manage the system.
        </td>
    </tr>
    <tr>
        <th>Organization Administrators</th>
        <td>
            Administrators of the respective organizations.
        </td>
    </tr>
    <tr>
        <th>B2B Consumers</th>
        <td>
            Users within an organization.
        </td>
    </tr>
    <tr>
        <th>Collaborators</th>
        <td>
            Consumers that belong to one organization but have access to resources in other organizations.
        </td>
    </tr>
</table>
-->