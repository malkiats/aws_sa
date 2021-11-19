Create an S3 Bucket and Enable Replication
1.	Navigate to S3.
2.	Copy the name of the lab-provided appconfigprod1 bucket.
3.	Click Create bucket.
4.	Set the following values:
•	Name: Paste the name you copied, but replace appconfigprod1 with appconfigprod2 and add some random characters to the end to ensure it is globally unique.
•	AWS Region: US West (Oregon) us-west-2
5.	Under Copy settings from existing bucket, click Choose bucket.
6.	Select the appconfigprod1 bucket.
7.	Click Choose bucket.
8.	Leave the rest of the setting as the defaults, and click Create bucket.
9.	Click the appconfigprod1 bucket to open it.
10.	Click the Management tab.
11.	In the Replication rules section, click Create replication rule.
12.	Click Enable Bucket Versioning.
13.	Set the following values:
•	Replication rule configuration
•	Replication rule name: CrossRegion
•	Source bucket
•	Choose a rule scope: This rule applies to all objects in the bucket
•	Destination
•	Bucket name:
1.	Click into the box.
2.	Select the appconfigprod2 bucket.
3.	Click Choose path.
4.	Click Enable bucket versioning.
•	IAM role
•	IAM role: Create new role
14.	Click Save.
Test Replication and Observe Results
1.	Click The appconfigprod1 bucket link in the breadcrumb trail navigation at the top of the screen.
2.	Click Upload.
3.	Either drag a file to the window or click Add file to upload a file of your choice.
4.	Click Upload.
5.	Click Buckets in the left-hand menu.
6.	Click the appconfigprod2 bucket to open it.
•	You should see the file you uploaded to appconfigprod1. If it isn't there yet, refresh and wait a few minutes. Note: To speed the replication you can turn on "predictable replication time" in the Replication rule.
