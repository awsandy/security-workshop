# Security Workshop - Part 1

## Login with Event Engine

* Visit the URL dashboard.eventengine.run 
  * Enter your HASH
  * Click "Open AWS Console"


## Setup GuardDuty AWS Config & SecurityHub
   
* Visit Services -> GuardDuty 
  * Click "Get Started" 
  * Click "Enable Guard Duty"

* Visit Services -> config
  * Click "Get Started"
  * Click "Next"
  * Click "Next"
  * Click "Configure"

* Visit Services -> IAM
  * Click "Access analyzer"   (on the left)
  * Click "Create analyzer"
  * Click "Create analyzer"

* Visit Services -> Security Hub
  * Click "Go to Security Hub"
  * Click "Enable Security Hub"

--- 

## Run the following Cloud Formation

* Open a new tab in your browser and use this link (cut n paste)

https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new?stackName=GuardDuty-Hands-On&templateURL=https://sa-security-specialist-workshops-us-west-2.s3-us-west-2.amazonaws.com/guardduty-hands-on/amazon-guard-duty-revamped-v1.yml

* Click "Next"
* Enter youremail@your.domain
* Click "Next"
* Click "Next"
* Click "I acknowledge that AWS CloudFormation might create IAM resources with custom names."
* Click "Create Stack"

### This stack creates:

* Three Amazon EC2 Instances (and supporting network infrastructure)
  * Two Instances that contain the name “Compromised Instance”
  * One instance that contains the name “Malicious Instance”
* AWS IAM Role For EC2 which will have permissions to SSM Parameter Store and DynamoDB
* One Amazon SNS Topic so you will be able to receive notifications
* Three AWS CloudWatch Event rules for triggering the appropriate notification or remediation
* Two AWS Lambda functions that will be used for remediating findings and will have permissions to modify Security Groups and revoke active IAM Role sessions (on only the IAM Role associated with this scenario)
* AWS Systems Manager Parameter Store value for storing a fake database password.
  

## Accept the SNS email

* Look in your email for the AWS Notifications email 
  * Use the "confirm subscription" link within to accept the SNS subscription.

**Wait 5 Minutes for the stack to create**

Back in the AWS console Check progress by looking in 

* CloudFormation -> Stacks ->  GuardDuty-Hands-On

---
 
## Setup Amazon Inspector Agent using Systems Manager

In the console navigate to:

* Services -> Systems Manager
  * Click "Managed Instances" - look for "Scenario 3"
  * Click "Actions" select "Run Command"
  * In the search box Search enter "AmazonInsp"
  * Select "AmazonInspector-ManageAWSAgent"
  * Scroll down and Click "Choose Instances Manually"
  * Select the "GuardDuty-Example: Compromised * Instance: Scenario 3" Instance
  * scroll down and unselect "Enable writing to an S3 bucket"
  * Click "RUN"

Should see the command "In-progress" 

Wait 30 seconds and refresh your browser

Should see the command "Success" 

## Initiate an Inspector Scan

* Visit Services -> Inspector
* Click "Get Started"
* Click "Run Once"

**If you see an error about a role not being created - wait a few seconds and then** 

* Click "Run Once" Again

* On the left click "Assesment templates" 
* Select the template "Assessment-Template-Default-All-Rules"
* Click "Run"


* On the left click "Assesment runs" 
  
You should see a run with status "Collecting Data" 

Next proceed to the Guard Duty Lab

---

# Security Workshop - Part 2

## Perform the main GuardDuty Lab

https://hands-on-guardduty.awssecworkshops.com/

**once this lab is completed return here**

---

# Security Workshop - Part 3

## Extra Activities

What are the Inspector Findings ?
- Inspector showing a lot of CVE's ?
- CIS Hardening Issues ?
- Other findings ?

Walk Through Security Hub 
* What is it telling you 
* What will it tell you 


Watch the AWS Demo

---

## References

https://github.com/aws-samples/amazon-guardduty-hands-on/

