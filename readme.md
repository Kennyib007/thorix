# AltSchool Second Semester Cloud Engineering Exam

## Project Objective
To create a dynamic prototype of a web application with the requirements listed below for my startup `Thorix_by_Kenny` to showcase my technical skills to investors.

- Provisioning the Server with Ubuntu distribution using an (EC2) or another cloud provider (e.g., DigitalOcean, Azure).
- Web Server Setup install Nginx (preferred) or Apache.
- Dynamic Landing Page (Beyond Static HTML), Create a personalized landing page with:
- Production-Ready Networking & Security 
- Bonus: Secure with Let’s Encrypt SSL (Certbot) and a custom domain.

**Cloud Provider:** AWS (Amazon Web Services)

## Steps:
1. **Set up base infrastructure**
To begin preparation for this project a base infrastructure of VPC, Subnets, Route table and internet gateway (igw) is required on AWS

   - Create a VPC on AWS to include required subnet (public or private)
   - Create an internet gateway to enable connection to the internet or endpoints to enable private connections to other services
   - Configure route tables to route traffic from your subnets to igw or required endpoint.

With a view of expansion and improved availability for my base infrastructure I created a VPC with 4 subnets (2 private, 2 public), route to the internet through an internet gateway, routes and s3endpoint for my private subnets. You may adopt an alternative approach to setting up your base infrastructure, provided all required components are present and properly configured.

![base](./Base%20Infra.JPG)

2. **Provision an EC2 Instance with Ubuntu distribution**:
   - Navigate to the EC2 page on the console and select launch instance
   - Select the Ubuntu Server 20.04 LTS (also compatible with 22.04 LTS).
   - t2.micro (free tier eligible).
   - Create a Security key to facilitate SSH connection
   - Create a security group with appropriate inbound rules to allow:
     - **SSH (Port 22)**
     - **HTTP (Port 80)**
     - **HTTPS (Port 443)**
   - Launched and confirmed instance state
   ![running ec2](./ec2%20available.jpg)
   - Create and allocate Elastic IP to maintain a consistent address across instance restarts.

3. **Accessed the Server via SSH and setup web server (Nginx)**:
   - SSH into the server by using the command below
   `ssh -i your-key.pem ubuntu@your-elastic-ip`
   - Install Nginx
   ```bash 
   sudo apt update
   sudo apt install nginx -y
   ```
   - Confirm Nginx status with  systemd
   ` sudo systemctl status nginx `
   - Confirm Nginx is available by visiting ip address with http (run curl ifconfig.me or copy from your EC2 dashboard)
   `http://serverip`
   - Build dynamic landing page with HTML and CSS and copy your index.html, style.css, and any assets to /var/www/html/ on your server.

4. **Set up custom domain and secure with Let’s Encrypt SSL (Certbot)**
   - Configure a custom domain using AWS Route 53.
     - Navigate to route53 in the AWS console
     - Select hosted zone for registered domain.
     - Add an A record to map the server's IP address to domain name in my case (thorix.kennycloudchronicles.com)
   - Secured with Let’s Encrypt SSL (Certbot)
    - Install Certbot
    ``` sudo apt install certbot python3-certbot-nginx -y
        sudo certbot --nginx
    ```
    - Follow the prompts to complete SSL cert generation.

My site is accesible via domain name at https://thorix.kennycloudchronicles.com and ip address 44.218.159.55

![rendered page](./page%20rendered.JPG)

## Conclusion

This project demonstrates the deployment of a dynamic web application using cloud infrastructure best practices in line with the requirements AltSchool Cloud Engineering second semester exam 2025.
© 2025 Kehinde Ibrahim (Kenny).