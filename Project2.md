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

  
  
  