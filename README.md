## Udacity-Linux-Server-Configuration
## By Parvathi
# About
This is the Udacity project 5 about the Configuring the Linux the server.

# Server Details
Server IP Address 13.127.33.29

Hosted site Url http://13.127.33.29.xip.io/

# How to connect as grader:
save private key provided in your local machine and run the following command

ssh -i path/to/privatekey -p 2200 grader@13.127.33.29
  
# Configuring Linux Server
# Updating all packages

sudo apt-get update
sudo apt-get upgrade
# Creating grader User:

sudo adduser grader
This will add new user

sudo nano /etc/sudoers
Below the Root user append the following line

grader  ALL=(ALL:ALL) ALL
This will grant sudo permission to grader

# Creating a ssh key pair for grader
On your local machine in terminal/command prompt

ssh-keygen
This will generate public and private ssh keys which is saved to .ssh folder

Then in your virtual machine change to newly created user

su - grader
Create a new directory .ssh and new file authorized_keys in that directory

mkdir .ssh
sudo nano .ssh/authorized_keys
Copy the public key with .pub extension to authorized_keys and save the file

chmod 700 .ssh
chmod 644 .ssh/authorized_keys

700 will give read write and execute permission to user.
644 prevent other user from writting in to file. Then restart ssh server
service ssh restart
Now from your log in to grader with private key generated
# ssh key
# id_rsa key:

-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAoH0U98qRouLgQ3XhHuhvIqTn9VN6v6/iFCnqws9c/qQE0e5n
Wmoz04fCllnHHGI8PxmseFnt1DtX1QD7m4mrcGEvtsQLFKcYuC17BNB7BFuN7EfX
6ZgHyiPFaX/N3t5nVJlN9EtKVvNLnMvkhLzWsM/kJ3FeUpYHYXDxVuvZieQ2nVtl
l29pGs6qcN5oeKk7xhz9DNFScVeZtC8/L5dSlgy4FTq0AtPCloJmBo2FmUB8dnwn
y0M6ifarr8jqpjJf1VLm3yR03ws/jdJ7OvB9dWF+lXflnGqcitsCluZDa4PEHnno
XeS+OIiPWPubXcbjnuvU6jBl+mnzI/OkSqeEKwIDAQABAoIBAFWnrKM7yFLpR8x5
g7ddUsNoxCxZa7AXDVC5toRW7Ekz/SaWWS8Wc6a4VJCuRejOPV1oNHbfeGHHcm9K
4P74kTmfhTnElC1nqXfTPk8pfh6rRqoPBhu0eqPWR6yw+42xofCzCboS3RBfNcHv
yH1X1DX2Hs02YqMtU68b+pLrueUvweCuaKxE3JM/rRngrkozKuAGXp9sgI1EJaVf
iBnnY7Fy3gh6xR4ibs7rt2edZrj0rdfKKiD6g8roZG5kUcrZKmp5uhSEawGGve2w
rPqoS5OWgiiL/FT0lwJfKabr2t+WxWxAkWD4MtLcKdqzrcycshtcB3nEm8b3skSK
i1Wgj/ECgYEAy1JgRSVacYCnwyKBVAwgY46dHHfqxcPmodCK0kINFbjkBj1EkD9O
jpyCYg4f8vU9OB2kQkBqLs6KWSkHSq1ujpmhCCensvrrBUw8GIX8CHK25zqbse8B
Wpo1clLy8jnV7yMrQfyf9URC1VqM1N4evqixVANWkcZlomPBYT3VkU8CgYEAyhG7
BJ1AiaR0gqy4Y5Qeeop8kHw6StpnRXzRZYZ6qoYiIEpVzO0FjgSqysGaiZ8GkbvH
rbhd2UPrRBZ6qNzqtxt9m+w8++4nlGg2TF/e8BXt1smMyRfG8IhHNVIBnqlFsQJZ
Gp80RmvikKaFjE+26JwhzbFoY7cLHOqrUTQb0GUCgYArXYR++vqRXtlpO0DORk/a
LB7CZalDSQc12B7jvYbA7VBlLEglY/tDW4pLk6uozDmkcF4Ka2a6WP8VCTUu7lK4
Q3gfHyYbfH0IAjyHFnys6JquMsfmaY2mX2Gq4ppCo6dHe/7L8i/Dxi1jCA8lj8KK
87vuqU+bg+9FdXVXYjLc7QKBgQCS+7i0z4ndVTGmx+pMDLbq3gdjtelU/271Pai3
F83scisqn8evi41p031EhPVbO8C0iwnhFGW3n07ntQ49/IwC600/+OQXQRGrQu6U
OXxZ2Smq/eqZb+E2n3pkj6U7+tcFvbaAxeNpghpIq8gi2u0qYD+6dlx/g+rietRo
+eVtfQKBgBfRl2TUB6ivhinngUShR2UcM3v8+qFOMEBUI9PWpvwKcN7g4s4rr9yl
T3k+WM7yjQP5Ifs51bNLMH0Fej0DHvEFnN0dacsP/8FREusOxyt1qRKZ5yhUKbI9
x2thal1vgR6/etJsX9RVPjAI+i69cFcRieGLBDslZt69/O5GCscl
-----END RSA PRIVATE KEY-----


ssh -i .ssh/id_rsa grader@13.127.33.29
Changing the ssh port to 2200
sudo nano /etc/ssh/sshd_config
Change port 22 to port 2200

Restart the ssh server

service ssh restart
Note: Before Logging using ssh add custom TCP port 2200 under lightsaail firewall in networking tab in lightsail instance console

# Now Login using command like this

ssh -i .ssh/id_rsa -p 2200 grader@13.127.33.29
# Disabling ssh login as root
sudo nano /etc/ssh/sshd_config

make change PermitRootLogin no

# Configurating Ufw firewall

sudo ufw allow 2200/tcp
sudo ufw allow 80/tcp
sudo ufw allow 123/udp
sudo ufw enable
This will allow all required ports and enables the ufw

After that

sudo ufw status
It will display all allowed ports

# Installing Apache2
In terminal

sudo apt-get install apache2

Now mod_wsgi

sudo apt-get install python-setuptools libapache2-mod-wsgi

Enable mod_wsgi

sudo a2enmod wsgi

## Setting up your flask application to work with apache2
# Creating a flask app

In /var/www directory create a new folder sudo mkdir FlaskApp

Install git

sudo apt-get install git

move to the FlaskApp cd FlaskApp

# In that direcory clone your github repository

sudo git clone https://github.com/paru1234/catalog.git

Rename your repository to FlaskApp

Then rename your project file to __init__.py

Error : While accesssing the client_secrets.json file

PROJECT_ROOT = os.path.realpath(os.path.dirname(__file__))
json_url = os.path.join(PROJECT_ROOT, 'client_secrets.json')
CLIENT_ID = json.load(open(json_url))['web']['client_id']
Use json_url instead client_secrets.json in script

Reffered from stack overflow

Install and configuring postgresql for project
Install Postgres sudo apt-get install postgresql

login to postgres sudo su - postgres

postgres shell psql

create user CREATE USER catalog WITH PASSWORD 'password';

permit user to createdb ALTER USER catalog CREATEDB;

Create a db name catalog with user catalog CREATE DATABASE catalog WITH OWNER catalog;

connect to db \c catalog

revoke all permission to public REVOKE ALL ON SCHEMA public FROM public;

Give schema permission to user catalog GRANT ALL ON SCHEMA public TO catalog;

exit from db and postgres \q and exit

Change the database connection in both db_setup.py and __init__.py as engine = create_engine('postgresql://catalog:password@localhost/catalog')

Now you are ready with your applicatiom

Configure and Enable a New Virtual Host
sudo nano /etc/apache2/sites-available/FlaskApp.conf

In this add the following code

<VirtualHost *:80>
 	ServerName mywebsite.com
 	ServerAdmin admin@mywebsite.com
 	WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
 	<Directory /var/www/FlaskApp/FlaskApp/>
 		Order allow,deny
 		Allow from all
 	</Directory>
 	Alias /static /var/www/FlaskApp/FlaskApp/static
 	<Directory /var/www/FlaskApp/FlaskApp/static/>
 		Order allow,deny
 		Allow from all
 	</Directory>
 	ErrorLog ${APACHE_LOG_DIR}/error.log
 	LogLevel warn
 	CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
Enable the virtual host sudo a2ensite FlaskApp

Disabling the default apache2 page sudo a2dissite 000-default.conf

Create the .wsgi File
```
cd /var/www/FlaskApp
sudo nano flaskapp.wsgi 
```
Add the following code

#!/usr/bin/python
 import sys
 import logging
 logging.basicConfig(stream=sys.stderr)
 sys.path.insert(0,"/var/www/FlaskApp/")

 from FlaskApp import app as application
 application.secret_key = 'Add your secret key'
save and exit

# Deploying flask app with apache2 is referred from Digital ocean

Installing require modules
You can either install all modules on your machine or create a virtual environment for the project and install the modules pip install flask sqlalchemy psycopg2 requests oauth2client

# Setting up your Google Oauth2
Login to your developer console and select your project and edit OAuth details as following

Javascript origin http://13.127.33.29.xip.io

redirect URI

http://13.127.33.29.xip.io\login

http://13.127.33.29.xip.io\gconnect

http://13.127.33.29.xip.io\callback

xip.io is a free DNS which will be the same as using IP address

# Final Step
Restart your apache2 server

sudo service apache2 restart
