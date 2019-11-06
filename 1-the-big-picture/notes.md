# AWS Developer: The Big Picture - Personal Notes

Personal notes for the course: [AWS Developer: The Big Picture](https://app.pluralsight.com/library/courses/aws-developer-big-picture/table-of-contents).

> **Level:** Beginner
>
> **Course Date:** Oct 9, 2019
>
> **Course Duration:** 1h 34m
>
> **Instructor:** Ryan Lewis

## Course Overview

The course will cover 3 main topics:

* Core services of AWS
* Extended services
* Different ways to access AWS

## Whats is AWS?

I should be able to answer the following questions:

* What is the "Cloud"?
* How AWS works?
* Why and when to use AWS?
* AWS vs Azure vs Google Cloud?

Objectives of the course:

* Understand the core services of AWS
  * EC2 - Elastic Cloud Compute
  * S3 - Simple Storage Service
  * RDS - Relational Database Service
  * Route53 - Router to handle domain names.
* Enhancing your App with AWS services
  * EB - Elastic Beanstalk (Containers)
  * Lambda (Serverless)
  * DynamoDB (No-SQL DB)
  * VPC - Virtual Private Cloud (Secure Services)
  * CloudFront (CDN)
  * CloudWatch (logs)
* Harnessing the power of AWS:
  * Web Console
  * Command Line Interface
  * SDK - Software Development Kit

### The Web Application Conundrum

In the past web applications used to run on Prem servers (physical machines) but over time this solution was not scalable due to the multiple users that grow over time. Then, people started to pay for hosting, where your web app is contained in a virtual machine inside a server sharing resources. Cloud computing aims to solve different problems like: scalability, performance and pricing. You only pay what you use. It's a good solution for start ups and large companies.

### Hello Amazon Web Services

AWS is a collection of cloud services that provide solutions to different problems.

Not only web applications can be deploy to AWS.

AWS is an excellent alternative to scale your application.

### Tracing the Global Infrastructure

AWS has different data centers around the globe that provides less latency to your web app and fault tolerance.

Every region has different zones, to provide redundancy.

[AWS Services Health Dashboard](http://status.aws.amazon.com)

AWS provides stability.

### How Does AWS Work?

AWS basically works the same way it works in your local machine. When you work with your application you may need to use different protocols and ports to communicate among services or computers. On AWS that works basically the same but every service has it's own IP address that work into a Virtual Private Cloud. The only thing that will require extra configuration is the Security Groups, in which you define what application has access to what resource.

Recommended course: [Amazon Web Services (AWS) Fundamentals for System Administrators](https://app.pluralsight.com/library/courses/aws-system-admin-fundamentals/table-of-contents).

### AWS vs. the rest

Other competitors:

* Microsoft Azure
  * Run Microsoft products
* Google Cloud
  * Big Data, Kubernetes, AI
* Heroku
  * Perfect choice for hobby web apps
  * Simpler to deploy
  * Does not have all services that AWS
  * Limited regions

## Understanding the Core Services of AWS

I should be able to answer the following questions:

* What's a EC2?
* What's S3?
* What's RDS?
* What's Route53?

### Elastic Cloud Compute (EC2)

EC2. Is an Elastic Cloud Computer. Elastic means that it can scale as needed (memory, cpu, etc...).

An EC2 instance is basically a virtual machine where you can do whatever you'd like as you would do with any computer.

EC2 instances requires an AMI (Amazon Machine Image) which are basically images that contain an Operating System with a subset of applications pre-installed ready to use (similar to Docker?).

EC2 instances have a *type* (nano, small, medium, large) and a *family* (machine learning, storage, network, ...)

Large instance Type and Families Comparison:

||vCPU|Memory|Network|
|-|-|-|-|
|General Purpose (t3.large)|2|8|Up to 5Gbps|
|Memory Optimized (r5.large)|2|16|Up to 10Gbps|
|Compute Optimized (c5.large)|2|4|Up to 10Gbps|

EC2 instances can replicate depending on the number of instances you define.

EBS means Elastic Block Storage which is basically your hard drive for your EC2 instance.

EC2 instances have Security Groups configurations which are rules that define how your virtual computer interacts with the rest of the world. For instance, you should only allow SSH from a known IP address (yours). With VPC you allow access to other EC2 instances, databases and HTTP incoming requests.

Key-Pair is used to SSH to your EC2.

EC2 instances are charged by hour. Example:

A `t2.micro` instance type running an `Amazon Linux` AMI will charge `$0.013 USD` per hour. Daily rate: `$0.31 USD` equals to `$6.00 MXN` (approximately). See [EC2 Pricing](https://aws.amazon.com/es/ec2/pricing/).

EC2 Instance Pricing Types:

* On-Demand (Cheap)
* Reserved (Cheaper)
* Spot (Cheapest)

### Simple Storage Services (S3)

S3 is a storage service where the maximum object size is up to 5TB!

S3 works with buckets that store objects.

Example of a S3 Bucket URL:

https://s3-us-west-1.amazonaws.com/my.org/img/logo.png

> S3 Buket Region: https://s3-us-west-1.amazonaws.com
>
> Bucket Name: my.org
>
> Object Path: img/logo.png

S3 provides Static Website Hosting to serve static files for your app.

You can use CloudFront to cache content!

S3 charges for the following:

* Amount of data stored
* Total of requests to Objects
* Amount of data transferred

### Relational Database Service (RDS)

NOTE: Prefer a RDS over installing you own database in a EC2

RDS manages database:

* Backups
* Updates
* Infrastructure

RDS supports (different price):

* MySQL
* Postgres
* SQL Server
* MariaDB
* OracleDB
* Amazon Aurora

Alternatives to SQL for NoSQL DBs:
* DynamoDB
* DocumentDB

### Route53

Provides a DNS solution for inside and outside AWS.

It's the core to allow access to your AWS services from the outside world.

Route53 Pricing:

* By Hosted Zone
* By Queries

Provides the Health Check service (expensive per health check).

## Enhancing Your App with AWS Databases and Application Services

I should be able to answer the following questions:

* What's EB?
* What's Lambda?
* What's DynamoDB?
* What's VPC?
* What's CloudWatch?
* What's CloudFront?

### Elastic Beanstalk (EB)

EB is a solution to encapsulate various tasks you'll do manually for EC2 instances.

EB lets you define an **Application** where you can run different versions of your application (code) in different environments (test, development, production).

**Applications** are stored in an S3 bucket.

EB is free*. You only pay for the EC2 instances and the S3 bucket.

### Lambda

A Lambda is code that runs serverless.

Lambda pricing:

* Number of requests
* Running time

Lambda Function structure:

* Code
* Platform Type (Node, Python, ...)
* Configuration
* Triggers

### DynamoDB

DynamoDB manages No-SQL databases.

DynamoDB features:

* Unlimited elastic storage
* No hardware choices

### Virtual Private Cloud

VPC secures EC2 instances.

VPC features:

* Configure VPC routing tables
* Use NAT Gateways for outbound traffic
* Internal IP address allocation

In a VPC you can declare multiple Subnets (private or public) in which you allow internet access or not.

VPC is free.

### CloudWatch

A monitor for other AWS services.

CloudWatch features:

* Monitoring Resources
* Acting on alerts
* Logging
* Archive of logs

CloudWatch pricing:

* By Region
* By Alarms
* By Ingesting Logs
* By Archived Logs
* By Dashboards

### CloudFront

It is a Content Delivery Network (CDN). It structured by _Distributions_. It used to reduce latency.

CloudFront integrates with:

* Route53
* LoadBalancer
* EC2
* S3

CloudWatch pricing:

* By Outgoing Data
* By Region

## Harnessing the Power of AWS from the Command Line to Code

There are three main ways to interact with AWS:

* Web Console (UI)
* Amazon Software Development Kit (SDK)
* Command Line Interface (CLI)

### AWS Web Console

You can navigate through the whole AWS services with this interface.

You can pin your favorite services in the navigation bar.

### AWS SDK

There are SDK for a lot of programing languages.

SDK are code libraries that make much easier to interact with AWS services with code.

You can install the `aws-sdk` into a npm project and start using it.

### AWS CLI

The CLI provides almost all the things that you can do with the UI.

You can create shell scripts to automate tasks.
