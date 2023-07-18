--- 
template: templates/single-column.html 
---

<style>

    @font-face {
    font-family: 'Material Icons';
    font-style: normal;
    font-weight: 400;
    src: url(https://wso2.cachefly.net/wso2/sites/all/fonts/docs/flUhRq6tzZclQEJ-Vdg-IuiaDsNcIhQ8tQ.woff2) format('woff2');
    }

    .material-icons {
    font-family: 'Material Icons';
    font-weight: normal;
    font-style: normal;
    font-size: 24px;
    line-height: 1;
    letter-spacing: normal;
    text-transform: none;
    display: inline-block;
    white-space: nowrap;
    word-wrap: normal;
    direction: ltr;
    -webkit-font-feature-settings: 'liga';
    -webkit-font-smoothing: antialiased;
    }


</style>


<div>
    <header>
        <h1>Welcome to the WSO2 Private CIAM Cloud Documentation!</h1>
    </header>
    <div class="md-main .md-content" style="float:left; width: 100%;  text-align:justify; max-height:100%; ">
        WSO2 Private CIAM Cloud is a fully managed customer identity and access management (CIAM) platform that helps you build effective B2B CIAM solutions for your organizations. You can innovate fast and deploy projects on your dedicated cloud infrastructure in your region. In addition to containing all of the capabilities of [WSO2 Identity Server 6.0.0](https://is.docs.wso2.com/en/6.0.0/), WSO2 Private CIAM Cloud has new organization management capabilities for B2B CIAM deployments.  
    </div>
    <div>
        <div class="content">
            <!-- begin card -->
            <div class="card-wrapper">
                <div class="card" onclick="location.href='guides/b2b-org-management/b2b-org-mgt-overview/';">
                    <div class="line"></div>
                    <div class="icon">
                        <img src="assets/img/intro/organization-management.svg">
                    </div>
                    <div class="card-content">
                        <p class="title">Organization Management</p>
                        <a href="http://www.google.com"></a>
                        <p class="hint">Manage the organizations in your B2B business</p>
                    </div>
                </div>
            </div>
            <!-- end card -->
            <!-- begin card -->
            <div class="card-wrapper">
                <div class="card" onclick="location.href='guides/org-user-management/';">
                    <div class="line"></div>
                    <div class="icon">
                        <img src="assets/img/intro/user-management.svg">
                    </div>
                    <div class="card-content">
                        <p class="title">User Management</p>
                        <p class="hint">Manage users in organizations of your B2B business</p>
                    </div>
                </div>
            </div>
            <!-- end card -->
            <!-- begin card -->
            <div class="card-wrapper">
                <div class="card" onclick="location.href='guides/organization-login/org-login-overview/';">
                    <div class="line"></div>
                    <div class="icon">
                        <img src="assets/img/intro/organization-login.svg">
                    </div>
                    <div class="card-content">
                        <p class="title">Organization Login</p>
                        <p class="hint">Enable login for business applications using organization IdPs</p>
                    </div>
                </div>
            </div>
            <!-- end card -->
            <!-- card for connectors -->
            <!-- end card -->
        </div>
    </div>
</div>