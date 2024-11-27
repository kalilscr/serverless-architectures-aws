## **Lab overview**

In this lab, after deploying the serverless backend using AWS SAM and API Gateway, you use AWS Amplify to deploy the frontend of the grid-maker application and configure it to authenticate using Amazon Cognito.

AWS Amplify is a development platform that provides a set of tools and services for building scalable and secure mobile and web applications. In this lab, you will use Amplify to deploy the frontend of the grid-maker application, which is a web application that allows users to interact with the serverless backend. Amplify simplifies the deployment process by providing easy-to-use tools and services that automate tasks like building, testing, and deploying applications.

To authenticate users, the lab uses Amazon Cognito, a managed authentication service that allows you to easily add user sign-up, sign-in, and access control to your applications. Cognito provides several features, including user pools, identity pools, and multi-factor authentication, that allow you to secure your application and control access to resources.

During the lab, you configure Amplify to use Cognito for authentication and authorization. You create a user pool in Cognito, which stores user accounts and user attributes, and an identity pool, which provides temporary AWS credentials to users. You then integrate Amplify with Cognito and configure the frontend to use the Cognito user pool for authentication.

By the end of the lab, you have a complete serverless application that includes a frontend deployed using Amplify and a backend deployed using SAM and API Gateway. You gain an understanding of how to use Amplify to deploy frontend applications and how to use Cognito for authentication and authorization.

### **Objectives**

By the end of this lab, you will be able to do the following:

* Install requirements to use AWS Amplify CLI.  
* Initialize AWS Amplify and deploy a project.  
* Configure Cognito to authenticate with the application.  
* Run the grid-maker application using authentication to create the grid image.

### **Technical knowledge prerequisites**

To successfully complete this lab:

* Familiarity with the basic navigation of the AWS Management Console.  
* Versed in editing and running scripts using an AWS Cloud9 code editor and terminal.  
* A basic understanding and familiarity with Amazon API Gateway, AWS Serverless Application Model (SAM), AWS Lambda, AWS CloudFormation, and AWS Amplify.  
* Prior experience with AWS services including AWS Amplify and serverless computing will be helpful but is not necessarily required.

### **Duration**

This lab requires *60* minutes to complete.

### **Icon key**

Various icons are used throughout this lab to call attention to different types of instructions and notes. The following list explains the purpose for each icon:

* **Caution:** Information of special interest or importance (not so important to cause problems with the equipment or data if you miss it, but it could result in the need to repeat certain steps).  
* **Command:** A command that you must run.  
* **Expected output:** A sample output that you can use to verify the output of a command or edited file.  
* **Note:** A hint, tip, or important guidance.  
* **Consider:** A moment to pause to consider how you might apply a concept in your own environment or to initiate a conversation about the topic at hand.  
* **Task complete:** A conclusion or summary point in the lab.  
* **Warning:** An action that is irreversible and could potentially impact the failure of a command or process (including warnings about configurations that cannot be changed after they are made).

## **Start lab**

1. To launch the lab, at the top of the page, choose **Start Lab**.

    **Caution:** You must wait for the provisioned AWS services to be ready before you can continue.

2. To open the lab, choose **Open Console**  
1. .

    You are automatically signed in to the AWS Management Console in a new web browser tab.

    **Warning:** Do not change the **Region** unless instructed.

### **Common sign-in errors**

#### **Error: Choosing Start Lab has no effect**

In some cases, certain pop-up or script blocker web browser extensions might prevent the **Start Lab** button from working as intended. If you experience an issue starting the lab:

* Add the lab domain name to your pop-up or script blocker’s allow list or turn it off.  
* Refresh the page and try again.

---

## **Task 1: Install and initialize AWS Amplify**

In this task, you connect to the AWS Cloud9 environment to install the Amplify CLI and its dependencies globally. Once installed you initialize Amplify. This will create all of the files and resources to deploy this project.

Amplify CLI is a command-line interface tool that you can use to configure and deploy your application. To install the Amplify CLI, you need to have *Node.js*, *npm* (Node.js Package Manager), and the Amplify dependencies installed. Node.js and npm are already installed.

You run the *npm install* from the \~/python-image-grid/react-amplified directory and npm dependencies are installed based on the *package.json* file.

### **Task 1.1: Connect to the AWS Cloud9 environment**

AWS Cloud9 is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. It includes a code editor, debugger, and terminal. AWS Cloud9 comes prepackaged with essential tools for popular programming languages including JavaScript, Python, PHP, and more. You do not need to install files or configure your development machine to start new projects.

In this task, you connect to the AWS Cloud9 environment provisioned as part of this lab.

3. Copy the **Cloud9Environment** URL link from the **Lab Information** section to the left of these instructions and paste it into a new browser tab. The browser takes you to the AWS Cloud9 environment that you use during this lab.

4. You do not need the **Cloud9 Welcome screen** or any of the other default tabs that appear when you first launch **Cloud9**, so choose the **x** next to each tab to close them. This section is where you update various file throughout this lab.

**Consider:** Take a moment to familiarize yourself with the **AWS Cloud9** IDE interface.

* In the middle of the screen, a single terminal session is open in the editor. You can open multiple tabs in this window to edit files and run terminal commands.  
* The file navigator appears on the left side of the screen. As you build out your CDK environment and application, additional directories and files appear here.  
* A gear icon appears on the right side of the screen. Choosing this icon opens the AWS Cloud9 Settings panel.

Every *AWS Cloud9* workspace is automatically assigned *IAM* credentials that provide it with limited access to some AWS services in your account based on your federated role. We call these AWS managed temporary credentials.

### **Task 1.2: Install npm and the Amplify CLI**

5. **Command:** Update the credentials used for this lab and use *npm* to install the *Amplify CLI dependencies*, based on the **package.json** file, with the following commands.

\# Update credentials  
update\_credentials

\# Change to directories to react-amplified  
cd \~/environment/react-amplified/

\# Install the dependencies  
npm install

**Expected output:** Output has been truncated. Your values may differ slightly.

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

npm warn deprecated inflight@1.0.6: This module is not supported, and leaks memory. Do not use it. Check out lru-cache if you want a good and tested way to coalesce async requests by a key value, which is much more comprehensive and powerful.  
npm warn deprecated rimraf@3.0.2: Rimraf versions prior to v4 are no longer supported  
npm warn deprecated glob@7.2.3: Glob versions prior to v9 are no longer supported

added 26 packages in 14s

7 packages are looking for funding  
  run \`npm fund\` for details

**Note:** All deprecation warning messages can be ignored.

6. **Command:** With the Amplify CLI dependencies installed, you can now install the Amplify CLI globally with the following command:

npm install \-g @aws-amplify/cli@12.8.2

**Expected output:** Your values may differ slightly.

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

npm warn deprecated inflight@1.0.6: This module is not supported, and leaks memory. Do not use it. Check out lru-cache if you want a good and tested way to coalesce async requests by a key value, which is much more comprehensive and powerful.  
npm warn deprecated rimraf@3.0.2: Rimraf versions prior to v4 are no longer supported  
npm warn deprecated glob@7.2.3: Glob versions prior to v9 are no longer supported

added 7 packages, and changed 26 packages in 14s

7 packages are looking for funding  
  run \`npm fund\` for details

**Note:** All deprecation warning messages can be ignored.

### **Task 1.3: Initialize Amplify**

Next, you initialize Amplify. During this step it creates all of the files and resources required to deploy this project.

7. **Command:** To initialize Amplify, run the following *amplify init* command:

**Caution:** The following commands create a variable for the Permissions Boundary ARN to help further secure the lab as Amplify has to create a few roles.

cd /home/ec2-user/environment/react-amplified

boundary\_policy=$(aws iam list-policies \--query 'Policies\[?PolicyName==\`AmplifyPermissionsBoundary\`\].Arn' \--output text)

amplify init \--permissions-boundary $boundary\_policy

8. You will be asked a series of questions. Use the following answers:

⚠️ For new projects, we recommend starting with AWS Amplify Gen 2, our new code-first developer experience. Get started at https://docs.amplify.aws/react/start/quickstart/

* For **Enter a name for the project (reactamplified)**, press **Enter** to use the default value.

* For **Initialize the project with the above configuration?**, accept default value for

Yes  
.

For **Select the authentication method you want to use:**, choose  
AWS profile  
.

For **Please choose the profile you want to use**, choose

* default  
  .

**Note:** Should you setup Amplify in your own environment. Please know that Amplify needs something in the *\~/.aws/config* file to be able to find and use the *default profile* in the *credentials* file that AWS Cloud9 configures with a temporary access key and secret access key. When bootstrapping the AWS Cloud9 environment, the *config* file was created to include the *output* format as *json*. Otherwise, it does not find it and asks if you want to create a user for this step.

It now initializes the Amplify project and create the required AWS resources.

* **Command:** For **Help improve Amplify CLI by sharing non sensitive configurations on failures (y/N)**, accept the default selection of **N**.

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Adding backend environment dev to AWS Amplify app: d3sogr4oscggoz

Deployment completed.  
Deploying root stack reactamplified \[ \==========------------------------------ \] 1/4  
        amplify-reactamplified-dev-18… AWS::CloudFormation::Stack     CREATE\_IN\_PROGRESS             Mon Mar 20 2023 18:32:26…       
        AuthRole                       AWS::IAM::Role                 CREATE\_COMPLETE                Mon Mar 20 2023 18:32:46…       
        UnauthRole                     AWS::IAM::Role                 CREATE\_IN\_PROGRESS             Mon Mar 20 2023 18:32:30…       
        DeploymentBucket               AWS::S3::Bucket                CREATE\_IN\_PROGRESS             Mon Mar 20 2023 18:32:30…     

✔ Help improve Amplify CLI by sharing non sensitive configurations on failures (y/N) · no  
Deployment state saved successfully.  
✔ Initialized provider successfully.  
✅ Initialized your environment successfully.

Your project has been successfully initialized and connected to the cloud\!

Some next steps:  
"amplify status" will show you what you've added already and if it's locally configured or deployed  
"amplify add \<category\>" will allow you to add features like user login or a backend API  
"amplify push" will build all your local backend resources and provision it in the cloud  
"amplify console" to open the Amplify Console and view your project status  
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud

Pro tip:  
Try "amplify add api" to create a backend API and then "amplify push" to deploy everything

**Note:** If you get an error stating, *amplify-reactamplified-dev-\#\#\#\#\#\#-deployment already exists.* Run the command again to allow a new bucket name to be created. The *6* digits are generated at random and it is possible to run into duplicates.

Once it finishes, it shows you a list of commands you can now perform.

**Task complete:** You have successfully installed npm, the Amplify CLI and initialized the Amplify project.

---

## **Task 2: Add hosting and authorization to the Amplify project**

In this task, you add *hosting* to the Amplify project. The command *amplify add hosting* adds the hosting resources for the application backend. Once host has been added you publish the project and verify the application is reachable. Then you add authorization to the project using Amazon Cognito.

### **Task 2.1: Add hosting to the Amplify project**

Add *hosting* via the console so the application can be accessed using a URL.

9. **Command:** To enable hosting, run the following command:

amplify add hosting

10. It asks you which hosting option to use. Choose **Hosting with Amplify Console (Managed hosting with custom domains, Continuous deployment)**.

11. For **Choose a type**, select **Manual deployment**.

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

✔ Select the plugin module to execute · Hosting with Amplify Console (Managed hosting with custom domains, Continuous deployment)  
? Choose a type Manual deployment

You can now publish your app using the following command:

Command: amplify publish

It now indicates you are able to publish your project.

### **Task 2.2: Publish the Amplify project**

The command *amplify publish* is designed to build and publish both the backend and frontend of the project. After running *amplify publish \--yes*, your app is available online and your terminal displays your app URL hosted on an *amplifyapp.com* domain. Whenever you have additional changes to publish, just re-run the amplify publish command.

12. **Command:** To publish the project, run the following **amplify** command:

amplify publish \--yes

**Note:** It does take a few minutes for the publishing process to finish.

While it deploys the resources in the AWS environment, open the Amplify console to see what is taking place.

13. At the top of the AWS Management Console, in the search bar, search for and choose  
13. AWS Amplify  
    . Open it in a new browser tab.

14. Once you open the Amplify console, choose the **reactamplified** app link.

15. Under the **Hosting environments** tab you should see a status message reading, “**Waiting to deploy** Your deployment is being queued…”

**Note:** There is a *Backend environments* feature, but you are not using it in this lab. In this lab, you are focusing on using Amplify for *frontend hosting* and then Amplify for setting up *Cognito for authentication*.

16. Switch back to the **AWS Cloud9** browser tab and wait for the publishing to finish.

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

✔ Select the plugin module to execute · Hosting with Amplify Console (Managed hosting with custom domains, Continuous deployment)  
? Choose a type Manual deployment

You can now publish your app using the following command:

Command: amplify publish  
LabUser:\~/environment/react-amplified $ amplify publish  
✔ Successfully pulled backend environment dev from the cloud.

    Current Environment: dev  
      
┌──────────┬────────────────┬───────────┬───────────────────┐  
│ Category │ Resource name  │ Operation │ Provider plugin   │  
├──────────┼────────────────┼───────────┼───────────────────┤  
│ Hosting  │ amplifyhosting │ Create    │ awscloudformation │  
└──────────┴────────────────┴───────────┴───────────────────┘  
✔ Are you sure you want to continue? (Y/n) · yes

Deployment completed.  
Deployed root stack reactamplified \[ \======================================== \] 2/2  
        amplify-reactamplified-dev-18… AWS::CloudFormation::Stack     UPDATE\_COMPLETE                Mon Mar 20 2023 19:59:16…       
        hostingamplifyhosting          AWS::CloudFormation::Stack     CREATE\_COMPLETE                Mon Mar 20 2023 19:59:13…       
Deployed hosting amplifyhosting \[ \======================================== \] 1/1

Deployment state saved successfully.

Publish started for amplifyhosting

\> react-amplified@0.1.0 build  
\> react-scripts build

Creating an optimized production build...  
Compiled with warnings.

\[eslint\]   
src/App.js  
  Line 19:20:  'setUniqueId' is assigned a value but never used  no-unused-vars

Search for the keywords to learn more about each warning.  
To ignore, add // eslint-disable-next-line to the line before.

File sizes after gzip:

  251 kB    build/static/js/main.dca75ce3.js  
  33.44 kB  build/static/css/main.a3e3b07c.css  
  1.79 kB   build/static/js/787.cbb326c1.chunk.js

The project was built assuming it is hosted at /.  
You can control this with the homepage field in your package.json.

The build folder is ready to be deployed.  
You may serve it with a static server:

  npm install \-g serve  
  serve \-s build

Find out more about deployment here:

  https://cra.link/deployment

✔ Zipping artifacts completed.  
✔ Deployment complete\!  
https://dev.d3sogr4oscggoz.amplifyapp.com

17. Once it finishes, you can switch back to the **Amplify** browser tab and see that it now shows that the **Deployment successfully completed.**. You can see the **Domain URL** is listed and that it matches the URL provided in the output in the **Cloud9** console.

18. Open the **URL** in a new browser tab.

The browser shows the application login screen. This uses Cognito to create an account with or to log in with a Cognito username if an account is already created. Cognito has not been configured yet, you configure Cognito in the next step.

![Application login screen][image1]

*Image depicts the application login screen. It has a link to Sign In or Create Account. There is a field for a Username and Password followed by a Sign in button. It also provides a link if you forgot your password, to have it reset.*

### **Task 2.3: Add authentication to the Amplify project**

The *amplify add auth* command is used to add authentication to your app. It creates an Amazon Cognito user pool and identity pool for your app, and configures your app to use them. It offers authentication/authorization services and you use the options to sign-up and sign-in. This application does not use multi-factor authentication (MFA) but it is an option should you need that as a requirement in the future. You configure Cognito to require an email and password to sign up. It sends a confirmation email with a verification code to activate your login credentials.

19. Switch back to the **AWS Cloud9** browser tab.

20. **Command:** Add Cognito authentication by running the **amplify add auth** option for this Amplify project with the following command:

amplify add auth

You are asked a series of questions:

* For the question **Do you want to use the default authentication security configuration?**, choose **Manual configuration**.

* For **User Sign-Up, Sign-In**, chose **user Sign-Up & Sign-In only (Best used with a cloud API only)**.

* For **Provide a friendly name for your resource that will be used to label this category in the project:**, use the **default** value for friendly name for your resource.

* For **Provide a name for your user pool:**, use the **default** value.

* For **How do you want users to sign in**, choose **email**.

* For **Do you want to add User Pool Groups?**, choose **No**.

**Note:** We do not have different levels of access to the application. Everyone gets the same access.

* For **Do you want to add admin queries API?**, choose **No**.

* For **Multifactor authentication (MFA) user login options**, choose **OFF**.

* For E**mail based user registration/forgot password**, choose **Enabled (Requires per-user email entry at registration)**.

* For **Specify an email verification subject: (Your verification code)**, use the **default** value.

* For **Specify and email verification message: Your verification code is {\#\#\#\#}**, use the **default** value.

* For **Do you want to override the default password policy for this User Pool?**, choose **No**.

* For **What attributes are required for signing up?**, choose **Email**.

* For **Specify the app’s refresh token expiration period (in days):**, use the default value of **30**.

* For **Do you want to specify the user attributes this app can read and write?**, use default value of **No**.

* For **Do you want to enable any of the following capabilities?**, press **Enter** to use the default value of **No**.

* For **Do you want to use an OAuth flow?**, choose **No**.

* For **Do you want to configure Lambda triggers for Cognito?**, type  
* n  
  .

Now it has everything it needs to push the changes.

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

✅ Successfully added auth resource reactamplified4c64a58c4c64a58c locally

✅ Some next steps:  
"amplify push" will build all your local backend resources and provision it in the cloud  
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud

21. **Command:** Push the changes to the project with the following command:

amplify push \--yes

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

✅ Successfully added auth resource reactamplified4c64a58c4c64a58c locally

✅ Some next steps:  
"amplify push" will build all your local backend resources and provision it in the cloud  
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud

LabUser:\~/environment/react-amplified $ amplify push  
✔ Successfully pulled backend environment dev from the cloud.

    Current Environment: dev  
      
┌──────────┬────────────────────────────────┬───────────┬───────────────────┐  
│ Category │ Resource name                  │ Operation │ Provider plugin   │  
├──────────┼────────────────────────────────┼───────────┼───────────────────┤  
│ Auth     │ reactamplified4c64a58c4c64a58c │ Create    │ awscloudformation │  
├──────────┼────────────────────────────────┼───────────┼───────────────────┤  
│ Hosting  │ amplifyhosting                 │ No Change │ awscloudformation │  
└──────────┴────────────────────────────────┴───────────┴───────────────────┘  
✔ Are you sure you want to continue? (Y/n)

**Note:** This output shows that the project is going to create the Auth option and that there is no change to the **Hosting** option.

The deployment with the authentication updates start.

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Deployment completed.  
Deploying root stack reactamplified \[ \===========================------------- \] 2/3  
        amplify-reactamplified-dev-18… AWS::CloudFormation::Stack     UPDATE\_IN\_PROGRESS             Mon Mar 20 2023 20:30:12…       
        authreactamplified4c64a58c4c6… AWS::CloudFormation::Stack     CREATE\_COMPLETE                Mon Mar 20 2023 20:31:52…       
        hostingamplifyhosting          AWS::CloudFormation::Stack     UPDATE\_COMPLETE                Mon Mar 20 2023 20:30:18…       
Deployed auth reactamplified4c64a58c4c64a58c \[ \======================================== \] 8/8  
        UserPool                       AWS::Cognito::UserPool         CREATE\_COMPLETE                Mon Mar 20 2023 20:30:26…       
        UserPoolClientWeb              AWS::Cognito::UserPoolClient   CREATE\_COMPLETE                Mon Mar 20 2023 20:30:31…       
        UserPoolClient                 AWS::Cognito::UserPoolClient   CREATE\_COMPLETE                Mon Mar 20 2023 20:30:31…       
        UserPoolClientRole             AWS::IAM::Role                 CREATE\_COMPLETE                Mon Mar 20 2023 20:30:50…       
        UserPoolClientLambda           AWS::Lambda::Function          CREATE\_COMPLETE                Mon Mar 20 2023 20:31:01…       
        UserPoolClientLambdaPolicy     AWS::IAM::Policy               CREATE\_COMPLETE                Mon Mar 20 2023 20:31:20…     

Deployment state saved successfully.

Once finished creating the *Cognito* resources and configuring the application, you need to update the *API* so it requires *authentication*.

**Task complete:** You have added hosting and authorization to the Amplify project.

---

## **Task 3: Configure the application to require authentication**

With the Cognito resources in-place, you now configure the application to use Cognito to authenticate existing users and allow new users to sign up. Then you use the SAM CLI to re-deploy the application with the authentication capabilities.

### **Task 3.1: Update the application to enable authentication**

The *amplify-meta.json* file is generated automatically by the Amplify CLI when you run *amplify init* command. This file contains metadata about your Amplify project and is used by the Amplify library to connect to your cloud resources.

The *amplify-meta.json* file is used by the Amplify CLI to keep track of your project’s backend environment. It contains information about your project’s backend environment such as the *name* of your environment, the *AWS region* where your resources are deployed, and more.

In this task, you obtain the *UserPoolId* value and the *AppClientIDWeb* value to update the SAM template for the API Gateway resource to be able to communicate with Cognito once it is created.

22. **Command:** To view the contents of the **amplify/backend/amplify-meta.json** file, run the following command:

cat \~/environment/react-amplified/amplify/backend/amplify-meta.json

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

{  
  "providers": {  
    "awscloudformation": {  
      "AuthRoleName": "amplify-reactamplified-dev-183225-authRole",  
      "UnauthRoleArn": "arn:aws:iam::111111111111:role/amplify-reactamplified-dev-183225-unauthRole",  
      "AuthRoleArn": "arn:aws:iam::111111111111:role/amplify-reactamplified-dev-183225-authRole",  
      "Region": "us-west-2",  
      "DeploymentBucketName": "amplify-reactamplified-dev-183225-deployment",  
      "UnauthRoleName": "amplify-reactamplified-dev-183225-unauthRole",  
      "StackName": "amplify-reactamplified-dev-183225",  
      "StackId": "arn:aws:cloudformation:us-west-2:111111111111:stack/amplify-reactamplified-dev-183225/90229c70-c74d-11ed-a568-063961e3d8f3",  
      "AmplifyAppId": "d3sogr4oscggoz"  
    }  
  },  
  "hosting": {  
    "amplifyhosting": {  
      "service": "amplifyhosting",  
      "providerPlugin": "awscloudformation",  
      "type": "manual",  
      "providerMetadata": {  
        "s3TemplateURL": "https://s3.amazonaws.com/amplify-reactamplified-dev-183225-deployment/amplify-cfn-templates/hosting/amplifyhosting-template.json",  
        "logicalId": "hostingamplifyhosting"  
      },  
      "lastPushTimeStamp": "2023-03-20T20:32:13.552Z",  
      "output": {},  
      "lastPushDirHash": "xi5ZgYwfYeFOHtERuead8NN4zwo="  
    }  
  },  
  "auth": {  
    "reactamplified4c64a58c4c64a58c": {  
      "service": "Cognito",  
      "providerPlugin": "awscloudformation",  
      "dependsOn": \[\],  
      "customAuth": false,  
      "frontendAuthConfig": {  
        "socialProviders": \[\],  
        "usernameAttributes": \[  
          "EMAIL"  
        \],  
        "signupAttributes": \[  
          "EMAIL"  
        \],  
        "passwordProtectionSettings": {  
          "passwordPolicyMinLength": 8,  
          "passwordPolicyCharacters": \[\]  
        },  
        "mfaConfiguration": "OFF",  
        "mfaTypes": \[  
          "SMS"  
        \],  
        "verificationMechanisms": \[  
          "EMAIL"  
        \]  
      },  
      "providerMetadata": {  
        "s3TemplateURL": "https://s3.amazonaws.com/amplify-reactamplified-dev-183225-deployment/amplify-cfn-templates/auth/reactamplified4c64a58c4c64a58c-cloudformation-template.json",  
        "logicalId": "authreactamplified4c64a58c4c64a58c"  
      },  
      "lastPushTimeStamp": "2023-03-20T20:32:13.667Z",  
      "output": {  
        "UserPoolId": "us-west-2\_axVszKHhS",  
        "AppClientIDWeb": "5nr9pittlv7o2pcj0eml8254qp",  
        "AppClientID": "3akhtr71tpdct78l0idnrhk81f",  
        "UserPoolArn": "arn:aws:cognito-idp:us-west-2:111111111111:userpool/us-west-2\_axVszKHhS",  
        "UserPoolName": "reactamplified4c64a58c\_userpool\_4c64a58c"  
      },  
      "lastPushDirHash": "+ELQ2dT1KrawBZ30JG8omXtMk/E="  
    }  
  }  
}

23. Find the values shown in the JSON output for the **UserPoolId** and the **AppClientIDWeb**.

The *api-backend-sam/template.yaml* file has place-holders for the *AppClientIDWeb* and the *USERPoolID*. You need to update the values as shown from the output of the *amplify-meta.json* file. (Should be towards the end of the output.)

To accomplish this, you will use a

jq  
command.

**Note:**

jq  
stands for *JASON Query*. It is a lightweight, flexible, and powerful command-line JSON processor. It allows you to filter, transform, and manipulate JSON data in various ways directly from the command line or within shell scripts.

24. **Command:** To create variables to store the values that will be used to update the placeholders for **UserPoolId** and **AppClientIDWeb** in the **api-backend-sam/template.yaml** file, run the following commands:

APP\_CLIENT\_ID\_WEB=$(jq \-r '.auth | .\[keys\[0\]\] | .output.AppClientIDWeb' \~/environment/react-amplified/amplify/backend/amplify-meta.json)

USER\_POOL\_ID=$(jq \-r '.auth | .\[keys\[0\]\] | .output.UserPoolId' \~/environment/react-amplified/amplify/backend/amplify-meta.json)

printf "\\n\\nUserPoolId placeholder value: $USER\_POOL\_ID\\n\\nAppClientIDWeb placeholder value: $APP\_CLIENT\_ID\_WEB\\n\\n"

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

UserPoolId placeholder value: us-west-2\_kEL35ZebC

AppClientIDWeb placeholder value: 7llgrsm9d9vc4p1kpcp93u7nhu

To help automate updating the *template.yaml* file with the variables just created, you use the

sed  
command.

**Note:**

sed  
stands for *stream editor*. It is a command line tool used to perform basic text transformations on an input stream. It is most commonly used to replace placeholders in a file with a new value.

25. **Command:** With the variables set, update the **api-backend-sam/template.yaml** file placeholders with the appropriate values using the following  
25. sed  
     commands:

clear  
before=$(cat \~/environment/api-backend-sam/template.yaml | head \-41 | tail \-7)  
update1=$(sed \-i "s/REPLACE\_WITH\_USERPOOL\_ID/$USER\_POOL\_ID/g" \~/environment/api-backend-sam/template.yaml)  
update2=$(sed \-i "s/REPLACE\_WITH\_APP\_CLIENT\_ID\_WEB/$APP\_CLIENT\_ID\_WEB/g" \~/environment/api-backend-sam/template.yaml)  
after=$(cat \~/environment/api-backend-sam/template.yaml | head \-41 | tail \-7)

printf "template.yaml \--\> code BEFORE update:\\n\\n$before; \\n\\ntemplate.yaml \--\> code AFTER update:\\n\\n $after\\n\\n"

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

template.yaml \--\> code BEFORE update:

        Authorizers:  
          GeneralAuth:  
            IdentitySource: "$request.header.Authorization"  
            JwtConfiguration:  
              issuer: \!Sub "https://cognito-idp.${AWS::Region}.amazonaws.com/REPLACE\_WITH\_USERPOOL\_ID"  
              audience:   
                \- "REPLACE\_WITH\_APP\_CLIENT\_ID\_WEB"; 

template.yaml \--\> code AFTER update:

         Authorizers:  
          GeneralAuth:  
            IdentitySource: "$request.header.Authorization"  
            JwtConfiguration:  
              issuer: \!Sub "https://cognito-idp.${AWS::Region}.amazonaws.com/us-west-2\_g1J6kO5Iu"  
              audience:   
                \- "7uqrunav741v4rja3e63vss28q"

**Note:** These updates are how the application authenticates users.

### **Task 3.2: Deploy the backend resources**

With the backend SAM template updated, it is time to create the deployment package and deploy the backend resources that will be used the the application.

26. **Command:** Build the deployment artifacts for the API using SAM with the following commands:

cd \~/environment/api-backend-sam  
sam build

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Building codeuri: /home/ec2-user/environment/api-backend-sam/add\_image runtime: python3.9 metadata: {} architecture: x86\_64 functions: AddImageFunction  
requirements.txt file not found. Continuing the build without dependencies.  
Running PythonPipBuilder:CopySource  
Building codeuri: /home/ec2-user/environment/api-backend-sam/generate\_grid runtime: python3.9 metadata: {} architecture: x86\_64 functions: GenerateGridFunction  
Running PythonPipBuilder:ResolveDependencies  
Running PythonPipBuilder:CopySource

Build Succeeded

Built Artifacts  : .aws-sam/build  
Built Template   : .aws-sam/build/template.yaml

Commands you can use next  
\=========================  
\[\*\] Validate SAM template: sam validate  
\[\*\] Invoke Function: sam local invoke  
\[\*\] Test Function in the Cloud: sam sync \--stack-name {stack-name} \--watch  
\[\*\] Deploy: sam deploy \--guided

27. **Command:** Now that the deployment package has been created, you deploy the changes to upgrade the API to require authentication with the following command:

sam deploy

**Expected output:** Output has been truncated

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Uploading to first-sam/b9f19ea8c53248d010c396d15857686e  675 / 675  (100.00%)  
Uploading to first-sam/4381ef5609eb70894de1fe227c1cdce8  14396311 / 14396311  (100.00%)

        Deploying with following values  
        \===============================  
        Stack name                   : first-sam  
        Region                       : us-west-2  
        Confirm changeset            : False  
        Disable rollback             : False  
        Deployment s3 bucket         : sam-app-images-us-west-2-0936467  
        Capabilities                 : \["CAPABILITY\_IAM"\]  
        Parameter overrides          : {}  
        Signing Profiles             : {}

Initiating deployment  
\=====================  
Uploading to first-sam/eb390d8c82cdff1605b91e0ff0f72d90.template  3325 / 3325  (100.00%)

Waiting for changeset to be created..  
CloudFormation stack changeset

\----------------------------------------------  
CloudFormation outputs from deployed stack  
\----------------------------------------------  
Outputs                                                                                                                                                                                                                        
\----------------------------------------------  
Key                 Api                                                                                                                                                                                                        
Description         API Gateway endpoint URL                                                                                                                                                                                   
Value               https://aoabc0cq3i.execute-api.us-west-2.amazonaws.com/Prod/                                                                                                                                               
\----------------------------------------------

Successfully created/updated stack \- sam-lab in us-west-2

28. Review the **API Gateway endpoint URL** value. You use this value less the ending **/** (forward slash) to update the **baseUrl** placeholder in the **react-amplified/src/app.js** file in the next task.

### **Task 3.3: Update the React app and test functionality**

To update the React app to know what endpoint to communicate with, you query the **sam-lab** CloudFormation stack, using the

aws cloudformation  
CLI command. It queries the stack for the API Gateway endpoint URL value and stores it in a variable. That variable is then used to update a placeholder for the API endpoint value.

29. **Command:** To set a variable that is used to update the the **baseUrl** placeholder value in the **react-amplified/src/app.js** file, run the following commands:

API\_URL=$(aws cloudformation describe-stacks \--stack-name sam-lab \--query 'Stacks\[0\].Outputs\[?OutputKey==\`Api\`\].OutputValue' \--output text | sed 's/\\/$//'); echo ""; echo "URL \= $API\_URL"; echo ""

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

URL \= https://wugzgju4e5.execute-api.us-west-2.amazonaws.com/Prod

30. **Command:** To replace the **baseUrl** placeholder value with the **Api Gateway endpoint URL**, run the following commands:

clear  
before1=$(cat \~/environment/react-amplified/src/App.js | head \-15 | tail \-2)  
update3=$(sed \-i "s|REPLACE\_ME\_WITH\_THE\_API\_URL|$API\_URL|g" /home/ec2-user/environment/react-amplified/src/App.js)  
after1=$(cat \~/environment/react-amplified/src/App.js | head \-15 | tail \-2)  
printf "App.js \--\> code BEFORE update:\\n\\n$before1\\n\\nApp.js \--\> code AFTER update:\\n\\n$after1\\n\\n"

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

App.js \--\> code BEFORE update:

const baseUrl \= 'REPLACE\_ME\_WITH\_THE\_API\_URL'

App.js \--\> code AFTER update:

const baseUrl \= 'https://vs01rshudi.execute-api.us-west-2.amazonaws.com/Prod'

For React to know what API endpoint to talk to, you had to update the **baseUrl** variable value in the place-holder for **REPLACE\_ME\_WITH\_THE\_API\_URL** section.

31. **Command:** Before updating the Amplify project with these changes, verify what happens if you attempt to **curl** the API with the following commands:

**Note:** As a step in this process, you set the baseUrl variable value to the API Gateway endpoint URL since it doesn’t currently exist. You set the variables and then print their values afterwards to make it cleaner to read. The “-s” in the curl command is used to hide the progress information from the command to clean up the output.

## **Hint**

\# Set variables  
baseUrl=$API\_URL   
uniqueGridId=\`date \+%s\`   
curlOutput=$(curl \-s \-X POST "${baseUrl}/generate\_grid?uniqueGridId=${uniqueGridId}")

\# Print variable values  
echo \-e "\\nbaseUrl: ${API\_URL}\\n"; echo \-e "uniqueGridId: ${uniqueGridId}\\n" ;  echo \-e "Curl command output: ${curlOutput}\\n"

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

baseUrl: https://e1smslsuqd.execute-api.us-west-2.amazonaws.com/Prod

uniqueGridId: 1684769690

Curl command output: {"message":"Unauthorized"}

Now, you need to publish the changes Amplify project to consume these updates.

32. **Command:** To redeploy the Amplify project, run the following commands:

cd \~/environment/react-amplified

amplify publish \--yes

**Expected output:**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\*\*\*\* This is OUTPUT ONLY. \*\*\*\*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

✔ Successfully pulled backend environment dev from the cloud.

    Current Environment: dev  
      
┌──────────┬────────────────────────────────┬───────────┬───────────────────┐  
│ Category │ Resource name                  │ Operation │ Provider plugin   │  
├──────────┼────────────────────────────────┼───────────┼───────────────────┤  
│ Hosting  │ amplifyhosting                 │ No Change │ awscloudformation │  
├──────────┼────────────────────────────────┼───────────┼───────────────────┤  
│ Auth     │ reactamplified3a9d423b3a9d423b │ No Change │ awscloudformation │  
└──────────┴────────────────────────────────┴───────────┴───────────────────┘

No changes detected

? Do you still want to publish the frontend? Yes

Publish started for amplifyhosting

\> react-amplified@0.1.0 build  
\> react-scripts build

Creating an optimized production build...  
Compiled with warnings.

\[eslint\]   
src/App.js  
  Line 19:20:  'setUniqueId' is assigned a value but never used  no-unused-vars

Search for the keywords to learn more about each warning.  
To ignore, add // eslint-disable-next-line to the line before.

File sizes after gzip:

  251.18 kB (+174 B)  build/static/js/main.6887d31d.js  
  33.44 kB            build/static/css/main.a3e3b07c.css  
  1.79 kB             build/static/js/787.cbb326c1.chunk.js

The project was built assuming it is hosted at /.  
You can control this with the homepage field in your package.json.

The build folder is ready to be deployed.  
You may serve it with a static server:

  npm install \-g serve  
  serve \-s build

Find out more about deployment here:

  https://cra.link/deployment

✔ Zipping artifacts completed.  
✔ Deployment complete\!  
https://dev.d2mn8e6o5x1t2o.amplifyapp.com

**Note:** With this update, you are publishing the Cognito configuration, which is now part of the frontend application, and the update to the **baseUrl** variable value in the Amplify project so that it knows the API Gateway endpoint to communicate with.

33. Open the application by opening the **URL** from the output in a new browser tab.

34. Choose the **Create Account** link.

35. **Command:** Enter an **email address**, that you have online access to, as well as a **password** and choose **Create Account** .

**Expected output:**

**We Emailed You**

Your code is on the way. To log in, enter the code we emailed to ***@***. It may take a minute to arrive?

36. Enter the **confirmation code** sent to your email in the **Confirmation Code** input field and choose **Confirm** .

The browser opens the application allowing you to upload images to generate a grid from.

**Note:** You can choose your own image files or download the following images to upload. The only constraint is that the images must be in any of the following formats:

* filename.jpg  
* filename.jpeg

## **Images you can download:**

37. From the **Drag and drop images below field** choose **Upload**.

38. Select as many images as you want.

39. Once the images show as being uploaded, choose **Generate Grid** and a grid image based on all of the images you selected with be shown.

**Task complete:** You have created a frontend for the application that requires authentication for all access to the frontend and to the APIs in the backend using Amazon Cognito.

---

## **Conclusion**

You have completed the following:

* Installed requirements to use AWS Amplify CLI.  
* Initialized AWS Amplify and deployed a project.  
* Configured Cognito to authenticate with the application.  
* Ran the grid-maker application using authentication to create the grid image.

## **End lab**

Follow these steps to close the console and end your lab.

40. Return to the **AWS Management Console**.

41. At the upper-right corner of the page, choose **AWSLabsUser**, and then choose **Sign out**.

42. Choose **End Lab** and then confirm that you want to end your lab.

## **Additional resources**

* For more information about how to use AWS Lambda, see [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/index.html).

For more information about AWS Training and Certification, see [*https://aws.amazon.com/training/*](https://aws.amazon.com/training/).

*Your feedback is welcome and appreciated.*  
 If you would like to share any feedback, suggestions, or corrections, please provide the details in our [*AWS Training and Certification Contact Form*](https://support.aws.amazon.com/#/contacts/aws-training).

[image1]: <data:image/png;base64,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>