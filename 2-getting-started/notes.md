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
