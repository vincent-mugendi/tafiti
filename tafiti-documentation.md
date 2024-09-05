# Tafiti Project Documentation
![tafiti logo](tafiti.png)

## Introduction

**Tafiti** is a privacy-focused search engine designed to provide users with an ad-free and secure search experience. Built using SearXNG, Docker, and Nginx, Tafiti aims to enhance user privacy by aggregating search results from multiple sources without tracking or storing personal data. This documentation outlines the process of creating Tafiti, the achievements, and the lessons learned during the project.

## Project Overview

### Objectives

- **Privacy Protection**: Ensure that user searches are not tracked or stored.
- **Ad-Free Experience**: Provide search results without displaying advertisements.
- **Secure Connection**: Use HTTPS to secure user data and interactions.

### Technologies Used

- **AWS EC2**: Cloud computing service to host the search engine.
- **SearXNG**: An open-source metasearch engine that respects user privacy.
- **Docker**: Containerization platform used to deploy SearXNG.
- **Nginx**: Web server and reverse proxy to manage HTTP/HTTPS requests.
- **Let's Encrypt**: Free SSL/TLS certificate provider for securing the domain.

## Steps to Create Tafiti

### 1. Setting Up the Cloud Server

**AWS EC2 Instance**:
- **Sign-Up**: Created a free-tier AWS account.
- **Launch Instance**: Deployed an EC2 instance with Amazon Linux 2.
- **Configuration**: Configured security group to allow SSH access.
- **Connection**: Connected to the instance via SSH.

### 2. Connecting the Domain

**Domain Setup**:
- **Public IP**: Obtained the public IP address of the EC2 instance.
- **DNS Configuration**: Configured DNS records with a third-party provider to point `search.example.com` to the EC2 instance.

### 3. Deploying SearXNG with Docker

**Docker Installation**:
- **Installation**: Installed Docker on the EC2 instance.
- **Containerization**: Ran SearXNG in a Docker container with the `BASE_URL` environment variable set to `https://search.example.com`.

### 4. Configuring Nginx as a Reverse Proxy

**Nginx Setup**:
- **Installation**: Installed Nginx on the EC2 instance.
- **Configuration**: Configured Nginx to proxy requests from port 80 to the SearXNG container running on port 8080.
- **Reverse Proxy**: Set up Nginx to forward HTTP requests to SearXNG and handle HTTPS redirection.

### 5. Securing the Domain with HTTPS

**SSL Certificate**:
- **Certbot Installation**: Installed Certbot to manage SSL certificates.
- **Certificate Acquisition**: Used Certbot to obtain and install an SSL certificate for `search.example.com`.
- **Auto-Renewal**: Configured Certbot to automatically renew the SSL certificate.

## Achievements

- **Privacy Assurance**: Successfully deployed a search engine that does not track user searches or display ads.
- **Secure Deployment**: Enabled HTTPS to ensure secure communication between users and the search engine.
- **Scalable Infrastructure**: Utilized Docker for containerization, making it easier to scale and manage the application.

## Lessons Learned

- **AWS EC2 Management**: Gained hands-on experience with AWS EC2, including instance management, security group configuration, and SSH access.
- **Docker Deployment**: Learned to deploy applications using Docker, which simplifies container management and isolation.
- **Nginx Configuration**: Acquired skills in configuring Nginx as a reverse proxy and managing HTTP/HTTPS traffic.
- **DNS Management**: Understood how to configure DNS records and verify domain propagation.
- **SSL/TLS Implementation**: Implemented SSL/TLS certificates using Let’s Encrypt to ensure secure communications.

## Conclusion

The Tafiti project was a valuable learning experience that enhanced my skills in cloud computing, containerization, web server configuration, and security. By building Tafiti, I demonstrated the ability to deploy and manage a privacy-focused search engine while ensuring a secure and ad-free user experience.

Feel free to explore Tafiti and witness the results of this project firsthand [HERE](https://search.vincentmugendi.tech)
For any questions or additional information, please reach out, check my profile for contact details.
