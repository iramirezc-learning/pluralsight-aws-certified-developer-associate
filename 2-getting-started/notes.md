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

## Getting Inside the Virtual Machine with EC2 and VPC

### Virtual Private Cloud Overview

The VPC is a free service! With a max of 5 VPC per account.

VPC allows to create a Virtual Network.

Resources have private IP addresses.

VPC works with Security Groups that define allowed incoming/outgoing IP addresses and ports. Like a mini-firewall.

Security Groups are attached to instance level.

Each VPC use a Routing Table to handle traffic to destinations outside the VPC.

Each VPC also use a Network Access Control List to handle allowed IP for incoming/outgoing traffic.

Instances are launched inside Subnets which are contained inside a VPC.

Each subnet has its own Routing Table and Network Access Control List.

Subnets can be configured to be public or private.

### Creating a Virtual Private Cloud

#### How to create a VPC:

1. Make sure you are in the correct Region!
2. Search for the service VPC.
3. In the VPC dashboard click on "Launch VPC Wizard" button.
4. From the left menu, select "VPC with a Single Public Subnet".
5. Click the "Select" button.
6. Give the VPC a name: __pizza-vpc__.
7. Select the first "Availability Zone" you see: __us-east-1a__.
8. Give the Subnet a name: __pizza-subnet-a__.
9. Click "Create VPC".
10. Click "Ok".

#### How to configure VPC Routing table to allow outgoing traffic to reach public Internet:

1. In the VPC dashboard, click on the left menu option "Your VPCs"
2. Select the VPC you wish: __pizza-vpc__.
3. In the details section click on the link next to "Route Table".
4. Click on the Route Table entry.
5. Click on the "Routes" tab.
6. Click "Edit Routes".
7. Then click "Add Route".
8. In the destination type: __0.0.0.0/0__ (meaning anywhere)
9. In the target select: __Internet Gateway__.
10. Select the first listed result: __igw-xxxxxxx__.
11. Click "Save Routes".
12. Click "Close".

#### How to create a subnet for scalability (for auto-scaling groups):

NOTE: A subnet can only be in a single Availability Zone.

1. In the VPC dashboard, click on the left menu option "Subnets".
2. Click "Create subnet".
3. Give it a name in the "Name tag" field: __pizza-subnet-b__.
4. Select the corresponding VPC: __pizza-vpc__.
5. Select a different Availability Zone from the previous subnet: __us-east-1b__.
6. In the IPv4 CIDR block type: __10.0.1.0/24__ (IPs: 10.0.1.1 -> 10.0.1.255).
7. Click "Create"
8. Click "Close"
9. You should see both subnets in the subnets list.

### Elastic Cloud Compute

An EC2 instance is just a virtual machine with:

* Memory
* CPU
* Storage
* Network

EC2 instances can support many OS like Windows or Linux. Note that OS with license cost more.

Amazon Machine Image (AMI) is the operating system installed in a EC2 instance.

The storage for a EC2 instance is managed by an Elastic Block Store (EBS Volume) which is independent.

EBS can be transferred or continue to exist even that an EC2 instances is terminated.

### Creating an EC2 Instance

1. Go to the EC2 service.
2. In the EC2 dashboard, click the "Launch instance" button.
3. Select the "Amazon Linux 2 AMI, SSD Volume Type"
4. Click "Select" next to it.
5. Choose the Instance Type: __t2.micro__ (Free tier eligible).
6. Click "Next: Configure Instance Details" in the bottom right.
7. Type the number of instances: __1__.
8. Select your Network: __pizza-vpc__.
9. Select the Subnet: __pizza-subnet-a__ (can be either one).
10. Click "Next: Add Storage".
11. Leave storage configuration defaults.
12. Click "Next: Add Tags".
13. Add a tag: __Key=Name__, __Value=pizza-app__
14. Click "Next: Configure Security Groups".
15. Choose "Create a new security group".
16. Change the Security Group Name: __pizza-ec2-sg__.
17. Give a description to the Security Group: __Security group for pizza EC2__
18. *Remember to restrict the SSH rule for Production.
19. Add a new rule clicking "Add rule".
20. Select "Custom TCP" from the Type column.
21. Type the "Port" your app will be running on: __3000__
22. Select "Anywhere" from the Source column.
23. Click "Review and Launch".
24. Click "Launch".
25. From the Key Pair modal, select "Create new key pair".
26. Give the keys a name: __pizza-keys__.
27. Click "Download Key Pair" and store the `.pem` file.
28. Click "Launch instances".
29. Click "View instances".
30. You are all set!

### Connecting to an EC2 Instance

NOTE: Even that we have configured the EC2 instance Routing table to allow incoming traffic from the outside world through the port `3000`, there's no way to pass the VPC configuration. So for that, we need to make the proper configuration.

Elastic IPs are public IPs that are associated to EC2 instances.

Elastic IPs are consistent and independent from EC2 instances.

#### How to create and assign a public IP address to the VPC

1. Go to the EC2 dashboard.
2. Select "Elastic IPs" from the left menu under the section "Network & Security"
3. Click "Allocate new address".
4. Choose "Amazon pool".
5. Click "Allocate".
6. Then click "Close".
7. Click the "Actions" button above.
8. Select "Associate address".
9. From the "Instance" dropdown select: __pizza-app__.
10. From the "Private IP" select the only IP available.
11. Click "Associate"
12. Finally, click "Close".
13. You should see the Elastic IP created.
14. Click the link under the "Instance" column.
15. Now you should see that the instance has a public IP address.
16. Copy that IP address so we can use it next.

#### How to connect to the EC2 instance via SSH

1. Change the `chmod` for the `.pem` file to make it readable only for your current user. See example below.
2. SSH to your instance by providing the `.pem` file and the public IP address retrieved from the previous steps.
3. Select `yes` if requested to continue.
4. You should be all set.

Example:

```sh
$ chmod 400 <path-to-pem-file>
# now connect to the EC2 instance by SHH
$ ssh -i <pem-file> ec2-user@<ec2-public-ip>
# Select `yes` if requested to continue
# now you should be connected to your EC2 instance
[ec2-user@ip-x-x-x-x ~]$
```

### Updating and Deploying to an EC2 instance

#### How to Update OS Software and Install Node.js

1. Connect to the EC2 instance via SSH.
2. Update OS software by running: `sudo yum update`.
3. Select `yes` if prompted.
4. Update YUM to download node.js via `curl`. See example below.
5. Then install node.js via YUM.
6. Test node.js version.
7. Test npm version.

Example:

```sh
# inside your EC2 instance shell
$ sudo yum update
# should update OS packages
$ curl -sL https://rpm.nodesource.com/setup_12.x | sudo bash -
# will update YUM with node.js installation files
$ sudo yum install -y nodejs
# will install node.js
$ node -v
# you should see the node version installed
$ npm -v
# you should see the npm version installed
```

#### How to Transfer App Code to the EC2 instance

1. Exit from the EC2 shell if you still login by issuing the `exit` command.
2. Make sure to remove the `node_modules` folder from your local: `rm -rf node_modules`
3. Transfer the source code from your local to the EC2 instance via `scp`.
4. Connect to the EC2 instance via SSH one more time.
5. Enter to the remote source code: `pizza-luvrs`.
6. Install npm dependencies: `npm install`.
7. Run the server: `npm run start`.
8. Open a web browser with the url `<ec2-public-ip>:3000`.
9. You should get the `pizza-luvrs` app up & running!
10. Celebrate your first app deployed to AWS.

Example:

```sh
[ec2-user@ip-x-x-x-x ~]$ exit
# now you should be in your local

# go to the App's folder code and remove node_modules
$ rm -rf node_modules
# go to the parents folder
$ cd ..
# then transfer the files via scp
$ scp -r -i <pem-file> <local_app_code> ec2-user@<ec2-public-ip>:/home/ec2-user/<remote_app_folder>
# this should copy all the source code from your local to the EC2 instance
# once finished, connect to the EC2 via SHH
$ ssh -i <pem-file> ec2-user@<ec2-public-ip>
# enter the source code folder
$ cd pizza-luvrs
# then install npm dependencies
$ npm install
# once finished, run the app
$ npm run start
# you should be all set
```

### Scaling EC2 Instances

When deploying your web applications to the cloud, it is important to NOT rely on a single instance. You need to Scale!

You can create a custom AMI by taking an snapshot to an EC2 instance!!! Which is wonderful!!! You don't need to go to the whole process of updating the SO software, installing node and pushing the code.

Creating a custom AMI manually might not be a good idea, there's where Auto Scaling Groups comes into play.

Auto Scaling Groups can launch a new EC2 instance based on some rules.

Load Balancer will help to over come the issue of having public addresses changing every time a new instance is launched.

A Load Balancer is basically a Router that handles DNS and balances incoming requests to multiple instances.

### Creating an Amazon Machine Image

#### How to create an AMI from an EC2 instance

1. Go to the EC2 dashboard
2. Select "Instances" from the left menu.
3. Select the EC2 instance from where you want to get the AMI.
4. Click the "Actions" button.
5. Select "Image" from the menu and then "Create image".
6. Give the image a name: __pizza-image__.
7. Give the image a description: __pizza app up & running__.
8. Click the button "Create image".
9. Click "Close".
10. Click the "Launch Instance" button to validate that the AMI was created.
11. From the left menu bar, select "My AMIs".
12. You should see the `pizza-image` AMI!
13. *You can also navigate through the EC2 dashboard, by selecting "AMIs" under the section "Images" from the left menu.

### Creating a Load Balancer

#### How to create a Load Balancer

1. From the EC2 dashboard, select "Load Balancer". Either from the left menu under the "Load Balancing" section or from the dashboard "Resources".
2. You should not see any load balancer yet. Click "Create Load Balancer".
3. Create a Load Balancer of Type: "Application Load Balancer (HTTP & HTTPS)".
4. Give it a name: __pizza-loader__.
5. Select `internet-facing` as the "Schema".
6. Select `ipv4` as the "IP address type".
7. Let the Listener use the protocol HTTP and port 80. __NOTE:__ HTTPS can be configured later on port 443.
8. Select the corresponding VPC: `pizza-vpc`.
9. Check at least 2 "Availability Zones": `us-east-1a` and `us-east-1b`.
10. Verify the subnets to be different: `pizza-subnet-a` and `pizza-subnet-b`.
11. Click "Next: Configure Security Settings"
12. A warning message might appear alerting about using a secure listener (HTTPS). Ignore that for a moment and click "Next: Configure Security Groups"
13. Choose "Create a new security group".
14. Give it a name: `pizza-lb-sg`.
15. Give it a description: `Pizza Load Balancer Security Group`.
16. Leave the port for the default "Custom TCP Rule" to be: `80`.
17. Click "Next: Configure Routing".
18. Give it a name: `pizza-tg`.
19. Select `Instance` as "Target type".
20. Change the port to be: `3000`. The port that the app listens too.
21. Leave Protocols and Health checks with the defaults values.
22. Click "Next: Register Tables".
23. You should see nothing in the "Registered targets" section.
24. Select the `pizza-app` instance and click "Add to registered".
25. Click "Next: Review".
26. Click "Create".
27. Click "Close.

#### How to Enable Instance Stickiness on Load Balancer

We need to make ensure that if a user connects to an EC2 instance the subsequent requests are done to the same instance.

1. Select the "Target Groups" under the  "Load Balancing" section in the left menu from the EC2 dashboard.
2. Select the target group fro which you want to enable stickiness: `pizza-tg`.
3. Under the Description Tab, scroll down to "Attributes".
4. Click "Edit Attributes".
5. Check the "Enable" checkbox for Stickiness.
6. Change the duration to be: `1 day`.
7. Click "Save".
8. You are all set!

### Creating an Auto-Scaling Group

#### How to create a Launch Configuration for an Auto-Scaling Group

1. Go to the EC2 dashboard
2. Select "Launch Configurations" from the section "Auto Scaling" at the left menu.
3. Click the "Create launch configuration" button.
4. Select "My AMIs" in the left side menu.
5. Click the button "Select" next to the AMI `pizza-image`.
6. Keep selected the EC2 type `t2.micro`.
7. Click "Next: Configure details".
8. Give it a name: `pizza-launcher`.
9. In the "Advanced Details" section. Type the `#!/bin/bash` script below inside the "User data".
10. Click "Next: Add storage".
11. Leave defaults and click "Next: Configure Security Groups"
12. Choose "Select an existing security group".
13. Select the `pizza-ec2-sg` previously created.
14. Click "Review".
15. Click "Create launch configuration".
16. In the Key Pair modal, keep selected the option "Choose an existing key pair".
17. And verify the `pizza-keys` key pair is selected.
18. Check the "I acknowledge..." checkbox.
19. Click "Create launch configuration".

Script:

```sh
#!/bin/bash
echo "starting pizza-luvrs"
cd /home/ec2-user/pizza-luvrs
npm run start
```

#### How to create an Auto-Scaling Group.

1. From the EC2 dashboard, click "Launch Configuration" from the left side menu under the section "Auto Scaling".
2. Select the `pizza-launcher`.
3. Click the button "Create Auto Scaling group".
4. Give it a "Group name": `pizza-scaler`.
5. Change the "Group size" to: `2`.
6. Select the `pizza-vpc` as "Network".
7. Add both subnets: `pizza-subnet-a` and `pizza-subnet-b`.
8. Expand the "Advance Details" section.
9. Check the box for "Receive traffic from one or more load balancers" next to "Load Balancing".
10. Select the `pizza-tg` as "Target Groups".
11. Click "Next: Configure scaling policies".
12. Click "Next: Configure notifications".
13. Click "Next: Configure tags".
14. Click "Review".
15. Click "Create Auto Scaling Group".
16. Click "Close".
17. Refresh until you see `2` in the "Instances" column.
18. Click on the "Instances" tab and you should see the 2 instances.
19. Select "Target Groups" from the left menu under the "Load Balancing" section.
20. Click the "Targets" tab.
21. You should see the 2 instances running.
22. Go back the the "Load Balancers" dashboard.
23. Copy the "DNS name" under the "Description" tab and paste it in your browser.
24. You should see the Pizza Luvrs App Up & Running!
25. Select "Security Groups" from the left menu.
26. Select the `pizza-ec2-sg`.
27. In the "Detail" section select the "Inbound" tab.
28. Click "Edit".
29. Remove the TCP Rule for IPv6 `::/0`.
30. Change the Source for the TCP Rule IPv4 to be `sg-xxxxx - pizza-lb-sg`.
31. Click "Save".
32. Now your app will only accept connections withing the load balancer and is secured.

### Scaling in Action

### How to Test Scaling

1. From the EC2 dashboard. Select "Auto Scaling Groups" in the left menu.
2. Select the `pizza-scaler`.
3. Click the "Scaling Policies Tab".
4. Click "Add Policy".
5. Click the link "Create a simple scaling policy".
6. Give it a name: `scale up`.
7. Click the link "Create new alarm".
8. Un-check the "Send a notification to:" checkbox.
9. Change "Whenever" to be "Network Out".
10. And change `>=` to be `100000` Bytes (NOTE: this is not realistic, it's just to see the scalability in action).
11. Click "Create Alarm".
12. Click "Close".
13. Change the "Action" to "Add" `1` instances.
14. Click "Create".
15. Repeat from step 3 to step 13. But this time create a policy named `scale down` to "Remove" `1` instance when the "Network Out" is `<=` than `10000` Bytes.
16. Now, select the "Details" tab.
17. Click "Edit".
18. Change the "Max" instances to be: `4`. This is to make room for auto-scaling to add or remove an instance as needed.
19. Click "Save".
20. Now you can stress the web app with `jMeter`, `Apache Benchmark` or by refreshing the web app multiple times disabling the cache. (See command for Apache Benchmark below).
21. Go to the "Activity History" tab and refresh until you see a new Status. (NOTE: this may take up to 5 minutes).
22. You are all set!

Usage of Apache Benchmark:

```sh
$ ab -n 100 -c 5 http://<url-to-load-balancer>
# Benchmarking http://pizza-loader-1114611100.us-east-1.elb.amazonaws.com/...
```
