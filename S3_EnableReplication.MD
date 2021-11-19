- Create an S3 Bucket and Enable Replication
Navigate to S3.
Copy the name of the lab-provided appconfigprod1 bucket.
Click Create bucket.
Set the following values:
Name: Paste the name you copied, but replace appconfigprod1 with appconfigprod2 and add some random characters to the end to ensure it is globally unique.
AWS Region: US West (Oregon) us-west-2
Under Copy settings from existing bucket, click Choose bucket.
Select the appconfigprod1 bucket.
Click Choose bucket.
Leave the rest of the setting as the defaults, and click Create bucket.
Click the appconfigprod1 bucket to open it.
Click the Management tab.
In the Replication rules section, click Create replication rule.
Click Enable Bucket Versioning.
Set the following values:
Replication rule configuration
Replication rule name: CrossRegion
Source bucket
Choose a rule scope: This rule applies to all objects in the bucket
Destination
Bucket name:
Click into the box.
Select the appconfigprod2 bucket.
Click Choose path.
Click Enable bucket versioning.
IAM role
IAM role: Create new role
Click Save.
Test Replication and Observe Results
Click The appconfigprod1 bucket link in the breadcrumb trail navigation at the top of the screen.
Click Upload.
Either drag a file to the window or click Add file to upload a file of your choice.
Click Upload.
Click Buckets in the left-hand menu.
Click the appconfigprod2 bucket to open it.
You should see the file you uploaded to appconfigprod1. If it isn't there yet, refresh and wait a few minutes. Note: To speed the replication you can turn on "predictable replication time" in the Replication rule.
