Probelm Statement:
Unmanaged Elastic Block Store (EBS) snapshots often accumulate over time. These snapshots incur ongoing storage costs, especially in large-scale environments or older accounts where manual cleanup is often overlooked. This leads to unnecessary storage expenditure, which can rapidly increase total cloud bills.

Solution:
Created a Lambda function that fetches all EBS snapshots owned by the same account ('self') and also retrieves a list of active EC2 instances (running and stopped). For each snapshot, it checks if the associated volume (if exists) is not associated with any active instance. If it finds a stale snapshot, it deletes it, effectively optimizing storage costs.

Implementation:
If you want to replicate this solution in your own AWS environment follow these steps:
1. Create an IAM Policy that grants ec2:DescribeSnapshots and ec2:DeleteSnapshot permissions. This ensures the Lambda function can only perform the necessary tasks.
2. Create Lambda and upload this code to a new AWS Lambda function.
3. Navigate to Amazon CloudWatch Events
4. Create a new Rule with a Schedule expression
5. Set the target of this rule to be the AWS Lambda function created in Step 4.

This setup ensures that the script runs automatically on your chosen schedule, providing continuous cost optimization without manual intervention.






