# Deploying a Node Js Application on AWS EC2

### Testing the project locally

1. Clone this project
```
git clone https://github.com/verma-kunal/AWS-Session.git
```
2. Setup the following environment variables - `(.env)` file
```
DOMAIN= ""
PORT=3000
STATIC_DIR="./client"

PUBLISHABLE_KEY=""
SECRET_KEY=""
```
3. Initialise and start the project
```
npm install
npm run start
```

### Set up an AWS EC2 instance

1. Create an IAM user & login to your AWS Console
    - Access Type - Password
    - Permissions - Admin
2. Create an EC2 instance
    - Select an OS image - Ubuntu
    - Create a new key pair & download `.pem` file
    - Instance type - t2.micro
3. Connecting to the instance using ssh
```
ssh -i instance.pem ubunutu@<IP_ADDRESS>
```

### Configuring Ubuntu on remote VM

1. Updating the outdated packages and dependencies
```
sudo apt update
```
3. Install Git - [Guide by DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-22-04) 
4. Configure Node.js and `npm` - [Guide by DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-22-04)

### Deploying the project on AWS

1. Clone this project in the remote VM
```
git clone https://github.com/verma-kunal/AWS-Session.git
```
2. Setup the following environment variables - `(.env)` file
```
DOMAIN= ""
PORT=3000






Deploying Node.js with Nginx on EC2

set up Nginx as a reverse proxy for your Node.js application:

Install Nginx on EC2 Instance:
bash
Copy code
sudo apt update
sudo apt install nginx
    • Configure Nginx as a Reverse Proxy:
Edit the Nginx configuration file to set up a reverse proxy:
bash
Copy code
sudo nano /etc/nginx/sites-available/default
Replace the contents with the following configuration:
nginx
Copy code
server {
    listen 80;

    server_name _;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
Save and close the file.
    • Start and Enable Nginx:
bash
Copy code
sudo systemctl restart nginx
sudo systemctl enable nginx
    • Update Security Group Rules:
    • Make sure the security group associated with your EC2 instance allows inbound traffic on port 80 (HTTP) and 3000 (if needed for direct access).
    • Deploy and Run Your Node.js Application:
Deploy and Run Your Node.js Application:
    • Clone the project and navigate to the project directory:
      bash
      Copy code
      git clone https://github.com/verma-kunal/AWS-Session.git
      cd AWS-Session
    • Install the dependencies:
      bash
      Copy code
      npm install
    • Start the application using PM2 for production readiness:
      bash
      Copy code
      sudo npm install -g pm2
      pm2 start npm -- start
      pm2 save
      pm2 startup


```
> For this project, we'll have to set up an [Elastic IP Address](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html) for our EC2 & that would be our `DOMAIN`

3. Initialise and start the project
```
npm install
npm run start
```

> NOTE - We will have to edit the **inbound rules** in the security group of our EC2, in order to allow traffic from our particular port

### Project is deployed on AWS 🎉
