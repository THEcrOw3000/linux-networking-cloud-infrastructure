Linux, Networking & Cloud Infrastructure — Module 02
This project documents my hands-on work with Linux, networking, and cloud infrastructure. I used an AWS EC2 Ubuntu server to practise Linux administration, connect to a remote machine, and work through deploying a web server.
Key Objectives
- Practise Linux CLI commands, file permissions, users, groups, processes, services, and SSH keys.
- Understand IP addressing, DNS, ports, firewalls, and AWS Security Groups.
- Follow the deployment process: create a virtual machine, configure Linux, secure access, deploy a service, and test connectivity.
Environment
- Cloud provider: AWS
- Service: EC2
- Region: us-east-2 (Ohio)
- Instance type: t3.micro
- Operating system: Ubuntu Server 26.04.1 LTS
- Local machine: Kubuntu
What I worked on
1. Linux commands and system information
I connected to the EC2 server over SSH and used Linux commands to check the current user, hostname, operating-system version, kernel, disk space, memory, and system uptime.

Some of the commands used:
whoami
hostname
hostnamectl
uname -a
lsb_release -a
df -h
free -h
uptime
2. Users and permissions
I practised creating a separate user and adding it to the sudo group, then checking its groups and user ID.
sudo adduser deploy
sudo usermod -aG sudo deploy
id deploy
groups deploy
I also reviewed common file-permission commands such as ls -l, chmod, and chown.
3. SSH access
I connected from Kubuntu to the EC2 Ubuntu server using the EC2 private key.

Example command:
ssh -i ~/.ssh/linux-infrastructure-lab.pem ubuntu@<EC2_PUBLIC_IP>
The private key stays on my computer and is not included in this repository.
4. Networking and security
I reviewed the purpose of IP addresses, CIDR notation, DNS, common ports, and firewall rules.

For the EC2 Security Group, the relevant access rules for this lab are:
Rule	Port	Purpose
SSH	22	Remote server access; restricted to my IP
HTTP	80	Web access


5. Nginx and connectivity
I worked with Nginx as the web server and used systemctl to manage Linux services.

Commands used for installation and service checks:
sudo apt update
sudo apt install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
sudo systemctl status nginx
To test the service locally:
curl -I http://localhost
To test access from my own computer:
curl -I http://<EC2_PUBLIC_IP>
The public test requires Nginx to be running and inbound HTTP traffic on port 80 to be allowed by the EC2 Security Group.
Screenshots
Screenshots for the lab are saved in the screenshots/ folder. They should show the actual commands and results from the work, without exposing private keys, passwords, AWS account details, or other sensitive information.
What I learned
- Using Linux commands to inspect and manage a server.
- Creating users and checking group permissions.
- Connecting to an AWS EC2 instance with SSH.
- Understanding the role of ports and AWS Security Groups.
- Managing a service with systemctl.
- Installing Nginx and checking HTTP connectivity.
Repository contents
- docs/ — notes about Linux, networking, SSH, users, and deployment checks.
- scripts/ — helper scripts used for the lab.
- screenshots/ — practical evidence from the lab.
