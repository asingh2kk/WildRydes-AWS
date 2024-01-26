# Wild Rydes AWS Amplify Setup

## Module 1: Initial Setup and AWS Amplify Configuration

This module guides you through configuring AWS Amplify to host the static resources for your web application with continuous deployment. The Amplify Console provides a git-based workflow, making deployment and hosting seamless. In subsequent modules, dynamic functionality will be added using JavaScript to call remote RESTful APIs built with AWS Lambda and Amazon API Gateway.

### Architecture Overview

The architecture is straightforward. AWS Amplify Console manages all static web content, and end-users access the site using the public URL provided by Amplify. No web servers are required.

### AWS Regions

This web application can be deployed in any AWS Region supporting services like AWS Amplify, AWS CodeCommit, Amazon Cognito, AWS Lambda, Amazon API Gateway, and Amazon DynamoDB. Refer to the [AWS Regional Services List](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) to find supported Regions.

## Setting Up Code Repository

### Step 1: Create CodeCommit Repository

1. Open the AWS CodeCommit console.
2. Choose Create Repository.
3. Enter `wildrydes-site` for the Repository name.
4. Choose Create.

### Step 2: Set Up IAM User and Git Credentials

- Set up an IAM user with Git credentials following instructions in the [AWS CodeCommit User Guide](https://docs.aws.amazon.com/codecommit/latest/userguide/setting-up-gc.html).

### Step 3: Configure AWS CLI

- If AWS CLI is not installed, install it using terminal commands specific to your OS.
- Enter `aws configure` in the terminal, providing Access Key ID, Secret Access Key, and Region.

### Step 4: Set Up Git Config

- For Linux, macOS, or UNIX machines, see Step 3 instructions for [Linux, macOS, or UNIX](https://docs.aws.amazon.com/codecommit/latest/userguide/setting-up-https-unixes.html).
- For Windows machines, see Step 3 instructions for [Windows](https://docs.aws.amazon.com/codecommit/latest/userguide/setting-up-https-windows.html).

### Step 5: Clone CodeCommit Repository

- Navigate to the AWS CodeCommit console.
- Select the `wildrydes-site` repository.
- Select Clone HTTPS from the Clone URL dropdown to copy the HTTPS URL.
- Run `git clone` in the terminal using the copied URL.

### Step 6: Copy Website Content

- Change directory into your repository (`wildrydes-site`).
- Copy static files from S3 bucket:
    ```bash
    aws s3 cp s3://wildrydes-us-east-1/WebApplication/1_StaticWebHosting/website ./ --recursive
    ```
- Add, commit, and push git files.

### Step 7: Launch AWS Amplify Console

- Launch the AWS Amplify console. 
- Choose Get Started. 
- Under the Amplify Hosting Host your web app header, choose Get Started. 
- On the Get started with Amplify Hosting page, select AWS CodeCommit and choose Continue.
- On the Add repository branch step, select wildrydes-site from the Select a repository dropdown.
- If you used GitHub, you'll need to authorize AWS Amplify to your GitHub account.
- In the Branch dropdown select master and choose Next. 

## Module 2: User Registration and Sign-In

### Overview
In this module, you will integrate Amazon Cognito User Pools to manage user accounts on your WildRydes website. Users will register, confirm their email, and sign in to access the site. This README provides step-by-step instructions for the setup and usage of the authentication system.

### Prerequisites
- AWS account with appropriate permissions.
- Git installed on your local machine.

### Setup Instructions

1. **Clone the repository to your local machine:**

    ```bash
    $ git clone <repository-url>
    $ cd wildryde-site
    ```

2. **Module 1: Initial Setup**
   - Follow the steps outlined in the "Module 1 - Initial Setup" section.

3. **Module 2: User Registration and Sign-In**
   - Perform the steps mentioned in the "Module 2 - User Registration and Sign-In" section.

4. **API Configuration:**
   - Save the authentication token generated after successful sign-in.

5. **Notes:**
   - Ensure email verification for real email addresses.
   - Verify SES settings for email delivery.
   - Update Cognito details in `config.js`.

6. **Deployment:**
   - Commit and push the changes to your Git repository.

    ```bash
    $ git add .
    $ git commit -m "module_2_changes"
    $ git push
    ```

7. **Testing:**
   - Open your deployed website and test user registration, confirmation, and sign-in.

### Troubleshooting
- Check the Cognito console for user details and confirmations.
- Verify email delivery settings in the SES console.

### Next Steps
Proceed to Module 3 for integrating the Amazon Cognito user pool authorizer with the RESTful API using Amazon API Gateway.

## Module 3: API Gateway Integration

### Overview
In this module, you will integrate Amazon API Gateway with AWS Lambda and Amazon DynamoDB to create a RESTful API for your web application. The API will enable the frontend application to communicate with the backend Lambda function, allowing users to request unicorns. The Lambda function processes these requests, records them in DynamoDB, and responds with details about the dispatched unicorn.

### Prerequisites
- Completed Module 2: Amazon Cognito User Pool Integration.
- AWS account with appropriate permissions.
- Git installed on your local machine.

### Setup Instructions

1. **Clone the repository to your local machine:**

    ```bash
    $ git clone <repository-url>
    $ cd wildryde-site
    ```

2. **Module 3: API Gateway Integration**
   - Follow the steps outlined in the "Module 3 - API Gateway Integration" section.

3. **Testing:**
   - Test the integration by making requests to the API Gateway endpoint.

4. **Deployment:**
   - Commit and push the changes to your Git repository.

    ```bash
    $ git add .
    $ git commit -m "module_3_changes"
    $ git push
    ```

5. **Notes:**
   - Ensure all IAM roles and permissions are correctly configured.
   - Verify API Gateway settings for integration with Lambda.

6. **Next Steps:**
   Proceed to Module 4 for securing your API using Amazon Cognito User Pool Authorizer.

### Module 3 - API Gateway Integration

1. **Create API Gateway:**
   - Use the Amazon API Gateway console to create a new API.
   - Configure the API to use a RESTful structure.

2. **Create Resource and Method:**
   - Add a resource and create a POST method for the `/ride` endpoint.
   - Configure the method to invoke the `RequestUnicorn` Lambda function.

3. **Deploy API:**
   - Deploy the API to a stage.

4. **Test Integration:**
   - Test the integration by making a POST request to the `/ride` endpoint using the provided test event.

5. **Update Frontend:**
   - Update the frontend application to use the API Gateway endpoint for requesting unicorns.

6. **Troubleshooting:**
   - Check API Gateway logs for any issues during integration.

### Important Notes
- This README assumes that you have successfully completed Module 2.
- Follow each step carefully to ensure proper API Gateway integration.
- Ensure the Lambda function and DynamoDB table are correctly configured.
- Test the API thoroughly before moving to the next module.

**End of Module 3 README**

## Module 4: API Security with Cognito User Pool Authorizer

### Overview
In this module, you will enhance the security of your RESTful API by adding an Amazon Cognito User Pool Authorizer. This authorizer will validate and authorize API requests using JSON web tokens (JWT) issued by the Cognito User Pool. By implementing this authorizer, you ensure that only authenticated and authorized users can access the API.

### Prerequisites
- Completed Module 3: API Gateway Integration.
- Configured Amazon API Gateway with a deployed stage.

### Setup Instructions

1. **Clone the repository to your local machine:**

    ```bash
    $ git clone <repository-url>
    $ cd wildryde-site
    ```

2. **Module 4: API Security with Cognito User Pool Authorizer**
   - Follow the steps outlined in the "Module 4 - API Security with Cognito User Pool Authorizer" section.

3. **Testing:**
   - Test the secured API by making requests with valid and invalid tokens.

4. **Deployment:**
   - Commit and push the changes to your Git repository.

    ```bash
    $ git add .
    $ git commit -m "module_4_changes"
    $ git push
    ```

5. **Notes:**
   - Ensure the Cognito User Pool Authorizer is correctly configured.
   - Verify API Gateway settings for the Authorizer.

6. **Next Steps:**
   Proceed to Module 5 for building the final part of your web application.

### Module 4 - API Security with Cognito User Pool Authorizer

1. **Create Cognito User Pool Authorizer:**
   - Use the Amazon API Gateway console to create a new Cognito User Pool Authorizer.
   - Configure the authorizer to use the Cognito User Pool created in Module 2.

2. **Configure API Gateway:**
   - Update the API Gateway settings to include the Cognito User Pool Authorizer.
   - Ensure that only authenticated users can access the `/ride` endpoint.

3. **Test Authorization:**
   - Test the API by making requests with valid and invalid authorization tokens.
   - Ensure that unauthorized users are denied access.

4. **Deployment:**
   - Deploy the updated API to the existing stage.

### Important Notes
- This README assumes that you have successfully completed Module 3.
- Follow each step carefully to ensure proper API security configuration.
- Test the API thoroughly to confirm that only authenticated users can access the `/ride` endpoint.

**End of Module 4 README**

## Module 5: Resource Cleanup

### Overview
In this final module, you will learn how to properly clean up and delete the resources created throughout the tutorial. It is essential to delete unused resources to avoid incurring unnecessary charges.

## Resource Cleanup Steps

### 1. Delete AWS Amplify App:
   - In the AWS Amplify console, select the "wildrydes-site" app created in Module 1.
   - Choose "Actions" and select "Delete app."
   - Confirm the deletion by entering "delete" and choose "Delete."

### 2. Delete Amazon Cognito User Pool:
   - In the Amazon Cognito console, select your WildRydes User Pool.
   - Choose "Delete user pool."
   - Select the checkbox to deactivate deletion protection, enter "WildRydes" to confirm, and choose "Delete."

### 3. Delete AWS Lambda Function:
   - In the AWS Lambda console, navigate to the "Functions" page.
   - Select the "RequestUnicorn" function created in Module 3.
   - From the "Actions" drop-down, choose "Delete function."

### 4. Delete IAM Role:
   - In the IAM console, select "Roles" from the left navigation pane.
   - Enter "WildRydesLambda" into the filter box.
   - Select the checkbox next to the role, "WildRydesLambda," and choose "Delete."
   - Confirm deletion by entering "WildRydesLambda" and choose "Delete."

### 5. Delete DynamoDB Table:
   - In the Amazon DynamoDB console, select "Tables" from the left navigation pane.
   - Select the checkbox next to the "Rides" table created in Module 3.
   - Choose "Delete."
   - Select the checkbox next to "Delete all CloudWatch alarms for Rides," enter "confirm," and choose "Delete."

### 6. Delete REST API:
   - In the Amazon API Gateway console, select the "WildRydes" API created in Module 4.
   - In the "Actions" dropdown, choose "Delete."
   - Confirm deletion by choosing "Delete" on the confirmation screen.

### 7. Delete CloudWatch Logs:
   - In the Amazon CloudWatch console, expand "Logs" in the left navigation pane and select "Log groups."
   - Select the checkbox next to the "/aws/lambda/RequestUnicorn" log group.
   - Choose "Delete log group(s)" from the "Actions" dropdown.
   - Confirm deletion.

### 8. Repeat Cleanup for CloudFormation Stacks (if applicable):
   - If you launched any CloudFormation stacks, repeat steps 2-7 for any log groups associated with custom resources in those stacks.

### 9. Final Confirmation:
   - Double-check that all resources have been successfully deleted by verifying their absence in their respective AWS service consoles.

## Important Notes
- Ensure you follow these cleanup steps to avoid incurring additional charges.
- Confirm the deletion of each resource to prevent any unintended consequences.
- Take note of any CloudFormation stacks or additional resources launched during the tutorial and ensure their cleanup.

**End of Module 5 README**
