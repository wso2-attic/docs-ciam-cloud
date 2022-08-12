# Organization domains and URLs

## Organization URLs

As a part of the B2B Organization Management feature, incorporated the organization identifier as first-class support for the URLs (similar to the current tenant specific endpoints) by introducing a path param to denote the specific organization to which the request should be directed to.

URL format - o/{organization id}/…

Organization-specific routing capability is introduced. The BasicAuthenticationHandler has also been improved to handle authentication when the username has the organization domain(id) appended.

The current behavior in BasicAuthenticationHandler is that if the username doesn't have the organization domain, the user is authenticated against the ROOT organization.
It was decided to improve the authentication logic as given below.
-   If the username doesn't have the organization domain, the user is authenticated against the /o/<org>.
-   Else retrieve the organization domain from the username (break from the last @ in the username) and authenticate the user against that organization.

Assume that mary is a user of orgA and she creates orgB as a child of orgA.
-   /o/<orgA domain>/.... -> mary@<orgA domain> (authentication happens against orgA)
-   /o/<orgA domain>/.... -> mary (authentication happens against orgA)
-   /o/<orgB domain>/.... -> mary@<orgA domain> (authentication happens against orgA)
-   /o/<orgB domain>/.... -> mary (authentication happens against orgB. hence will result in a failure)
-   /o/<orgB domain>/.... -> mary@<orgB domain> (authentication happens against orgB. hence will result in a failure)

## Organization Domain

The domain of an Organization is represented by an Organization Domain, sometimes called a User Email Domain.
