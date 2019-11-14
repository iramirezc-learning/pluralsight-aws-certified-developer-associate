# AWS Developer: Getting Started - Personal Notes

Personal notes for the course: [AWS Developer: Getting Started](https://app.pluralsight.com/library/courses/aws-developer-getting-started/table-of-contents).

> **Level:** Beginner
>
> **Course Date:** Sep 20th, 2019
>
> **Course Duration:** 4h 6m
>
> **Instructor:** Ryan Lewis

## Course Overview

The course will cover 4 main topics:

* Deploying scalable applications with EC2 and EB
* Storing static content with S3
* Creating reproducible infrastructure with cloud-formation templates
* Using managed databases like RDS and DynamoDB

## Welcome to AWS

The course will focus on how to deploy a demo app `Who loves Pizza` to the cloud.

I should be able to answer the following questions:

* What is AWS (cloud) development?
* What's the Web Console?
* What's an SDK?
* What's the AWS CLI?

I should be able to:

* Create an AWS Account
* Create Access Keys for my account
* Install and configure the AWS CLI

### Developing in the Cloud

Developing in the cloud is very similar to develop in your local:

* HTTP server listens to the same ports
* App will run over some virtual machine / OS / Architecture
* For .NET you need the platform installed
* App will connect to DBs

Differences between local vs cloud development:

* You need to separate responsibilities of your app as services (micro services)
* You make the connection between services by code
* Cloud services will be resilient

### The Web of Amazon Web Services

All services interact with each other mostly with HTTP and ports.

Services will have its own IP address or the ARN (Amazon Resource Name)

### AWS Tooling: Web console

Most of the time I will be interacting with the Web Console (accordingly to the course).

All services have its own dashboard.

### AWS Tooling: CLI

Benefits:

* Great for shell scripting
* Complete support with the Web Console & SDKs
* Interacts with any service

AWS CLI is most used by DevOps.

AWS CLI is your starting point to configure the local environment.

### AWS Tooling: SDKs

SDKs APIs will depend on the programming language used.

SDKs are developed by Amazon Engineers and the community.

### Who Loves Pizza?

Web Application Architecture will consist of:

* An EC2 containing the core code
* An S3 storing all the images & assets
* A DynamoDB to store all the users & toppings collections
* An ElastiCache to store user sessions
* An RDS to store the pizzas

### Installing Node.js

[Download & Install Node.js from official page](https://nodejs.org/en).

After installation check both `node` and `npm` versions:

For node:

```sh
$ node -v
v10.15.3
```

For npm:

```sh
$ npm -v
6.4.1
```

### Installing the AWS CLI

Go to the [AWS CLI page](https://aws.amazon.com/cli/?nc1=h_ls) and follow the instructions. _Note: You may need to restart your computer_.

After installation, check the version:

```sh
$ aws --version
aws-cli/1.11.136 Python/2.7.10 Darwin/18.7.0 botocore/1.6.3
```

### Creating and Initializing an AWS Account

1. Create your AWS account. Open the [AWS Console](https://aws.amazon.com/console/) page and click on "Create new account".
2. Once created your AWS account. Open the [AWS Console](https://aws.amazon.com/console/) one more time and now click on the "Sign in to the Console".
3. Generate an AWS Access Key for the CLI and SDK:
    1. Click on your user name
    2. Select "security credentials"
    3. Click the "continue to security credentials" button
    4. Click on the "Access keys" menu. (It should be empty)
    5. Click the "Create new access key" button
    6. Download the CSV (since you can only view and download the secret once)
    7. Click the "Close" button
4. Configure the CLI with your ACCESS_KEY and SECRET
    1. In the console type `aws configure`
    2. Paste your AWS Secret Key ID
    3. Paste your AWS Secret Access Key
    4. Select a region: `us-east-1`
    5. Select an output format: `json`
5. Test your connection by issuing `aws c2 describe-instances`.

AWS CLI configuration example:

```sh
$ aws configure
AWS Access Key ID [****************DBHV]: <YOUR_ACCESS_KEY_ID>
AWS Secret Access Key [****************5vmH]: <YOUR_SECRET_ACCESS_KEY>
Default region name [us-east-1]:
Default output format [None]: json
$ aws ec2 describe-instances
# you should see something like:
{
  "Reservations": []
}
```

## Sounding the Alarm with IAM and Cloudwatch

I should be able to:

* Monitor the cloud
* Know how to set Alarms & Notifications with Cloudwatch & Simple Notification Service (SNS)
* Use Policies, Users & Groups with IAM

### Cloudwatch Overview

Cloudwatch is a service that can receive notifications (triggers) from other services like DynamoDB, EC2 or Billing.

Cloudwatch can send notifications via SNS as HTTP, SMS messages and email.

Cloudwatch is not limited only for notifications, it can trigger other actions like Auto Scaling by adding an extra EC2 instance if the network traffic increments.

### Simple Notification Service (SNS)

SNS works with "Topics".

SNS is very similar to the Observer Pattern, you publish to a Topic, which has an ARN, and then the subscribers are notified.

_NOTE:_ Topics are related to regions.

How to create an SNS Topic with Email Subscription:

1. In the Web Console, change the Region to: "N. Virginia".
2. Click on "Services".
3. Search for "SNS".
4. In the SNS Dashboard, write the topic name: `admin_email`.
5. Click on the "Next step" button.
6. Click on the "Create topic" button.
7. In the "Subscriptions" panel, click the "Create subscription" button.
8. Select "Email" as `Protocol`.
9. Type your email address as the `Endpoint`.
10. Click on the "Create topic" button.
11. You'll receive an email, confirm the subscription to complete the process.

### Creating a CloudWatch Alarm

 __NOTE: North Virginia is the only region that allows billing alarms__.

How to create a CloudWatch billing alarm:

1. In the Web Console, change the region to: "N. Virginia".
2. Click on your username.
3. Select "My Billing Dashboard".
4. In the left side menu select "Billing preferences".
5. Check the box "Receive Billing Alerts".
6. Click on the "Save preferences" button.
7. Click on "Services" on the menu bar.
8. Search for "CloudWatch"
9. In the CloudWatch dashboard, select "Alarms" from the left menu.
10. Click the button "Create Alarm".
11. In the next screen click the "Select metric" button.
12. Select "Billing".
13. Then select "Total Estimated Charged".
14. Check the "USD" currency.
15. Click on the "Select Metric" button.
16. Scroll down to the "Conditions" section.
17. Configure whatever value you want to be notified.
    * Threshold: Static
    * Whenever Estimated Charge is: Greater
    * Than: 1 USD
18. Click the "Next" button.
19. In the "Notification" section, make sure about:
    * Whenever this alarm state is: in Alarm
    * Select an SNS topic: Existing SNS topic
    * Send a notification to: `admin_email`
20. Click on the "Next" button.
21. Add a name to your alarm: Billing Alarm.
22. Click on the "Next" button.
23. Review the preview and then click on the "Create Alarm" button
24. Back in the CloudWatch Dashboard, refresh until you see a status of "OK"

### Identity & Access Management Overview

IAM allows to create users, groups and permission for those users.

IAM also manages passwords, multi-factor authentication, access keys and SSH keys.

IAM works with **Policies**.

Policies are compound of:

* Permissions
* Resource Permissions
* Service Permissions

Policy groups can be applied:

* particular users.
* multiple users (group) to have specific permissions over a resource.

### Securing Your AWS Account

When you create your AWS account the first time, you are logged in as a **ROOT** user, having full access to all services. This may be dangerous!

You need to make green all the Security Status warnings in the IAM dashboard:

* [x] Delete your root access keys.
* [x] Activate the MFA on your root account.
* [x] Create individual IAM users.
* [x] Use groups to assign permissions.
* [x] Apply an IAM password policy.

#### How to setup MFA (Multi-Factor Authentication) on your Root AWS account:

> Before you continue: Install a MFA app into your smartphone. Okta Verify works like a charm!

1. Click on your user name.
2. Select "My Security Credentials" from the menu.
3. Close the pop-up.
4. Expand the "Multi-Factor authentication (MFA)" section.
5. Click the "Activate MFA" button.
6. Select "virtual" (for smartphone).
7. Click on the "Continue" button.
8. Scan the QR code.
9. Type 2 MFA codes.
10. Click on the "Assign MFA" button.
11. Click on the "Close" button in the modal that appears.
12. Sign out from your AWS account.
13. Try to sign in again using the MFA.

### Understanding Policies

Policies are the way in AWS to give permissions to users.

**By default a user has NO permissions.**

A policy is compound by 3 statements:

1. Effect. Can be either _Allow_ or _Deny_. All permission are denied by default.
2. Action. What kind of operations a user or a group is allowed to.
3. Resource. The ARN that is the target of the policy.

There are 2 types od policies:

1. Amazon Managed Policies
2. Custom Managed Policies

### Configuring Users & Groups

#### How to create a user:

1. Log in to the Web Console as a root.
2. Go to IAM service.
3. Select "Users" from the left side.
4. Click on the "Add user" button.
5. Write a user name.
6. Check the "Programmatic Access"
7. Click on the "Next: Permissions" button.
8. Click on the "Next: Tags" button.
9. Click on the "Next: Review" button.
10. Click on the "Create user" button.
11. Download the CSV.
12. Copy the link where users can log in. (https://479067773742.signin.aws.amazon.com/console) After last step, you can also click on the IAM dashboard and get this same link.
13. Click on the "Close" button.
14. Configure your new Access Keys into the CLI: `aws configure`.
15. Test your credentials: `aws ec2 describe-instances`.

#### How to delete your root access keys:

1. Log in to the Web Console as a root user.
2. Click on your username.
3. Select "My Security Credentials"
4. Close the modal (if appears).
5. Expand the "Access keys" section.
6. Click on the "Delete" link next to the Access keys you wish to delete.
7. Confirm by clicking on the "Yes" button.
8. You'll see a status of "Deleted" for the access keys.
9. You're all set.

#### How to create a group:

1. Log in to the Web Console as a root.
2. Go to IAM service dashboard.
3. Select "Groups" from the left side.
4. Click on the "Create new group" button.
5. Give a name to your group: **admin**
6. Click the "Next step" button.
7. Click the "Next step" button.
8. Click the "Create group" button.

#### How to assign a policy to a group:

1. In the IAM service dashboard.
2. Select "Groups" from the left side.
3. Click on the group you wish to attach a policy to.
4. Click on the "Permission" tab.
5. Click the "Attach Policy" button.
6. Check the policy you want. **Administrator Access** for `admins`.
7. Click on the "Attach Policy" button.
8. You should see the policy attached.

#### How to assign a user to a group:

1. In the IAM service dashboard.
2. Select "Groups" from the left side.
3. Click on the group you wish to attach a policy to.
4. Click on the "Users" tab.
5. Click on the "Add Users to Group" button.
6. Check the users you'd like to add to the group.
7. Click on the "Add users" button.
8. You're all set.

#### How to Create a password policy:

1. In the IAM service dashboard.
2. Select "Account Settings" from the left side.
3. Click on the "Set password policy" button.
4. Select the password policy requirements you wish.
    * Min Length of 6 characters.
    * Allow users to change their own password.
5. Click on the "Save changes" button.

#### How to set a password to a user:

1. In the IAM service dashboard.
2. Select "Users" from the left side.
3. Click on the user name you'd like to set a password.
4. Select the "Security Credentials" tab.
5. Click on the "Manage" link next to "Console password".
6. For the "Console Access" choose "Enable".
7. For the "Set Password" choose "Custom password".
8. Type the password.
9. Click on the "Apply" button.
10. You're all set.

#### How to login as the new user:

1. Using the link generated in the step when creating a user.
2. Enter the username and password.
3. You should have access to the web console.
