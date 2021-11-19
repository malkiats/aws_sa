![image](https://user-images.githubusercontent.com/43002915/142621746-5b4f813c-732f-4e29-86a5-84838bbe6bdd.png)

# Create a Public Bucket  
1.	Navigate to S3 using the Services menu or the unified search bar.  
2.	Click Create bucket.  
3.	Set the following values:  
•	Bucket name: acg-testlab-<random>-public, where <random> is a random string of characters to make the bucket name globally unique (e.g., acg-testlab-4324yr-public)  
•	Region: US East (N. Virginia) us-east-1  
4.	In the Bucket settings for Block Public Access section, make sure the box is checked for Block all public access (we'll update this setting later).
5.	In the Tags section, click Add tag and set the following values:  
•	Key: CreatedBy  
•	Value - optional: YOUR NAME  
6.	Leave the rest of the settings as their defaults.
7.	Click Create bucket.  
  
# Create a Private Bucket  
1.	From the S3 Buckets screen, click Create bucket.
2.	Set the following values:  
•	Bucket name: acg-testlab-<random>-private, where <random> is a random string of characters to make the bucket name globally unique (you can use the same string from your public bucket, e.g., acg-testlab-4324yr-private)  
•	Region: US East (N. Virginia) us-east-1  
3.	In the Bucket settings for Block Public Access section, make sure the box is checked for Block all public access (we'll update this setting later).
4.	In the Tags section, click Add tag and set the following values:  
•	Key: CreatedBy  
•	Value - optional: YOUR NAME  
5.	Leave the rest of the settings as their defaults.
6.	Click Create bucket.  
  
# Enable Public Access to the Public Bucket  
1.	From the S3 Buckets screen, select the public bucket name to open it.
2.	Select the Permissions tab.
3.	In the Block public access (bucket settings) section, click Edit.
4.	Uncheck the Block all public access checkbox.
5.	Click Save changes.
6.	In the dialog box that pops up, enter "confirm" in the text field and click Confirm. You should now see the bucket's access states that Objects can be public.
7.	Click Amazon S3 in the breadcrumbs at the top of the screen to return to your S3 buckets. Your public bucket now has public access enabled, while your private bucket does not.

# Upload a File in the Public Bucket    
1.	From the S3 Buckets screen, select the public bucket name to open it.
2.	Ensure the Objects tab is selected, and click Upload.
3.	Click Add files.
4.	Navigate to the files you downloaded for the lab and upload the pinehead.jpg image.
5.	Leave the rest of the settings on the page as their defaults.
6.	Click Upload.
7.	After the file uploads successfully, you're taken to a screen showing your bucket's contents. Select the pinehead.jpg image name to view its details.
8.	In the Object overview section, click on the Object URL. You should receive an error message because although the bucket is public, the object is not.
9.	To make the object public, go back to the image details.
10.	Select the Object actions dropdown and click Make public.
11.	On the Make public screen, click Make public.
12.	Select the Source URL to return to your public S3 bucket, then select the pinehead.jpg image name to view its details.
13.	In the Object overview section, click on the Object URL. You should now see the image.  
  
# Upload a File in the Private Bucket  
1.	Navigate back to your S3 buckets.
2.	Select the private bucket name to open it.
3.	Ensure the Objects tab is selected, and click Upload.
4.	Click Add files.
5.	Navigate to the files you downloaded for the lab and upload the pineheadv2.jpg image.
6.	Leave the rest of the settings on the page as their defaults.
7.	Click Upload.
8.	After the file uploads successfully, select the Destination URL to return to your S3 private bucket.
9.	Select the pineheadv2.jpg image name to view its details.
10.	In the Object overview section, click on the Object URL. You should receive an error message because the object is not public.
11.	To make the object public, go back to the image details.
12.	Select the Object actions dropdown and click Make public.
13.	On the Make public screen, click Make public. This time, you should receive an error message because you don't have sufficient permissions to make this object public. To make the object public, you must first enable public access to the private bucket. You can do this by following the same steps you took to enable public access on your public bucket.  
Enable Versioning on the Public Bucket and Validate Access to Different Versions of Files with the Same Name  
Enable Versioning  
1.	Navigate back to your S3 buckets.
2.	From the S3 Buckets screen, select the public bucket name to open it.
3.	Select the Properties tab.
4.	In the Bucket Versioning section, click Edit.
5.	Click Enable to enable bucket versioning.
6.	Click Save changes.  
  
# Upload Another Image to Test Versioning  
1.	Select the Objects tab.
2.	Click Upload, then click Add files.
3.	Rename pineheadv2.jpg to pinehead.jpg (this way, you'll upload a different image than the original pinehead.jpg image).
4.	Upload the newly renamed pinehead.jpg image.
5.	Click Upload.
6.	After the file is successfully uploaded, select the Destination URL to return to your public bucket.
7.	In the Objects section, toggle Show versions on. You should now see two versions of the pinehead.jpg image listed.  
  
# View the Image Versions
1.	Select the original version of the pinehead.jpg image.
2.	Click on the Object URL for the image. You should see the original image you uploaded earlier.
3.	Go back to your public bucket and select the newly uploaded version of the pinehead.jpb image.
4.	Click on the Object URL for the image. This time, you should receive an error message because the object is not currently public.
5.	To make the new image version public, go back to the image details.
6.	Select the Object actions dropdown and click Make public.
7.	On the Make public screen, click Make public.
8.	Go back to your public bucket and select the newly uploaded version of the pinehead.jpg image again.  
Note: You may need to toggle Show versions on again.  
9.	Click the Object URL for the image again. This time, you should see a new image, which confirms versioning is working as expected.

