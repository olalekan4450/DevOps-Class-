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
sudo apt install php libapache2-mod-php php-mysql
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
 

  
  

  

  



