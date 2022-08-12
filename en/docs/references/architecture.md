# Architecture

## B2B organizations

Identifying the needs and wants of the user group is a crucial factor in utilizing a product. To gain the most out of identity server solution, it's better to identify their target audience needs and try to cater it with the provided solution. But he we are providing more advanced feature which will enable your business to operate in hierachycal manner. Not like in a simple IdP solution, we provide the organizational IdP solution which prefectly fits to your desired application. Identity Server Accounts and Organizations serve as the foundation for organizing and grouping Identity Server assets, and it's possible that you'll need to use an existing Identity Server deployment to integrate with Single Sign-on (SSO), centralized user profile management, consolidated billing, or similar features.

## B2B2C organizations

Some B2B CIAM use cases can be generic for B2B2C and B2B, but some can be grouped into requirements in B2B2C and B2B.

##  Generic requirements

We could identify below driving factors in B2B2C and B2B businesses and user cases in each driving factor.

### Application driven use cases

-   Same set of services being consumed by all the business users
-   Onboarding businesses have the choice of subscribing for selected set of services

## Specific requirements
(End user is a consumer of the consuming business)
We could identify below driving factors in B2B2C businesses and user cases in each driving factor.

### User driven use cases

-   Based on user account management strategies, below options are available.
    -   End users (consumers) need to be managed at the IdP of the service provider.
    -   End users (consumers) are onboarded by connecting an IdP from the consuming business where these users are managed
        -   No user management (user credentials, lifecycle)
        -   Application side authorization is managed at the application level
            -   Only users are provisioned and user authorization is handled at the application level
            -   Decision on the authorization can be taken by utilizing user identity info (user groups, a meta info)
        -   Their credential, lifecycle and profile needs to be managed
        -   Ex:  HealthyFoods is a food supplier for hospitals.Patients in the hospitals that are partnered with the hospitals can log in to HealthyFoods portal and order the food for their rooms. Hospital2 is already managing its own IdP to manage patients and Hospital2 wants to provide capability for its patients to consume the service. 
    -   Users can come from the IdP of the consuming business, but user credential or/and user lifecycle can be managed by and IdP of the service provider. This is a hybrid status of the above options.
-   Based on user collaboration requirements, below options are available.
    -   Users can collaborate with consuming businesses (organization) for service management (admin collaboration)
        -   Ex: Employees of one business, partners of the service provider, collaborate with businesses onboarded to the platform to help them set up functionalities and start
    -   Consumer collaboration is not considered. Consumer accounts are private to the consuming business.
