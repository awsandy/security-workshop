# GuardDuty and supplimental material

Visit dashboard.eventengine.run and enter your HASH
Click "Open AWS Console"


1. Setup GuardDuty, SecurityHub
Visit Services -> GuardDuty and click 
"Get Started" then "Enable Guard Duty"

2. Visit Services -> Security Hub
Click "Go to Security Hub"
Click "Enable Security Hub:


3. Run the following Cloud Formation



#### Run the following Cloud Formation Script
* https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new?stackName=GuardDuty-Hands-On&templateURL=https://sa-security-specialist-workshops-us-west-2.s3-us-west-2.amazonaws.com/guardduty-hands-on/amazon-guard-duty-revamped-v1.yml

Click "Next"
Enter youremail@your.domain
Click "Next"
Click "Next"
Click "I acknowledge that AWS CloudFormation might create IAM resources with custom names."
Click "Create Stack"

Creates:

* Three Amazon EC2 Instances (and supporting network infrastructure)
  * Two Instances that contain the name “Compromised Instance”
  * One instance that contains the name “Malicious Instance”
* AWS IAM Role For EC2 which will have permissions to SSM Parameter Store and DynamoDB
* One Amazon SNS Topic so you will be able to receive notifications
* Three AWS CloudWatch Event rules for triggering the appropriate notification or remediation
* Two AWS Lambda functions that will be used for remediating findings and will have permissions to modify Security Groups and revoke active IAM Role sessions (on only the IAM Role associated with this scenario)
* AWS Systems Manager Parameter Store value for storing a fake database password.
  

**Accept the SNS email**
Look in your email for the AWS Notifcations email and use the "conform subscription" link within to accept the SNS subscription

Wait 5 Minutes for the stack to create
Check progress by looking in 
CloudFormation -> Stacks ->  GuardDuty-Hands-On

## Extra
### System Manager
In the console navigate to:
Services -> Ssystems Manager

Click "Managed Instances" - look for "Scenarion 3"
Click "Actions" select "Run Command"
In the search box Search enter "AmazonInsp"
Select "AmazonInspector-ManageAWSAgent"
Scroll down and Click "Choose Instances Manually"
Select the "GuardDuty-Example: Compromised Instance: Scenario 3" Instance
scroll down and unselect "Enable writing to an S3 bucket"
Click "RUN"

Should see the command "In-progress" 
Wait 30 seconds and refresh brwoser
Should see the command "Success" 


1. Visit Services -> Inspector
   Click "Get Started"
   Click "Run Once"

If you see an error about a role not being created 

Click "Run Once" Again

On the left click "Assesment templates" 
Select the template "Assessment-Template-Default-All-Rules"
Click "Run"


On the left click "Assesment runs" should see a run with status "Collecting Data" 

Next proceed to the Guard Duty Lab

## Guard Duty Lab

https://hands-on-guardduty.awssecworkshops.com/


## Extra Activities

What are Inspectors Findings ?
- Inspector showing a lot of CVE's ?
- CIS Hardening Issues ?
- 

Remediate patches:

Run Command
AWS-RunShell
yum -y update

Walk Through Security Hub


AWS Demo






## References

https://github.com/aws-samples/amazon-guardduty-hands-on/

