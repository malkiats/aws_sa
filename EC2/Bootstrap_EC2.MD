![image](https://user-images.githubusercontent.com/43002915/142751471-47b7c4f6-90fe-4187-9aed-173d0ebdfd51.png)

# Manually Install Software on webserver-01
1.	From the AWS Management Console, navigate to EC2.
2.	In Resources at the top, click Instances (running).
3.	Select the webserver-01 instance and click Connect.
4.	Select EC2 Instance Connect and click Connect to open a terminal window. You may also use your own local terminal if you prefer.

6.	Log in to the server using the credentials provided on the lab page:  
ssh cloud_user@<PUBLIC_IP_ADDRESS>  

6.	Update the packages, using the same password as before when prompted:  
sudo apt-get update  

7.	Install the Apache2 web server:  
sudo apt-get install apache2  

8.	When asked if you want to continue, hit Enter for yes.
9.	Once installed, return to the AWS Management Console.
10.	Navigate back to the EC2 dashboard.
11.	Click Instances (running).
12.	Under Details at the bottom of the page, click open address next to the public IPv4 address to access our Apache web page.  

Note: When opening the page, you may receive an error that this site can't be reached. This is because the link defaults to HTTPS instead of HTTP. In the address URL, change HTTPS to HTTP to load the page.  

13.	Return to the terminal window and install the unzip command:  
sudo apt-get install unzip  

14.	Download the AWS CLI tool:  
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"  

1.	Unzip the file:  
unzip awscliv2.zip  

2.	Install:  
sudo ./aws/install  

3.	Verify that AWS CLI version 2 has been installed:  
/usr/local/bin/aws --version  

4.	To edit our web page's index.html file, we need to grant normal user access to the file:  
sudo chmod 777 /var/www/html/index.html  

5.	To get instance metadata about our server's availability zone, enter the following command:  
curl http://169.254.169.254/latest/meta-data/placement/availability-zone  

** Note:** If you don't get output, wait a moment and retry the command.  

6.	Add availability zone, instance ID, public IP, and local IP instance metadata to our website:  
echo '<html><h1>Bootstrap Demo</h1><h3>Availability Zone: ' > /var/www/html/index.html  
curl http://169.254.169.254/latest/meta-data/placement/availability-zone >> /var/www/html/index.html  
echo '</h3> <h3>Instance Id: ' >> /var/www/html/index.html  
curl http://169.254.169.254/latest/meta-data/instance-id >> /var/www/html/index.html  
echo '</h3> <h3>Public IP: ' >> /var/www/html/index.html  
curl http://169.254.169.254/latest/meta-data/public-ipv4 >> /var/www/html/index.html  
echo '</h3> <h3>Local IP: ' >> /var/www/html/index.html  
curl http://169.254.169.254/latest/meta-data/local-ipv4 >> /var/www/html/index.html  
echo '</h3></html> ' >> /var/www/html/index.html  

16.	Return to our Apache web page and refresh to view the results of the changes we've made.

18.	Return to the terminal and install MySQL using the password from the lab page:  
sudo apt-get install mysql-server  

18.	When asked if you want to continue, hit Enter for yes.  

Note: It may take a few mintues for MySQL to install.  

Use a Bootstrap Script to Build webserver-02 and Debug Issues  

1.	Return to the AWS Management Console and navigate to EC2.
2.	On the EC2 dashboard, click Launch instances.
3.	Scroll down to Ubuntu Server 20.04 LTS and click Select.
4.	Click Next: Configure Instance Details.
5.	In Auto-assign Public IP, click Enable.

7.	Scroll down to User data and paste in the following Bootstrap script:  
#!/bin/bash  
sudo apt-get update -y  
sudo apt-get install apache2 unzip -y  
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"  
unzip awscliv2.zip  
sudo ./aws/install  
echo '<html><h1>Bootstrap Demo</h1><h3>Availability Zone: ' > /var/www/html/index.html  
curl http://169.254.169.254/latest/meta-data/placement/availability-zone >> /var/www/html/index.html  
echo '</h3> <h3>Instance Id: ' >> /var/www/html/index.html  
curl http://169.254.169.254/latest/meta-data/instance-id >> /var/www/html/index.html  
echo '</h3> <h3>Public IP: ' >> /var/www/html/index.html  
curl http://169.254.169.254/latest/meta-data/public-ipv4 >> /var/www/html/index.html  
echo '</h3> <h3>Local IP: ' >> /var/www/html/index.html  
curl http://169.254.169.254/latest/meta-data/local-ipv4 >> /var/www/html/index.html  
echo '</h3></html> ' >> /var/www/html/index.html  
apt-get install mysql-server  

22.	Click Next: Add Storage.
23.	Click Next: Add Tags.
24.	Click Add Tag.
25.	Set the Key to "Name" and the Value to "webserver-02".
26.	Click Next: Configure Security Group.
27.	Click Select an existing security group.
28.	Select the security group that has EC2SecurityGroup available.
29.	Click Review and Launch.
30.	Click Launch.
31.	In the key pair modal, select the first dropdown and click Create a new key pair.
32.	In Key pair name, enter a name of your choice.
33.	Click Download Key Pair.
34.	Click Launch Instances.
35.	At the bottom right, click View Instances.
36.	Once the webserver-02 instance has passed status checks, select the instance and click Connect.
37.	Select EC2 Instance Connect and click Connect to connect to our webserver-02 instance in a new terminal window.
38.	Check that Apache installed correctly:
ps aux |grep apache
The output should display 3 Apache servers running.
39.	Return to the EC2 dashboard.
40.	Under Details at the bottom of the page, click open address next to the public IPv4 address to access our Apache web page.
Note: When opening the page, you may receive an error that this site can't be reached. This is because the link defaults to HTTPS instead of HTTP. In the address URL, change HTTPS to HTTP to load the page.
41.	Return to the terminal window and check that AWS CLI was installed:
aws --version
42.	Check that MySQL installed:
43.	ps aux |grep mysql
44.	sudo service mysql start
sudo service mysqld start
These commands should all return an error that the MySQL service was not found.
45.	To troubleshoot, check the bootstrapping script used when this system was booted:
curl http://169.254.169.254/latest/user-data
46.	At the bottom of the script, notice the following code:
apt-get install mysql-server
Our code is missing the -y command needed for MySQL to automatically install without a user prompt.
Use a Fixed Bootstrap Script to Build webserver-03
1.	Return to the EC2 dashboard and click Launch instances.
2.	Scroll down to Ubuntu Server 20.04 LTS and click Select.
3.	Click Next: Configure Instance Details.
4.	In Auto-assign Public IP, click Enable.
5.	Scroll down to User data and paste in the our Bootstrap script with -y added this time to the final command:
6.	#!/bin/bash
7.	sudo apt-get update -y
8.	sudo apt-get install apache2 unzip -y
9.	curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
10.	unzip awscliv2.zip
11.	sudo ./aws/install
12.	echo '<html><h1>Bootstrap Demo</h1><h3>Availability Zone: ' > /var/www/html/index.html
13.	curl http://169.254.169.254/latest/meta-data/placement/availability-zone >> /var/www/html/index.html
14.	echo '</h3> <h3>Instance Id: ' >> /var/www/html/index.html
15.	curl http://169.254.169.254/latest/meta-data/instance-id >> /var/www/html/index.html
16.	echo '</h3> <h3>Public IP: ' >> /var/www/html/index.html
17.	curl http://169.254.169.254/latest/meta-data/public-ipv4 >> /var/www/html/index.html
18.	echo '</h3> <h3>Local IP: ' >> /var/www/html/index.html
19.	curl http://169.254.169.254/latest/meta-data/local-ipv4 >> /var/www/html/index.html
20.	echo '</h3></html> ' >> /var/www/html/index.html
apt-get install mysql-server -y
21.	Click Next: Add Storage.
22.	Click Next: Add Tags.
23.	Click Add Tag.
24.	Set the Key to "Name" and the Value to "webserver-03".
25.	Click Next: Configure Security Group.
26.	Click Select an existing security group.
27.	Select the security group that has EC2SecurityGroup available.
28.	Click Review and Launch.
29.	Click Launch.
30.	In the key pair modal, select the first dropdown and click Choose an existing key pair.
31.	Select the key pair from our previous instance and click Launch Instances.
32.	At the bottom right, click View Instances.
33.	Once the webserver-03 instance has passed status checks, select the instance and click Connect.
34.	Select EC2 Instance Connect and click Connect to connect to our webserver-03 instance in a new terminal window.
35.	Check that Apache installed correctly:
ps aux |grep apache
The output should display 3 Apache servers running.
36.	Return to the EC2 dashboard.
37.	Under Details at the bottom of the page, click open address next to the public IPv4 address to access our Apache web page.
Note: When opening the page, you may receive an error that this site can't be reached. This is because the link defaults to HTTPS instead of HTTP. In the address URL, change HTTPS to HTTP to load the page.
38.	Return to the terminal window and check that AWS CLI was installed:
aws --version
39.	Check that MySQL installed:
ps aux |grep mysql
MySQL should be running successfully this time.

