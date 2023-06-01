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
- If you see the above page, then your web server is now correctly installed and accessible through your firewall.
  
  ## STEP 2 INSTALLING MYSQL
- To acquire and install this software:
`sudo apt install mysql-server` when promted type yes
  ![1 instaling Mysql](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/fc96882e-c7ee-49a5-a7d0-79af22b903dc)

- When the installation is finished, log in to the MySQL console by typing:
`sudo mysql`
  ![2 installing mysql](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/5bac07a3-565b-4ca4-95a7-f9f5b2dd8317)
 
  - Before running the script, you will set a password for the root user, using mysql_native_password as default authentication method. We’re defining this user’s password as PassWord.1 ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
Exit the MySQL shell with:

`mysql> exit`

Start the interactive script by running:

`sudo mysql_secure_installation`
![3 installing mysql](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/0c4cdf47-09b3-4e63-a16c-a725d378fa56)

This will ask if you want to configure the VALIDATE PASSWORD PLUGIN.

Answer Y for yes, or anything else to continue without enabling.
  
![2 installing mysql](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/8262f270-58b4-4c9e-90c6-d212cc88fa9a)
  
  Let's test if we are able to log in to the MySQL console by typing: sudo mysql -p Notice the -p flag in this command, which will prompt you for the password used after changing the root user password.

Exit the MySQL console, type: mysql> exit Notice that you need to provide a password to connect as the root user.

## STEP 3 INSTALLING PHP
- To process PHP requests, it's necessary to set up php-fpm, an acronym for "PHP fastCGI process manager", and configure Nginx to route them to this program. Moreover, you'll require php-mysql, a PHP extension that facilitates communication with databases based on MySQL. The fundamental PHP packages will be automatically installed as dependencies.

- To install these 2 packages at once, run:

`sudo apt install php-fpm php-mysql`
  ![Installing PHP ](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/6a0a648f-b718-4b30-8580-8bb4cd90944d)

When prompted, type Y and press ENTER to confirm installation. You now have your PHP components installed. Next, you will configure Nginx to use them.

 ## STEP 4 CONFIGURING NGINX TO USE PHP PROCESSOR
Nginx web server allows us to create server blocks that act like virtual hosts in Apache, enabling us to compartmentalize configuration details and support multiple domains on a single server. To illustrate this concept, we will use the domain name "project LEMP" in this guide.

Create the root web directory for your domain as follows: `sudo mkdir /var/www/projectLEMP`

Let's assign ownership of the directory with the $USER environment variable, which will reference your current system user: `sudo chown -R $USER:$USER /var/www/projectLEMP`

Then, open a new configuration file in Nginx’s sites-available directory using your preferred command-line editor. Here, we’ll use nano: `sudo nano /etc/nginx/sites-available/projectLEMP`

paste this:

#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }

}
  
When you’re done editing, save and close the file. If you’re using nano, you can do so by typing: CTRL+X and then y and ENTER to confirm.

- Activate your configuration by linking to the config file from Nginx’s sites-enabled directory:
sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/

This will tell Nginx to use the configuration next time it is reloaded. You can test your configuration for syntax errors by typing:

`sudo nginx -t`

You shall see following message:
![config Nginx to use PHP process  testing nginx syntax ](https://github.com/olalekan4450/DevOps-Class-/assets/106252004/38a36cf5-6e82-4cf0-b257-73e29d2361c0)

  - If you receive any error messages, you should revisit your configuration file and check its contents before proceeding further. In addition, you must deactivate the default Nginx host that is presently set to use port 80. To accomplish this, execute the following command:
`sudo unlink /etc/nginx/sites-enabled/default`

- Let's reload Nginx to apply the changes:
`sudo systemctl reload nginx`

- The website is up and running now, but the web root directory located at /var/www/projectLEMP is still empty. To ensure that your new server block is functioning correctly, We will create an index.html file in that directory using the following command:
`sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html`

Now go to your browser and try to open your website URL using IP address: `http://<EcintancePublic-IP-Address>:80`
 
  
  
