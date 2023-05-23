# WEB STACK IMPLEMENTATION (LEMP STACK)
## LEMP (Linux, Engine X (NGINX), MySQL, PHP)
- We need an AWS account

- launch a new EC2 instance of t2.micro family with Ubuntu Server 22.04 LTS

- Private key (.PEM file) should be saved securely and spin up the instance

- Connecting to EC2 terminal

-Using the terminal on MAC/Linux

-Using Windows Terminal

-We'll be connecting to the EC2 instance using Gitbash terminal installed in my windows system

We'll be needing our saved PEM key file change directory to download folder
to navigate to the download where our PEM key is saved,we use the command first 
`cd ~`

![img 1 nav to download folder](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/c198122e-08c3-4055-b082-15df87460eb4)
then, to this command 
`cd downloads`

![img 2 cd download](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/c82be203-5d52-421a-80d1-3a27a2cb4773)

Run this command to ensure your key is not publicly viewable
`chmod 400 devOpsproject.pem`
![img 3 chmod 400](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/2c201e13-ab9b-4f73-9bd4-b2b8ea9839e1)

I will utilize the ssh protocol to establish a connection between my local terminal and my EC2 server

  `ssh -i "devOpsproject.pem" ubuntu@44.202.245.165`
  ![img 4 connecting to instance  IP ](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/07e61675-09a5-4c49-b29d-9b15a4c4deda)
  
  - Type yes to connect

- Now we are connected to our instance well done 🎉

## Step 1 Installing the Nginx Web Server

- `sudo apt update`
![img 1 installing nginx ws](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/8d2d6b3c-b76a-4146-ad00-8d1ffe6dac58)

`sudo apt install nginx`
When prompted, enter Y to confirm that you want to install Nginx
![img 2 installing nginx ws](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/955ec670-5a9e-4e17-bc14-0d2c02ef8150)

To confirm that nginx has been installed correctly and is functioning as a service on Ubuntu.

Run: `sudo systemctl status nginx`
![img 3 installng nginx active state ](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/fa115ca3-43ac-43e5-8d25-969ff3fae2b6)

If it is green and running, then you did everything correctly

As we know, we have TCP port 22 open by default on our EC2 machine to access it via SSH, so we need to add a rule to EC2 configuration to open inbound connection through port 80: Our server is running and we can access it locally and from the Internet (Source 0.0.0.0/0 means ‘from any IP address’). First, let us try to check how we can access it locally in our Ubuntu shell

Run: `curl http://localhost:80`
![img 4 nginx welcome page](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/a5455054-dd42-41b0-826b-797840654ee1)

Let's test if our Nginx server can respond to requests from the Internet
Open a web browser of your choice and try to access following url http://<EcintancePublic-IP-Address>:80  
<img width="865" alt="image" src="https://github.com/olalekan4450/DevOps-Class-/assets/106252004/02a6f58c-1f5a-4a52-96cb-9de021eb774f">
<img width="914" alt="image" src="https://github.com/olalekan4450/DevOps-Class-/assets/106252004/861786b6-c49f-43fa-a527-0cf5bc03ae3a">
  
  
  
