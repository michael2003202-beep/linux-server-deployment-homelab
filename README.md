# Linux Server Deployment Homelab

# Project Overview:
- This repository documents the setup and configuration of my local Linux Lab Environment. It's built
with the goals of building a foundation for server deployment, networking, and security testing. I've built a Linux Server using an Ubuntu Server inside a virtualized environment. The server's configured with a web server, database server, firewall rules and SSH remote access.

- The goal of this project is to simulate a small infrastructure environment and practice system administration tasks such as service management, networking, and server configuration.

# Environemnt:
- Host Machine
$\cdot$ macOS
$\cdot$ Intel i7 MacBook Pro

# Virtualization:
$\cdot$ VirtualBox

# Operating System:
$\cdot$ Ubuntu Server

# Services:
$\cdot$ NGINX
$\cdot$ MySQL

# Architecture:
MacBook
   │
   ├─ SSH → localhost:2222
   └─ HTTP → localhost:8080
        │
VirtualBox NAT Port Forwarding
        │
Ubuntu Server VM
   ├─ NGINX Web Server
   └─ MySQL Database

# Virtual Machine Setup:
- VM was created using VirtualBox
- Configuration:
    - Memory: 4096 MB
    - CPU: 2 cores
    - Disk: 25 GB
    - Network: NAT
    - Ubuntu Server 24.04 LTS was installed using ISO installer.

# Networking Configuration:
- VM network adapter was configuring using NAT networking.
- NAT allows the virtual machine to access the internet through the host machine
- Port Forwarding rules were created to allow host access to services running inside the VM.

# SSH Port Forward:
- Host IP: 127.0.0.1
- Host Port: 22222
- Guest IP: 10.0.2.15
- Guest Port: 22

# Web Server Port Forward:
- Host Port: 8080
- Guest Port: 80
- This allows host machine to connect to services inside the VM

# Verifying Network Configuation:
- After installation the networking configuration should be verified:
    ```bash
    ip a
    ```
- VM receives IP address from VirtualBox NAT which confirms VM has internet connectivity

- Following Installation system is updated:
    ```bash
    sudo apt update
    sudo apt upgrade -y
    ```
# NGINX installation:
- Web Server installed using package manager:
    ```bash
    sudo apt install nginx
    ```
- Verify service status:
    ```bash
    sudo systemctl status nginx
    ```
# Configure Firewall:
- Ubuntu uses UFW (Uncomplicated Firewall)
- Enable firewall:
    ```bash
    sudo ufw enable
    ```
- Allow HTTP traffic:
    ```bash
    sudo ufw allow 80
    ```
- Verify firewall rules:
    ```bash
    sudo ufw status
    ```
# Install Database Server:
- MySQL databse server installation:
    ```bash
    sudo apt install mysql-server
    ```
- Verify database service:
    ```bash
    sudo systemctl status mysql
    ```
# Secure MySQL Installation:
- Run MySQL security configuration script:
    ```bash
    sudo mysql_secure_installation
    ```
- Options selected:
    Remove anonymous users: YES
    Disallow root login remotely: YES
    Remove test database: YES
    Reload privilege table; YES

# Create Database:
- Access the MySQL shell:
    ```bash
    sudo mysql
    ```
- Create a database:
    ```bash
    CREATE DATABASE project1db;
    ```
- Verify database creation:
    ```bash
    SHOW DATABASES;
    ```
- Exit MySQL:
    ```bash
    exit
    ```

# Configure VirtualBox Port Forwarding:
- Since VirtualBox NAT networking does not allow direct access to the VM IP address from the host, port forwarding was configured.
- VirtualBox Network Configuration:
    Adapter: NAT
- Port Forwarding Rules
    SSH
        - Host IP: 127.0.0.1
        - Host Port: 2222
        - Guest IP: 10.0.2.15
        - Guest Port: 22
    HTTP
        - Host Port: 8080
        - Guest Port: 80
# Testing Web Server:
- Inside VM:
    ```bash
    curl localhost
    ```
- From host machine:
    http://localhost:8080
# Testing SSH Access;
- SSH access test from host machine
    ```bash
    ss user.name@localhost -p 2222
    ```
- Sucessful login confirms remote admin is working

# Service verification:
    ```bash
    sudo systemctl status nginx
    sudo systemctl status mysql
    sudo systemctl status ssh
    ```

# Troubleshooting:
- Unable to Access VM from Host
    - Cause: VirtualBox NAT Networking prevents direct access to VM internal IP addresses.
    - Solution: Configure NAT port forwarding rules:
        SSH: localhost: 2222 -> VM port 22
        HTTP: localhost: 8080 -> VM port 80