# AWS Cloud Cost Optimization - Identifying Stale EBS Snapshots

## Project Description
This project is aimed at helping AWS users optimize their storage costs by automatically identifying and deleting stale EBS snapshots. A stale EBS snapshot is one that is no longer associated with any active EC2 instance or is linked to a volume that does not exist. By cleaning up these unused snapshots, you can reduce unnecessary storage costs.

## Problem :
Sometimes, developers create EC2 instances with volumes attached to them by default. For backup purposes, these developers also create snapshots. However, when they no longer need the EC2 instance and decide to terminate it, they sometimes forget to delete the snapshots created for backup. As a result, they continue to incur costs for these unused snapshots, even though they are not actively using them.

## Solution :
We're using AWS to save money on storage costs. We made a Smart Lambda function that looks at our snapshots and our EC2 instances. If Lambda finds a snapshot that isn't connected to any active EC2 instances, it deletes it to save us money. This helps us keep our AWS costs down.

## Note :
There are many similar problems like this. For instance, we might attach an Elastic IP to our EC2 instance but forget to delete the Elastic IP after terminating the EC2 instance. In such a case, the Elastic IP continues to incur costs for us.

## Steps :
### Step 1:
1. Go into your AWS Console.<br>
2. Navigate to the EC2 Console.<br>
3. In the Instances section, select 'Instances,' and then click on 'Launch Instance'.<br>

![Architecture](screenshot/1.png)

4. Next, navigate to the 'Elastic Block Store' section and select 'Volumes'.<br>

![Volume](screenshot/2.png)

5. You will notice that a default volume has already been created for us.<br>
6. Next, click on 'Snapshots,' and then click the 'Create Snapshot' button. It will prompt you with a page that looks like this.<br>

![Volume](screenshot/3.png)

7. In Volume ID section choose your default Volume ID created when we create instance.<br>
8. Next, click 'Next,' provide a name for your Snapshot, and then scroll down and click 'Create Snapshot'.<br>

### Step 2 :
1. After creating a Snapshot, navigate to the Lambda Console..<br>
2. You will see some options in the user interface, such as 'Create Function'.<br>
3. Click on 'Functions'.<br>

![Volume](screenshot/4.png)

4. Select 'Author from Scratch,' then enter the Function name, and choose the latest Python version.<br>
5. Scroll down and click 'Create Function'.<br>
6.After creating the function, scroll down, and you will see something like the image below..<br>

![Lambda](screenshot/5.png)

