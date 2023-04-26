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
 URL: `http://<Public-IP-Address>:80`

![installing apache2 1f ](https://user-images.githubusercontent.com/106252004/233038311-adbc1437-4e89-4130-86a8-3a8d13811fcc.jpg)
looks like this:

![installing apache2 1g web page ](https://user-images.githubusercontent.com/106252004/233038923-171661dd-6b8b-451f-83d5-a31d9bee4b00.jpg)
It works



