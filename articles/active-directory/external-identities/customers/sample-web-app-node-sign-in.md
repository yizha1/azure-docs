---
title: Sign in users in a sample Node.js web application 
description: Learn how to configure a sample web app to sign in and sign out users.
services: active-directory
author: kengaderdus
manager: mwongerapk

ms.author: kengaderdus
ms.service: active-directory
ms.workload: identity
ms.subservice: ciam
ms.topic: sample
ms.date: 06/23/2023
ms.custom: developer, devx-track-js
#Customer intent: As a dev, devops, I want to learn about how to configure a sample Node.js web app to sign in and sign out users with my Azure Active Directory (Azure AD) for customers tenant
---

# Sign in users in a sample Node.js web application 

This how-to guide uses a sample Node.js web application to show you how to add authentication to a web application. The sample application enables users to sign in and sign out. The sample web application uses [Microsoft Authentication Library for Node (MSAL Node)](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) for Node to handle authentication.

In this article, you do the following tasks:

- Register a web application in the Microsoft Entra admin center. 

- Create a sign-in and sign-out user flow in Microsoft Entra admin center.

- Associate your web application with the user flow. 

- Update a sample Node.js web application using your own Azure Active Directory (Azure AD) for customers tenant details.

- Run and test the sample web application.

## Prerequisites

- [Node.js](https://nodejs.org).

- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor.

- Azure AD for customers tenant. If you don't already have one, <a href="https://aka.ms/ciam-free-trial?wt.mc_id=ciamcustomertenantfreetrial_linkclick_content_cnl" target="_blank">sign up for a free trial</a>. 

<!--Awaiting this link http://developer.microsoft.com/identity/customers to go live on Developer hub-->


## Register the web app

[!INCLUDE [active-directory-b2c-register-app](./includes/register-app/register-client-app-common.md)]
[!INCLUDE [active-directory-b2c-app-integration-add-user-flow](./includes/register-app/add-platform-redirect-url-node.md)]  

## Add app client secret 

[!INCLUDE [active-directory-b2c-add-client-secret](./includes/register-app/add-app-client-secret.md)] 

## Grant API permissions

Since this app signs-in users, add delegated permissions:

[!INCLUDE [active-directory-b2c-grant-delegated-permissions](./includes/register-app/grant-api-permission-sign-in.md)] 

## Create a user flow 

[!INCLUDE [active-directory-b2c-app-integration-add-user-flow](./includes/configure-user-flow/create-sign-in-sign-out-user-flow.md)] 

## Associate the web application with the user flow

[!INCLUDE [active-directory-b2c-app-integration-add-user-flow](./includes/configure-user-flow/add-app-user-flow.md)]

## Clone or download sample web application

To get the web app sample code, you can do either of the following tasks:

- [Download the .zip file](https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial/archive/refs/heads/main.zip) or clone the sample web application from GitHub by running the following command:

    ```console
        git clone https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial.git
    ```
If you choose to download the *.zip* file, extract the sample app file to a folder where the total length of the path is 260 or fewer characters.

## Install project dependencies 

1. Open a console window, and change to the directory that contains the Node.js sample app:

    ```console
        cd 1-Authentication\5-sign-in-express\App
    ```
1. Run the following commands to install app dependencies:

    ```console
        npm install && npm update
    ```

## Configure the sample web app

1. In your code editor, open *App\authConfig.js* file. 

1. Find the placeholder: 
    
    1. `Enter_the_Application_Id_Here` and replace it with the Application (client) ID of the app you registered earlier.
     
    1. `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](how-to-create-customer-tenant-portal.md#get-the-customer-tenant-details).
     
    1. `Enter_the_Client_Secret_Here` and replace it with the app secret value you copied earlier.

## Run and test sample web app 

You can now test the sample Node.js web app. You need to start the Node.js server and access it through your browser at `http://localhost:3000`.

1. In your terminal, run the following command:

    ```console
        npm start 
    ```

1. Open your browser, then go to http://localhost:3000. You should see the page similar to the following screenshot:

    :::image type="content" source="media/how-to-web-app-node-sample-sign-in/web-app-node-sign-in.png" alt-text="Screenshot of sign in into a node web app.":::

1. After the page completes loading, select **Sign in** link. You're prompted to sign in.

1. On the sign-in page, type your **Email address**, select **Next**, type your **Password**, then select **Sign in**. If you don't have an account, select **No account? Create one** link, which starts the sign-up flow.

1. If you choose the sign-up option, after filling in your email, one-time passcode, new password and more account details, you complete the whole sign-up flow. You see a page similar to the following screenshot. You see a similar page if you choose the sign-in option.

    :::image type="content" source="media/how-to-web-app-node-sample-sign-in/web-app-node-view-claims.png" alt-text="Screenshot of view ID token claims.":::

1. Select **Sign out** to sign the user out of the web app or select **View ID token claims** to view ID token claims returned by Microsoft Entra. 

### How it works

When users select the **Sign in** link, the app initiates an authentication request and redirects users to Azure AD for customers. On the sign-in or sign-up page that appears, once a user successfully signs in or creates an account, Azure AD for customers returns an ID token to the app. The app validates the ID token, reads the claims, and returns a secure page to the users.  

When the users select the **Sign out** link, the app clears its session, the redirect the user to Azure AD for customers sign-out endpoint to notify it that the user has signed out.   

If you want to build an app similar to the sample you've run, complete the steps in [Sign in users in your own Node.js web application](tutorial-web-app-node-sign-in-prepare-tenant.md) article. 

## Next steps

You may want to: 

- [Enable password reset](how-to-enable-password-reset-customers.md)

- [Customize the default branding](how-to-customize-branding-customers.md)
 
- [Configure sign-in with Google](how-to-google-federation-customers.md)

- [Sign in users in your Node.js web application](tutorial-web-app-node-sign-in-prepare-tenant.md)
