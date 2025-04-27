# AWS EBS Snapshot Cleanup - Lambda Function and Cloudwatch
## This project contains an AWS Lambda function written in Python that automatically cleans up old or unused EBS snapshots.


 ## Overview
### This Lambda function:

 - Lists all EBS snapshots owned by your AWS account

 - Checks if each snapshot is attached to an existing volume

 - Deletes snapshots that:

 - Are not associated with any volume

 - Are associated with a volume that no longer exists

 - Are associated with a volume not attached to any running EC2 instance

 - The function helps you reduce unnecessary storage costs by cleaning up unused snapshots.

## How it Works
 - Connects to the EC2 service using boto3.

 - Fetches all snapshots owned by your AWS account.

 - Fetches all running EC2 instances.

 - Iterates over each snapshot and:

 - Deletes snapshots that have no volume attached.

 - Deletes snapshots if their volume doesn't exist or is detached.

 ## Deployment Steps
### Create a Lambda function in AWS Console.

   - Copy and paste the Python code (lambda_function.py) into your Lambda function.

### Assign an IAM role to your Lambda with the following permissions:

````
ec2:DescribeSnapshots

ec2:DeleteSnapshot

ec2:DescribeInstances

ec2:DescribeVolumes
````
- (Optional) Set up a trigger using CloudWatch (EventBridge):

- Create a rule to run the Lambda on a schedule (e.g., daily).

### Scheduling with CloudWatch
 - You can use Amazon EventBridge (formerly CloudWatch Events) to trigger this Lambda function automatically:

 - Go to EventBridge → Rules → Create rule

 - Set a Schedule (e.g., rate(1 day) or cron(0 2 * * ? *))

 - Set your Lambda function as the Target

This allows automated daily or weekly snapshot cleanup!

![Screenshot 2025-04-25 125349](https://github.com/user-attachments/assets/0aebbb8a-63e5-4b1d-bd1b-3e2537e54732)







           
