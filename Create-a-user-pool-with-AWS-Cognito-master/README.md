# Create a user pool with AWS Cognito

## Overview

[Amazon Cognito](https://aws.amazon.com/tw/cognito/) not only lets you add user sign-up, **authorization**, sign-in, and access control to your web and mobile apps quickly and easily but also scales to millions of users. Moreover, your users can sign in through **a third party** such as Facebook, Amazon, or Google and **enterprise identity** providers via SAML 2.0.

Two main components of Amazon Cognito are **user pools** and **identity pools**. User pools are user directories that provide sign-up and sign-in options for your app users. What's more, it also recorded all the users from your Web or application. Identity pools enable you to grant your users access to other AWS services. You can use identity pools and user pools separately or together.

## Scenario

Ｗith this lab, you will create your user pool use built-in webpages available for signing up and signing in your users. Amazon Cognito hosted UI is the foundation for other features such as the ability to sign in directly to your user poor thorough third party as well as through OpenID Connect(OIDC) and SAML identity providers.


## Step by Step

### Build static web hosting
You will setup static web hosting in S3.

1. Download index.html on this file.

2. On service menu, choose **S3**.

3. Click **create bucket** and **Create**.

    * Bucket name: `cognitoyourname`.

4. Type your bucket name in the field of Search for buckets, then choose your bucket.

<p align="center">
   <img src="image /009-Cognito_S3-01.jpg" width="70%" height="70%">
</p>

5. Click **upload**, select index.html and **upload**.

6. Choose **Permissions** tab and **public access settings**.

    * **edit** and **unclick** four option and **save**.

<p align="center">
   <img src="image /010-Cognito_S3-02.jpg" width="70%" height="70%">
</p>

7. Enter `confirm` in the field and **Confirm**.

<p align="center">
   <img src="image /011-Cognito_S3-03.jpg" width="70%" height="70%">
</p>

8. Select your index.html and click tab **Permissions**.

    * Select **everyone** and **Read Object** and **save**.

<p align="center">
   <img src="image /012-Cognito_S3-04.jpg" width="70%" height="70%">
</p>

9. Return to previous page.

10. Select **Properties** tab and choose **static website hosting**.

<p align="center">
   <img src="image /014-Cognito_S3-06.jpg" width="70%" height="70%">
</p>

11. Select **Use this bucket to host a website**, input `index.html` and **save**.

<p align="center">
   <img src="image /015-Cognito_S3-07.jpg" width="60%" height="60%">
</p>

### Adding an App client
Create a client pool to log in your website.

1. Under Service menu, choose **Cognito**.

2. Choose left one **Manage User Pools** and **Create a user pool** storing user's information.

3. Enter `UserPool_yourname` for Pool name and click **Step through settings**.

4. On the left panel, choose **App clients** and click **add an app client**.

5. Enter `myclient_yourname` on App client name, **unclick** Generate client secret and create.

<p align="center">
   <img src="image /001-Cognito_appclient-01.jpg" width="70%" height="70%">
</p>

6. Click **Return to pool details** and click **Create pool**.

7. On Enabled Identity Providers click **Select All**.

8. Enter `S3 bucket's Object URL` in **Callback URL(s)**

    * Go to S3 console and select your bucket and click index.html and copy **Object URL**.

<p align="center">
   <img src="image /002-Cognito_clientsetting-01.jpg" width="70%" height="70%">
</p>

9. Click **Save changes** and Choose **domain name**.

10. Enter `yourname` in **your domain name** or webpages you are willing to protect and click check availability to make sure your name is usable and Save changes.

## Test your website

**Login to your webpage**

Log in to your web using AWS Cognito.

1. Open a new tab, enter
```
https://<your domain>/login?response_type=code&client_id=<your_app_client_id>&redirect_uri=<your_callback_url>
```
>  You can find **your_domain** on the left panel App integration and click **Domain name**. 

> You can find **your_app_cleient_id**, **your_callback_url** on the left panel App integration and click **App client setting**.

For example：
```
https://yourname.auth.yourregion.amazoncognito.com/login?response_type=token&client_id=1234xxxxxx123xxxx78x93x80x&redirect_uri=https://s3.amazonaws.com/yourbucketname/index.html
```

2. You can login or register.

<p align="center">
   <img src="image /003-Cognito_login-01.jpg" width="60%" height="60%">
</p>

3. Sign up for an acount.

<p align="center">
   <img src="image /004-Cognito_signin-01.jpg" width="60%" height="60%">
</p>

4. Receive a verify email.

<p align="center">
   <img src="image /016-Cognito_Verifyemail-02.jpg" width="60%" height="60%">
</p>

5. Login to your webpage see this webpage.

<p align="center">
   <img src="image /008-Cognito_Web-01.jpg" width="70%" height="70%">
</p>

6. Back to Cognito, you can check the account you registered.

<p align="center">
   <img src="image /007-Cognito_member-01.jpg" width="70%" height="70%">
</p>

## Furthermore
**User Pools** 

A user pool is a user directory in Amazon Cognito. Your users can sign in to your web or mobile app through Amazon Cognito, or federate through a third-party identity provider (IdP). No matter which one user choose to log in, you can see all the member information in you AWS Cognito.

**Identity Pools**

With an identity pool, your users can obtain temporary AWS credentials to access AWS services, such as Amazon S3 and DynamoDB. I


## Conclusion

You have learned how to write a login webpages with AWS Cognito. You can log in to webpages and register a new account. All the information will show on AWS Cognito user pool.

Now you can try to create your own login webpages or application with AWS Cognito. Authentication, authorization, and user management for your web and mobile apps become more and more important issue. Therefore, you should try AWS Cognito to protect your webpages.

## Reference

1. AWS Cognito : [here](https://aws.amazon.com/tw/cognito/)

2. AWS Cognito document: [here](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)