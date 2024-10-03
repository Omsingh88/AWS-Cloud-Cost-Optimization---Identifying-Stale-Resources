# AWS Cloud Cost Optimization - Identifying Stale EBS Snapshots

## Project Description
This project is aimed at helping AWS users optimize their storage costs by automatically identifying and deleting stale EBS snapshots. A stale EBS snapshot is one that is no longer associated with any active EC2 instance or is linked to a volume that does not exist. By cleaning up these unused snapshots, you can reduce unnecessary storage costs.

## Features
- **Automated Snapshot Cleanup**: The Lambda function checks for snapshots that are not associated with any active EC2 instances and deletes them.
- **Volume Association Verification**: Ensures that only snapshots from non-existent volumes or unassociated volumes are deleted.
- **Cost Optimization**: Reduces AWS EBS storage costs by eliminating unused snapshots.

## Architecture and Workflow
The solution utilizes the following AWS services:
- **AWS Lambda**: The core logic is implemented in a Lambda function, which can be executed manually.
- **Amazon EC2**: To identify active instances and their associated volumes.
- **IAM**: Permissions required to read EBS snapshot and EC2 instance information and delete EBS snapshots.

## Implementation Details
The Lambda function performs the following operations:

1. **Retrieve All EBS Snapshots**:
   It uses the `describe_snapshots` method to get a list of all snapshots owned by the account.

2. **Get Active EC2 Instances**:
   It retrieves all active EC2 instances (in the 'running' state) to compare which snapshots are associated with these instances.

3. **Check for Stale Snapshots**:
   It iterates through each snapshot and verifies:
   - If the snapshot has no associated volume, it deletes it.
   - If the associated volume exists but is not linked to any active EC2 instance, it deletes the snapshot.

4. **Delete Stale Snapshots**:
   If a snapshot meets the criteria of being stale, it deletes the snapshot using the `delete_snapshot` method.

## Benefits
- **Reduced Costs**: Automatically removes unused snapshots to save on storage costs.
- **Improved Efficiency**: Automates the cleanup process, reducing the time required for manual maintenance.
- **Simple Setup**: Easy-to-implement solution with minimal configuration required.

## Setup Guide

### 1. Create an IAM Role
1. Navigate to the IAM console and create a new role.
2. Attach the `AWSLambdaBasicExecutionRole` policy.
3. Attach a custom policy with the following permissions:
   - `ec2:DescribeSnapshots`
   - `ec2:DescribeInstances`
   - `ec2:DescribeVolumes`
   - `ec2:DeleteSnapshot`

### 2. Create a Lambda Function
1. Go to the Lambda console and create a new function.
2. Upload the script file (e.g., `lambda_function.py`) containing the code logic.
3. Assign the IAM role created in step 1 to this Lambda function.
4. Execute the function manually from the Lambda console to perform the snapshot cleanup.

## Screenshots
Here are a few screenshots demonstrating the project setup and execution:

![Lambda Function Execution](screenshots/lambda-execution.png)
*Lambda function executing to identify and delete stale EBS snapshots.*

![EBS Snapshot Cleanup Results](screenshots/cleanup-results.png)
*Results of the snapshot cleanup operation.*

## Future Enhancements
- **CloudWatch Integration**: Set up a CloudWatch Event to trigger the function periodically for automated cleanups.
- **Enhanced Filtering**: Add filters to identify snapshots based on tags, creation date, or size.
- **Multi-Region Support**: Extend the function to run across multiple AWS regions.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
