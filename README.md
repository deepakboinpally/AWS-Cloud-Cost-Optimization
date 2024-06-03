# AWS-Cloud-Cost-Optimization
here's a project outline for an AWS Lambda function to optimize EC2 costs by starting and stopping instances using Boto3 and CloudWatch Events:

1.Create IAM Role:
   Create an IAM role with the necessary permissions for Lambda to start and stop EC2 instances. The permissions should include `ec2:StartInstances` and `ec2:StopInstances`.
   
2. Create Lambda Function:
   - Go to the Lambda console in the AWS Management Console.
   - Click "Create function" and choose "Author from scratch".
   - Configure the function:
     - Name: `EC2Cost-Optimization-Function`
     - Runtime: Python 3.x
     - Role: Choose the IAM role created in step 1.
   - Click "Create function".

3. Write Lambda Function Code:
   Below is a sample Lambda function code using Boto3 to start and stop EC2 instances based on CloudWatch Events:
```python
import boto3
region = 'us-east-2'
instances = ['i-0aba442f31f0542d8', 'i-04076b60cb210a876','i-0b072fa71d7298996']
ec2 = boto3.client('ec2', region_name=region)

def lambda_handler(event, context):
    ec2.start_instances(InstanceIds=instances)
    ec2.stop_instances(InstanceIds=instances)

```
4. Create CloudWatch Rule:
   - Go to the CloudWatch console in the AWS Management Console.
   - Click "Create rule" under Events -> Rules.
   - Choose "Schedule" as the event source and configure the schedule as required (e.g., every day at a specific time).
   - Add a target, select "Lambda function", and choose the Lambda function created in step 2.
   - Configure the input to pass the action (`start` or `stop`) and instance IDs to the Lambda function.

5. Testing:
   - Test the Lambda function manually by triggering it with sample events to ensure it starts and stops EC2 instances correctly.
   - Verify that CloudWatch Events trigger the Lambda function based on the schedule.

6. Optimization:
   - Fine-tune the schedule in the CloudWatch Rule based on usage patterns to optimize cost savings.
   - Monitor EC2 usage and adjust the Lambda function logic or schedule as needed for better optimization.

This project provides a basic framework for cost optimization of EC2 instances using AWS Lambda, Boto3, and CloudWatch Events. You can further enhance it by adding error handling, logging, and additional functionality as per your requirements.
