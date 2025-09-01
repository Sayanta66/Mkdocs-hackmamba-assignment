# Adding Email-Password Login to your Application

Protekt allows you to add email-password authentication to any application in an instant. This guide will help you configure email login in the Protekt dashboard and add email-password authentication in your application.

## Prerequisites

Before proceeding, it's important to make sure you've done a few things first. These are:

* Sign-up for a **free Protekt account** and access the **Protekt dashboard** to create an **application**. Learn about our dashboard configuration from the [configuration guide](../../Getting%20Started/Configuration.md).
* Obtain your **Client ID** and **Domain** from the application settings.
* A basic understanding of your development stack (e.g., JavaScript, React.js, Vue.js, etc.) and installations of your tech stack dependencies.

## 1. Enable Email-Password Login in the Dashboard

Before integrating the email-password login in your application, enable it from the dashboard and specify the required details. To enable email login in the Protekt dashboard:

1. Log in to the [Protekt dashboard](https://protekt.dev/login).
2. Navigate to **Authentication** > **Methods**.
3. Toggle the **Email + Password** button to **enabled**. Further instruction on password configuration will appear.
4. Set the minimum length of the password according to your requirements.
5. Set the password complexity by checking the required options. The available options are **Must have a capital letter** and **Must have a special character**.
6. Click on **More Password Settings** to set the password reset rules.
    * Set the number of days after which the user has to reset the password.
7. Click **Okay**.

## 2. Configure the Email Templates

Protekt helps you in delivering system emails like welcome, verification, and password-reset emails. To configure such email templates:

1. Go to **Authentication** > **Email Settings**.
2. Use the Protekt-provided templates by default or customize your own template.
3. To use the default templates:
    * Select the template for each purpose according to your liking.
4. To use a customized template:
    * Apply the HTML, CSS, and JS code snippets as required in the respective fields.
    * Click **Apply**.
5. If you are using a custom email provider, ensure that the **SMTP settings** are verified by clicking on the **SMTP Configuration** collapsible. To do that:
    * Enter the **SMTP Host** (e.g., smtp.gmail.com).
    * Ensure the **Port** for the configuration (**587** for **TLS**, **465** for **SSL**).
    * Enter your **Username** (usually your email address).
    * Enter the **Password/App Password** given for the email provider (or **SMTP token** from your provider).
    * Specify the **From Address** (the email address from which the users will receive, e.g., noreply@yourapp.com).
    * Click **Save**.
    * Click **Send Test Email** to verify the applied settings.
    * Enter your email address. Protekt will try to send an email to your email address.
    * If you receive the email, the applied settings are verified :white_check_mark:.
6. Click **Save Template**.

>Note: More details on the configuration of email templates can be found in [Email Templates](../../Branding%20and%20Customization/EmailTemplates.md).

## 3. Integrate Email-Password Login in your Application

After verifying all of the above settings and configuration, it's time to integrate the email-password login into your application. Try out the methods below to integrate it through your preferred tech stacks.

=== "JavaScript"

    1. Install the Protekt JS SDK
    
        Protekt provides a JavaScript SDK to simplify the process of integrating Protekt authentication with your application. Install the SDK by executing the following command in your terminal.
        ```
        npm install @protekt/js
        ```
    2. Create the Protekt Client

        Create a new Protekt client provided by the SDK and provide the **Client ID** and **Domain** that you obtained earlier. The following code snippet will help you do that:
        ```
        import ProtektAuth from "@protekt/js";

        const auth = new ProtektAuth({
            clientId: "YOUR_CLIENT_ID",
            domain: "YOUR_DOMAIN.protekt.dev"
        });
        ```
    3. Add Signup to your Application

        After the client setup is done, you need to set up the signup mechanism for new users in your application. To do this, use the `auth.signupWithEmail()` method to create a new user account with email and password. The following code block helps you do that.
        ```
        async function signup(email, password) {
              try {
                await auth.signupWithEmail({ email, password });
                alert("Check your email to verify your account!");
            } catch (err) {
                console.error(err);
            }
        }
        ```
    4. Add Login for Existing Users in your Application

        Once the signup mechanism is added, the login mechanism needs to be added for the existing users in the application. Use the `auth.loginWithEmail()` method to authenticate an existing user. The code snippet below will help you add that.
        ```
        async function login(email, password) {
            try {
                const tokens = await auth.loginWithEmail({ email, password });
                console.log("Access Token:", tokens.accessToken);
            } catch (err) {
                console.error(err);
            }
        }
        ```
    5. Add SignOut to your Application

        Finally, once the sign-up/login for a user is completed, it's time to put the sign-out mechanism in place, through which a user will sign out or log out from the application. The auth.logout() method will help in doing that. The following code snippets show how to use that method.
        ```
        async function signout() {
          try {
            await auth.logout();
            console.log("User signed out successfully.");
            window.location.href = "/login";
            } catch (err) {
                console.error("Sign out failed:", err);
            }
        }
        ```

=== "React"

    1. Install the Protekt React SDK
    
        Protekt provides a React.js SDK to simplify the process of integrating Protekt authentication with your application. Install the SDK by executing the following command in your terminal.
        ```
        npm install @protekt-react/js
        ```
    2. Create the Protekt Client

        Create a new Protekt client provided by the SDK and provide the **Client ID** and **Domain** that you obtained earlier. The following code snippet will help you do that:
        ```
        import React, { useState } from "react";
        import ProtektAuth from "@protekt-react/js";

        const auth = new ProtektAuth({
        clientId: "YOUR_CLIENT_ID",
        domain: "YOUR_DOMAIN.protekt.dev"
        });
        ```
    3. Add Signup to your Application

        After the client setup is done, you need to set up the signup mechanism for new users in your application. To do this, use the `auth.signupWithEmail()` method to create a new user account with email and password. The following code block helps you do that.
        ```
        async function signup(email, password) {
              try {
                await auth.signupWithEmail({ email, password });
                alert("Check your email to verify your account!");
            } catch (err) {
                console.error(err);
            }
        }
        ```
    4. Add Login for Existing Users in your Application

        Once the signup mechanism is added, the login mechanism needs to be added for the existing users in the application. Use the `auth.loginWithEmail()` method to authenticate an existing user. The below code snippet will help you add that.
        ```
        async function login(email, password) {
            try {
                const tokens = await auth.loginWithEmail({ email, password });
                console.log("Access Token:", tokens.accessToken);
            } catch (err) {
                console.error(err);
            }
        }
        ```
    5. Add Signout to your Application

        Finally, once the sign-up/login for a user is completed, it's time to put the sign-out mechanism in place, through which a user will sign out or log out from the application. The auth.logout() method will help in doing that. The following code snippets show how to use that method.
        ```
        async function signout() {
          try {
            await auth.logout();
            console.log("User signed out successfully.");
            window.location.href = "/login";
            } catch (err) {
                console.error("Sign out failed:", err);
            }
        }
        ```

=== "Angular"

    1. Install the Protekt Angular SDK
    
        Protekt provides a Angular.js SDK to simplify the process of integrating Protekt authentication with your application. Install the SDK by executing the following command in your terminal.
        ```
        npm install @protekt-angular/js
        ```
    2. Create the Protekt Client

        Create a new Protekt client provided by the SDK and provide the **Client ID** and **Domain** that you obtained earlier. The following code snippet will help you do that:
        ```
        import { Injectable } from '@angular/core';
        import ProtektAuth from "@protekt-angular/js";

        const auth = new ProtektAuth({
            clientId: "YOUR_CLIENT_ID",
            domain: "YOUR_DOMAIN.protekt.dev"
        });
        ```
    3. Add Signup in your Application

        After the client setup is done, you need to set up the signup mechanism for new users in your application. To do this, use the `auth.signupWithEmail()` method to create a new user account with email and password. The following code block helps you do that.
        ```
        async function signup(email, password) {
              try {
                await auth.signupWithEmail({ email, password });
                alert("Check your email to verify your account!");
            } catch (err) {
                console.error(err);
            }
        }
        ```
    4. Add Login for Existing Users in your Application

        Once the signup mechanism is added, the login mechanism needs to be added for the existing users in the application. Use the `auth.loginWithEmail()` method to authenticate an existing user. The below code snippet will help you add that.
        ```
        async function login(email, password) {
            try {
                const tokens = await auth.loginWithEmail({ email, password });
                console.log("Access Token:", tokens.accessToken);
            } catch (err) {
                console.error(err);
            }
        }
        ```
    5. Add Signout to your Application

        Finally, once the sign-up/login for a user is completed, it's time to put the sign-out mechanism in place, through which a user will sign out or log out from the application. The auth.logout() method will help in doing that. The following code snippets show how to use that method.
        ```
        async function signout() {
          try {
            await auth.logout();
            console.log("User signed out successfully.");
            window.location.href = "/login";
            } catch (err) {
                console.error("Sign out failed:", err);
            }
        }
        ```
!!! tip "More integrations"
    
    For more detailed integration with different tech stacks, check out our [integration guides](../../Getting%20Started/Integrations/).

## Next Steps

Congratulations! You have made it this far. This means that you have successfully integrated the Protekt email-password authentication in your application. The journey doesn't end here.

To learn more about what you can do with Protekt, check out the below features and resources:

* [Self-Host Protekt](../../Deployment/)
* [Multifactor Authentication](../../Multifactor%20Authentication%20(MFA)/)