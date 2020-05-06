# GuardDuty and supplimental material
## Setup link (London - because have Detective)


1. Setup GuardDuty, SecurityHub

2. Run Cloud Formation
#### London
* https://console.aws.amazon.com/cloudformation/home?region=eu-west-2#/stacks/new?stackName=GuardDuty-Hands-On&templateURL=https://sa-security-specialist-workshops-us-west-2.s3-us-west-2.amazonaws.com/guardduty-hands-on/amazon-guard-duty-revamped-v1.yml

#### Ireland
* https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new?stackName=GuardDuty-Hands-On&templateURL=https://sa-security-specialist-workshops-us-west-2.s3-us-west-2.amazonaws.com/guardduty-hands-on/amazon-guard-duty-revamped-v1.yml

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

## Extra
### System Manager
Managed Instances - look for "Scenarion 3"
Run Command - Search for "AmazonIns"
Select "AmazonInspector-ManageAWSAgent"
Click "Choose Instances Manually"
Select the "Scenarion 3" Instance
Disable writing to S3 bucket
RUN ("In-progress" - 30 seconds or so)


### Inspector
Assesment Targets - open twisty - Preview Target
    Should see instance "Healthy"
Assesment templates - RUN
Assesment runs - See progress 

## Guard Duty Lab

https://hands-on-guardduty.awssecworkshops.com/

### Scenario 1:
Compromised instance pings malicious instance (simulating outbound egress to known bad host - the malicaious instance)

In GuardDuty: 
EC2:MalliciousIPCaller.Custom

Look at lists - drill though to S3 - quick look to see public IP
Should match the public IP of the Malicious EC2 instance

Note:
GuardDuty uses managed threat intelligence provided by AWS Security and third-party providers, such as ProofPoint and CrowdStike. You can expand the monitoring scope of GuardDuty by configuring it to use your own custom trusted IP lists and threat lists. 

CloudWatch - Events - Rules
Click on the rule named GuardDuty-Event-EC2-MaliciousIPCaller.

Look at Lambda - and logs
Should of put EC2 compromised host 1 into the Forensic SG
Should also get email.

### Scenario 2:

* The malicious instance makes API calls. The EIP on the instance is in a custom threat list. API calls are logged in CloudTrail
* GuardDuty is monitoring the CloudTrail Logs (in addition to VPC Flow Logs and DNS Logs) and analyzing this based on threat list, machine learning, baselines, etc.
* GuardDuty generates a finding and sends this to the GuardDuty console and CloudWatch Events.
* The CloudWatch Event rule triggers an SNS topic.
* SNS sends you an e-mail with the finding information

In GuardDuty look for:  
UnauthorizedAccess:IAMUser/MaliciousIPCaller.Custom

Click on the see resource effected (IAM role) 
Correlate in CloudTrail

### Scenario 3:

Get credentials from SSM scenario 3 
run scripts

In Lambda - look for CloudWatch Log insights (not the graphs)
Click through


## Extra - Inspector showing a lot of CVE's
AWS-RunShell
yum -y update




## References

https://github.com/aws-samples/amazon-guardduty-hands-on/

