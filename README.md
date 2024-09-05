# Tafiti: Privacy-Focused Search Engine
![tafiti logo](tafiti.png)

## Overview

**Tafiti** is a search engine designed with user privacy at its core. It delivers search results without tracking user data or serving advertisements. Built using modern technologies, Tafiti ensures a secure and seamless search experience.

## Key Features

- **Privacy-First**: No user tracking or ad serving.
- **Secure**: HTTPS encrypted connections.
- **Open Source**: Built with SearXNG, a privacy-respecting search engine software.

## Technologies Used

- **SearXNG**: The search engine software providing privacy-focused search capabilities.
- **Docker**: Containerization for easy deployment and management.
- **Nginx**: Reverse proxy to manage traffic and enable HTTPS.
- **AWS EC2**: Cloud server hosting the application.
- **Certbot**: SSL certificate management for secure HTTPS connections.

## Prerequisites

Before setting up Tafiti, ensure you have the following:

- **AWS Account**: For creating and managing the EC2 instance.
- **Docker**: To run SearXNG in a container.
- **Domain Name**: For custom search engine URL.
- **Nginx**: For reverse proxy configuration.

## Getting Started

Follow these steps to deploy Tafiti:

### 1. Setting Up Your Cloud Server

1. **Sign Up for AWS Free Tier**:
   - Create an AWS account if you don't have one.

2. **Launch an EC2 Instance**:
   - Log into the AWS console and go to the EC2 Dashboard.
   - Launch a new instance using Amazon Linux 2 AMI.
   - Choose instance type `t2.micro` (free tier eligible).
   - Configure instance details, add storage (default 8GB), and set up security groups (allow SSH).
   - Review, create a new key pair, and launch the instance.

3. **Connect to Your Instance**:
   - Find your instance’s Public IP in the EC2 dashboard.
   - Use SSH to connect: `ssh -i "path-to-your-key.pem" ec2-user@<PublicIP>`.

### 2. Domain Configuration

1. **Find Your EC2 Instance's Public IP Address**:
   - Go to the EC2 dashboard and copy the Public IPv4 address.

2. **Update DNS Records**:
   - Log in to your domain registrar.
   - Add an A Record for `search.yourdomain.com` pointing to your EC2 instance’s IP address.
   - Save the record and verify DNS propagation.

### 3. Deploying SearXNG Using Docker

1. **Install Docker**:
   - SSH into your EC2 instance.
   - Update packages: `sudo yum update -y`.
   - Install Docker: `sudo amazon-linux-extras install docker -y`.
   - Start Docker: `sudo service docker start`.
   - Add user to Docker group: `sudo usermod -aG docker ec2-user`. Log out and back in.

2. **Run SearXNG**:
   - Create a directory: `mkdir searxng && cd searxng`.
   - Deploy SearXNG container: 
     ```bash
     docker run -d --name searxng \
     -e "BASE_URL=https://search.yourdomain.com" \
     -p 8080:8080 \
     searxng/searxng
     ```
   - Check container status: `docker ps`.

### 4. Configuring Nginx as a Reverse Proxy

1. **Install Nginx**:
   - On your EC2 instance, install Nginx: `sudo yum install nginx -y`.

2. **Configure Nginx**:
   - Edit the Nginx configuration: `sudo vim /etc/nginx/nginx.conf`.
   - Replace the server block with:
     ```nginx
     server {
         listen 80;
         server_name search.yourdomain.com;

         location / {
             proxy_pass http://localhost:8080;
             proxy_set_header Host $host;
             proxy_set_header X-Real-IP $remote_addr;
             proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
             proxy_set_header X-Forwarded-Proto $scheme;
         }
     }
     ```
   - Start Nginx: `sudo service nginx start`.

### 5. Securing Your Domain with HTTPS

1. **Install Certbot**:
   - Install Certbot: `sudo yum install certbot python2-certbot-nginx -y`.

2. **Obtain an SSL Certificate**:
   - Run Certbot: `sudo certbot --nginx -d search.yourdomain.com`.

3. **Verify and Auto-Renew**:
   - Test SSL setup by visiting `https://search.yourdomain.com`.
   - Test auto-renewal: `sudo certbot renew --dry-run`.

## Conclusion

Congratulations! You've successfully set up Tafiti, a privacy-focused search engine, using modern cloud and containerization technologies. This setup not only ensures a secure and private search experience but also provides you with valuable skills in cloud computing, containerization, and web security.

Feel free to reach out if you have any questions or need further assistance. Happy searching!

# RESOURCES
- find tafiti project documentation [here](./tafiti-documentation.md)
- access tafiti using this [link](https://search.vincentmugendi.tech)
