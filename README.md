# QuickLoan – Scalable Web Application on AWS

## Project Overview

QuickLoan is a scalable web application deployed on Amazon Web Services (AWS).
The goal of this project was to design and implement a **highly available, scalable, and secure cloud architecture** for hosting a web application.

The application was first deployed and tested on an EC2 instance using **Nginx and PHP**. After successful testing, an **Amazon Machine Image (AMI)** was created and used in an **Auto Scaling Launch Template** to dynamically scale application instances based on demand.

An **Application Load Balancer (ALB)** was placed in front of the Auto Scaling Group to distribute incoming traffic across multiple EC2 instances.

The application database is hosted on **Amazon RDS (MySQL)**, and Security Groups were configured to allow secure communication between the application servers and the database.

---

## Project Duration

Academic / Internship Project

---

## Tech Stack

### Frontend

* HTML
* CSS
* JavaScript

### Backend

* PHP

### Database

* MySQL (Amazon RDS)

### Web Server

* Nginx

### Cloud Platform

* AWS

---

## AWS Services Used

* Amazon VPC
* Amazon EC2
* Amazon RDS (MySQL)
* Application Load Balancer (ALB)
* Auto Scaling Group
* Launch Template
* Amazon Machine Image (AMI)
* Security Groups
* Internet Gateway

---

## Architecture Overview

The application architecture includes:

User → Application Load Balancer → Auto Scaling EC2 Instances → Amazon RDS

Key features of the architecture:

* Highly available infrastructure
* Automatic scaling of EC2 instances
* Load balanced traffic
* Secure communication between services
* Managed relational database

---

## Application Deployment Steps

### 1. Update the System

```bash
sudo hostnamectl set-hostname appsrv
sudo dnf update -y
```

---

### 2. Install Nginx

```bash
sudo dnf install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```

---

### 3. Install PHP

```bash
sudo dnf install php8.2 php-fpm php-mysqlnd php-pdo php-mbstring -y
php -v
```

Start PHP service:

```bash
sudo systemctl start php-fpm
sudo systemctl enable php-fpm
sudo systemctl restart nginx
```

---

### 4. Install MySQL Client (MariaDB)

```bash
sudo yum install mariadb105 -y
```

This client is used to connect to the **Amazon RDS MySQL database**.

---

### 5. Create Database and Tables

Connect to the database:

```bash
mysql -h <db_endpoint> -u <username> -p
```

Then run the SQL script:

```
init.sql
```

This script creates the required **database and tables**.

---

### 6. Copy Application Files

Copy the following directories:

```
includes
public
```

to:

```
/usr/share/nginx/html/
```

---

### 7. Set Required Permissions

```bash
sudo chown -R nginx:nginx /usr/share/nginx/html/public
sudo chmod -R 755 /usr/share/nginx/html/public
```

---

### 8. Configure Nginx

Update the configuration file with your domain name:

```
quickloan.conf
```

Copy the configuration file:

```bash
sudo cp /usr/share/nginx/html/nginx/quickloan.conf /etc/nginx/conf.d/
```

Test Nginx configuration:

```bash
sudo nginx -t
```

Restart Nginx:

```bash
sudo systemctl restart nginx
```

---

### 9. Configure Database Connection

Update the file:

```
/usr/share/nginx/html/includes/db_connect.php
```

Add the following details:

* db_endpoint
* username
* password
* db_name

---

### 10. Access the Application

Open the browser and access the application:

```
http://<EC2-Public-IP>
```

or your configured domain name.

---

## Security Implementation

Security Groups were configured with the following rules:

### EC2 Security Group

* Allow HTTP (Port 80)
* Allow SSH (Port 22)

### RDS Security Group

* Allow MySQL (Port 3306) only from EC2 instances

---

## Key Features

* Highly available cloud architecture
* Automatic scaling using Auto Scaling Group
* Load balancing using Application Load Balancer
* Secure database access through RDS
* Nginx and PHP based application deployment
* Fault tolerant infrastructure

---

## Skills Demonstrated

* AWS Cloud Architecture
* EC2 Deployment
* RDS Database Configuration
* Auto Scaling Implementation
* Load Balancer Configuration
* Linux Server Administration
* Nginx Web Server Configuration
* Secure Network Design using VPC

---

## Future Improvements

* Infrastructure as Code using Terraform
* CI/CD pipeline using Jenkins or GitHub Actions
* Monitoring using Amazon CloudWatch
* Containerization using Docker
* Deployment using Kubernetes (EKS)

---

## Author 
