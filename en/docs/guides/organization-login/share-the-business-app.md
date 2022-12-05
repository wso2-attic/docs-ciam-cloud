# Share the business app

When the business application is shared with the organizations in the hierarchy, a new application/service provider will be created for each organization. 

Application (Service Provider) property (isFragmentApp) is introduced to denote whether this application is a fragment of the main application. Users are allowed to update only the Sign-In Method in a fragment application. The fragment application contains an OAuth consumer application, which is used at the user login to redirect to the correct organization login.

## Prerequisites

First, [configure your business apps](../create-the-business-app#configure-the-login-flow) in the root organization as required.

!!! info
    Note that you cannot share fragment applications. A fragment application is an app belonging to a different organization that has been shared with your organization.

## Share the application

Follow the steps given below to share a business application with suborganizations in the organization structure.

1.  On the Management Console, go to **Develop > Applications** to view the list of applications.
        
2.  Click **Share Appliction** and select the organization(s) with which you want to share the application.

    <img src="../../../assets/img/guides/organization-login/share-the-business-app/share_application.png" alt="Share Application" width="700" style="border:1px solid grey">

3.  Click **Share Application** to proceed.

    <img src="../../../assets/img/guides/organization-login/share-the-business-app/share_application_with_organizations.png" alt="Share Application with Organizations" width="400" style="border:1px solid grey">

The fragments applications are now created in the suborganizations.

## View the fragment apps

Now, switch to the organization you’ve shared the application with and you will see this application as a fragment application in its application list.

<img src="../../../assets/img/guides/organization-login/share-the-business-app/fragment_application.png" alt="Fragment Application" width="700" style="border:1px solid grey">
