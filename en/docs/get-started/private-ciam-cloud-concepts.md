# Concepts

Given below are concepts you will use when you work with WSO2 Private CIAM Cloud for your B2B organizational requirements.

## Organizations

An organization represents a grouping of users and other organizations in the WSO2 Private CIAM Cloud. You can maintain multiple organizations within a single organization that depicts a hierarchical or flat organizational structure. 

The WSO2 Private CIAM Cloud can manage a large number of roles and user groups within an organizational boundary. Because organizations are isolated from one another, businesses can maintain their own enterprise structures and identity providers.

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
            <p>The identifier of the organization where sub organizations are created.</p>
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

## Applications

<table>
    <tr>
        <th>System Applications</th>
        <td>
            All the applications/portals provided by the CIAM Private Cloud.
        </td>
    </tr>
    <tr>
        <th>Business Applications</th>
        <td>
            B2B applications hosted by the root organization with its sub organizations. For exmaple: MedConnect, MedStone, MedStar, etc.
        </td>
    </tr>
</table>

## Roles

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

## User/Persona

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
            Consumers belonging to one organization but having access to resources in other organizations.
        </td>
    </tr>
</table>