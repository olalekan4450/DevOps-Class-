# WEB STACK IMPLEMENTATION FOR LAMP STACK

## LAMP (Linux, Apache, MySQL, PHP or Python, or Perl)

### Setting up our AWS instance

-We require an AWS account
-Initiate the creation of a new EC2 instance from the t2.micro family, running Ubuntu Server 20.04 LTS
-Ensure that the private key (.PEM file) is saved securely before starting the instance

![0](https://user-images.githubusercontent.com/106252004/233028963-b5661a2e-8cf8-4927-abff-0f11b3b0c52e.jpg)

-Connecting to EC2 terminal

  - Using the terminal on MAC/Linux
  - Using Windows Terminal
  - We'll be connecting to the EC2 instance using Gitbash terminal installed in my windows system
-We will need the PEM key file that we have saved. Navigate to the download folder in the terminal

![1](https://user-images.githubusercontent.com/106252004/233030455-2735a9bc-6749-42d0-80bc-67d9738abcfa.jpg)

- We need to run this command to ensure our key is not publicly viewable.
`chmod 400 <your-PEM-file-name>.pem`

![2](https://user-images.githubusercontent.com/106252004/233030993-e8902f9d-d82a-4235-811c-3448bf617d96.jpg)

-I'll be utilizing the SSH protocol to establish a connection between my local terminal and the EC2 server
`ssh -i <private-key-name>. pem ubuntu@<Public-IP-address>`

![3](https://user-images.githubusercontent.com/106252004/233032213-6684b8bf-e718-4edf-82cf-df4541f88d96.jpg)
  
-Type yes to connect
-Now we are connected to our instance well done.

![4](https://user-images.githubusercontent.com/106252004/233032712-bb51dd8c-eb78-4969-935a-cfa88e4645a3.jpg)
  
- We have successfully created our first Linux server in the cloud, and our current setup looks like this: (we are the client)
![5](https://user-images.githubusercontent.com/106252004/233033157-6fabe537-fa61-4ef2-b003-9d8dc89247fa.jpg)

  ## STEP 1
### Installing Apache and updating the firewall
  
- Update the list of software packages in the package manager:

`sudo apt update`

- Run apache2 package installation:

`sudo apt install apache2`

To confirm if apache2 is running as a service in our operating system, execute the following command.:

`sudo systemctl status apache2`

If the status of apache2 is displayed as "green" and it is running, then we have successfully completed all the necessary steps. Congratulations! We have successfully launched our first web server in the cloud!

![Creating a virtual host 4g](https://user-images.githubusercontent.com/106252004/233035495-7aa05552-9b5c-40f3-8452-04658346d6ff.jpg)
Now, let's verify if our server is running and accessible both locally and from the internet. To check the local access in Ubuntu shell, we can run the following command:
`curl http://localhost:80`

<img width="709" alt="image" src="https://user-images.githubusercontent.com/106252004/233037085-1f4e6340-15ae-41e9-acd3-2576475553b2.png">
It's now time to test the responsiveness of our Apache HTTP server to requests from the internet. We need to open a web browser and attempt to access the following 
 URL:http://<Public-IP-Address>:80

![installing apache2 1f ](https://user-images.githubusercontent.com/106252004/233038311-adbc1437-4e89-4130-86a8-3a8d13811fcc.jpg)
looks like this:

![installing apache2 1g web page ](https://user-images.githubusercontent.com/106252004/233038923-171661dd-6b8b-451f-83d5-a31d9bee4b00.jpg)
It works
  
  ## STEP 2
### Installing MYSQL
  
- Use ‘apt’ to acquire and install this software

- sudo apt install mysql-server

When prompted, confirm installation by typing Y, and then ENTER.

- When the installation is finished, log in to the MySQL console by typing: sudo mysql
  
  ![installing mysql 2a ](https://user-images.githubusercontent.com/106252004/234592921-57a969f2-dbe1-4e32-b9f9-b1ace39f2256.jpg)
  
![Installing mysql 2b](https://user-images.githubusercontent.com/106252004/234593543-e46583ce-77ed-4c42-9bf9-3b07a4043a98.jpg)
  
  - It is advisable to execute a security script that is pre-installed with MySQL. This script will eliminate insecure default settings and secure access to our database system. Prior to running the script, we will need to set a password for the root user, using 'mysql_native_password' as the default authentication method. The password for this user will be defined as 'PassWord.1'. `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`
  
  ![installing mysql 2c](https://user-images.githubusercontent.com/106252004/234593874-8e196e53-976b-41c0-96d8-2b04254ace3e.jpg)
  
 - Exit the MySQL shell with:
`mysql> exit`
  
  ![installing mysql 2d](https://user-images.githubusercontent.com/106252004/234594505-fd0a63be-fb60-407d-bbac-8c48ef08f4f0.jpg)
  
  - Start the interactive script by running sudo mysql_secure_installation

Answer Y for yes, or anything else to continue without enabling.
![installing mysql 2e](https://user-images.githubusercontent.com/106252004/234595125-eafe6104-f70b-47f2-af16-5d9e1a1e948e.jpg)
  
 Press y|Y for Yes, any other key for No:
![installing mysql 2f](https://user-images.githubusercontent.com/106252004/234595710-a5e4417a-5044-413e-aa94-f773b27033c9.jpg)

- If we choose to answer "yes" to the script, we will be prompted to select a level of password validation. It's important to note that if we input '2' for the strongest level, we may encounter errors while setting passwords that do not meet the criteria of including numbers, uppercase and lowercase letters, special characters, or are based on common dictionary words. For example, "PassWord.1" would meet the criteria for this level of password validation
  
![installing mysql 2g mysql console login page ](https://user-images.githubusercontent.com/106252004/234596737-458b906b-5138-4f61-8434-0793b6252ba7.jpg)
  
 - Exit the MySQL shell with:
`mysql> exit`

Your MySQL server is now installed and secured. Next, we will install PHP, the final component in the LAMP stack.
  
  ## STEP 3 INSTALLING PHP
  
We have Apache installed to serve our content, MySQL installed to store and manage our data, and PHP as the component that will process code to display dynamic content to the end user. To complete the setup, we will need to install the following packages:

php-mysql: This is a PHP module that allows PHP to communicate with MySQL-based databases. libapache2-mod-php: This package enables Apache to handle PHP files. When we install the php package, the necessary core PHP packages will be automatically installed as dependencies.

- To install all three packages - php, php-mysql, and libapache2-mod-php - simultaneously, we can run the following command:
  
     `sudo apt install php libapache2-mod-php php-mysql`
  ![installing PHP 3a](https://user-images.githubusercontent.com/106252004/234598804-ce1b0be4-95cc-4d18-baa4-6e4c18c72f97.jpg)
![installing PHP 3b](https://user-images.githubusercontent.com/106252004/234599868-869d1256-194d-4843-b398-8668c092c44f.jpg)
  
- After the installation is completed, we can use the following command to verify our PHP version:
`php -v`
 ![installing PHP 3c](https://user-images.githubusercontent.com/106252004/234600058-db78b604-0077-4f8c-b01a-bcf251cb3c1b.jpg)
  
  At this point, our LAMP stack is completely installed and fully operational.

- Linux (Ubuntu)

- Apache HTTP Server

- MySQL

- PHP
  
  # STEP 4 CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE
- Create the directory for projectlamp using ‘mkdir’ command as follows:
`sudo mkdir /var/www/projectlamp`
  ![Creating a virtual host 4a](https://user-images.githubusercontent.com/106252004/234608562-09e5323e-3c2c-4713-b9c4-656ac72d018c.jpg)

- Next, assign ownership of the directory with our current system user: 
`sudo chown -R $USER:$USER /var/www/projectlamp`
  
  ![Creating a virtual host 4b ](https://user-images.githubusercontent.com/106252004/234608833-c035143c-f769-4d07-9965-f694b609b3a0.jpg)
  
- Then, create and open a new configuration file in Apache’s sites-available directory using your preferred command-line editor.
`sudo nano /etc/apache2/sites-available/projectlamp.conf`
  

This will create a new blank file. Paste in the following configuration text:

<VirtualHost *:80>

ServerName projectlamp

ServerAlias www.projectlamp

ServerAdmin webmaster@localhost

DocumentRoot /var/www/projectlamp

ErrorLog ${APACHE_LOG_DIR}/error.log

CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
- right click and paste

 ![creating a virtual host 4c](https://user-images.githubusercontent.com/106252004/234609368-64ee9ef8-3e8e-40f9-be63-fa8483ac592f.jpg)
  
  - press ctrl + x to exit
  ![230796546-156020fb-5b46-4660-a969-4aaa0be9e482](https://user-images.githubusercontent.com/106252004/234615514-62374afd-6387-4eb8-9598-6a8333620240.png)
  
  - Type Yes and Enter
  - Please press the 'ENTER' key to execute the command.
  ![230796582-4ada17de-f669-4a89-a412-0efd0c5c83ba](https://user-images.githubusercontent.com/106252004/234616311-ed599a42-98c2-447e-8d2c-1fb0910a477a.png)
  
  We can utilize the 'ls' command to display the new file in the 'sites-available' directory.

`sudo ls /etc/apache2/sites-available`

You will see something like this;

 ![creating a virtual host 4d](https://user-images.githubusercontent.com/106252004/234617371-d17b3f2c-ffc3-446e-b8d3-87e67b65b446.jpg)
  
  We can now enable the new virtual host using the 'a2ensite' command.

`sudo a2ensite projectlamp`

If we are not using a custom domain name and want to disable Apache's default website to prevent it from overriding our virtual host configuration, we can use the 
  
a2dissite' command. Enter the following command:

`sudo a2dissite 000-default`

To ensure that our configuration file does not contain any syntax errors, we can run the following command:

`sudo apache2ctl configtest`
  
![creating a virtual host 4e](https://user-images.githubusercontent.com/106252004/234618469-a6a25070-f399-45f7-a64d-5ee5c4c1c058.jpg)

  Finally, reload Apache so these changes take effect:
 `sudo systemctl reload apache2`
  
![Creating a virtual host 4g](https://user-images.githubusercontent.com/106252004/234623972-d125d276-999d-4219-b430-4944ebfbc862.jpg)
  
- Our new website is now active, but the web root /var/www/projectlamp is still empty. Lets create an index.html file in that location so that we can test that the virtual host works as expected:
sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html

- Now let's go to our browser and try to open our website URL using IP address:

`http://<EC2-Public-IP-Address>:80`
  
  ![creating a virtual host 4h website url ](https://user-images.githubusercontent.com/106252004/235129737-e1fbdf8b-5472-497d-b4c1-e3854d8f9c52.jpg)
  
  - We can also access our website in our browser by public DNS name, not only by IP. Let us try it out, the result must be the same (port is optional)

`http://<Public-DNS-Name>:80`
  
 ![creating a virtual host 4i DNS ](https://user-images.githubusercontent.com/106252004/235132932-9648b5ad-7bdb-47bb-88c3-d6ce49b0b803.jpg)
  
 - Let's keep the 'index.html' file as a temporary landing page for our application until we set up an 'index.php' file to replace it. Once we configure the 'index.php' file, we will remove or rename the 'index.html' file from our document root, as it would take precedence over an 'index.php' file by default.
  
 ## STEP 5 ENABLE PHP ON THE WEBSITE
  
### In case we want to change the default behavior of Apache where 'index.html' takes precedence over 'index.php' file, we can edit the '/etc/apache2/mods-enabled/dir.conf' file and modify the order of listing within the 'DirectoryIndex' directive to prioritize 'index.php' file.
sudo nano /etc/apache2/mods-enabled/dir.conf

- clear everythng and paste this in:
<IfModule mod_dir.c>

#Change this:

#DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm

#To this:

DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm

</IfModule>
  
- press ctrl + x to exit
- Type Yes and Enter
![Enable PHP on the website 5a](https://user-images.githubusercontent.com/106252004/235134090-82056bfb-e1c8-46c5-83f5-f35dd5307103.jpg)
  
- press Enter

- After saving and closing the file, you will need to reload Apache so the changes take effect:

`sudo systemctl reload apache2`

- Create a new file named index.php inside your custom web root folder:
`nano /var/www/projectlamp/index.php`

- This will open a blank file. Add the following text, which is valid PHP code, inside the file:

  <?php

phpinfo();

![enable PHP on the website 5b ](https://user-images.githubusercontent.com/106252004/235140217-b2ba1212-6778-4529-b507-488a7da01b49.jpg)

save and close the file, refresh the page and you will see a page similar to this

![Enable PHP on the website 5c PHP web page ](https://user-images.githubusercontent.com/106252004/235141327-72a5e91c-f123-4305-9c5a-3888a35535df.jpg)

  
