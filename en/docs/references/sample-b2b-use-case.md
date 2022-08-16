# Sample B2B CIAM use case

**Guardio** is an auto insurance service company that has partnerships with two other organizations **Best Auto Mart** and **Car Traders**. Users of Car Traders and Best Auto Mart should be able to use the services offered by Guardio Insurance. Guardio Insurance offers its services through an application named **Guardio-SaaS-App**.

<img src="../../assets/img/guides/organization-login/try-it-out/scenario_diagram.png" alt="Scenario Diagram" width="700">

Guardio Insurance is using the WSO2 CIAM Cloud to manage the identity and access requirements of all consumers of its partner organization. This requirement is handled in the WSO2 CIAM Cloud as follows:

-   The two partner organizations **Best Auto Mart** and **Car Traders** are registered as suborganizations of **Guardio** in the WSO2 CIAM Cloud.
-   The **Guardio-SaaS-App** app is registered in the root organization (Guardio) as a SaaS application and configured with the organization login option.
-   The **Guardio-SaaS-App** app is shared with its suborganizations as a fragment app (copy of the SaaS app). This allows each sub organization to update the sign-in flow for for its own user base by adding its own IdP to the application sign-in flow.
-   Users of the suborganizations will then be able to sign in to the **Guardio-SaaS-App** app as follows:

    1.  Access the application on a browser.
    2.  Use the Organization Login option on the login page.
    2.  In the next step, select the organization IdP and log in.

    The user is now authenticated with the organization's own IdP when accessing the **Guardio-SaaS-App** app.

<!--

## Terminology

-   Service provider

	Business that provide the software as a service with a B2B relationship

-   Service provider application

	Application or service that is provided by the service provider

-   IdP of the service provider

    Identity provider of the service provider business.  Identity server product is intended to be used for this purpose in this scenario.

-   Consuming business

    Business that consumes the application or the service provided by the service provider.

-   IdP of the consuming business

    Identity provider of the consuming business. This IdP can contain the employees or the end consumers.
-->
