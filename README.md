# Linux, Networking & Cloud Infrastructure — Module 02

Deploying and configuring a Linux server on AWS EC2, practising Linux administration, remote access, networking, and web server deployment.

**Flow:** Create VM → Configure Linux → Manage Users → Secure Access → Deploy Nginx → Test Connectivity

---

## Linux Fundamentals — Cheat Sheet

### File permissions

```bash
ls -l                       # View file permissions
chmod 755 file.sh           # Owner: rwx, Group: r-x, Others: r-x
chmod u+x file.sh           # Add execute permission for owner
chown user:group file.sh    # Change file owner and group
```

Permission values:

- `4` = Read
- `2` = Write
- `1` = Execute
- `7` = Read + Write + Execute
- `5` = Read + Execute

### Users & groups

```bash
sudo adduser deploy              # Create a new user
sudo usermod -aG sudo deploy    # Add user to sudo group
id deploy                        # Check user ID and groups
groups deploy                    # Display group membership
cat /etc/passwd                  # View user account information
```

### Process & service management

```bash
ps aux                       # List running processes
top                          # Live process monitor
kill <PID>                   # Stop a process
systemctl status nginx       # Check Nginx service status
sudo systemctl start nginx   # Start Nginx
sudo systemctl stop nginx    # Stop Nginx
sudo systemctl restart nginx # Restart Nginx
sudo systemctl enable nginx  # Enable Nginx at boot
journalctl -u nginx          # View Nginx logs
```

### SSH access

```bash
# Connect to the EC2 instance using its private key
ssh -i ~/.ssh/linux-infrastructure-lab.pem ubuntu@<EC2_PUBLIC_IP>

# Check SSH directory permissions
ls -la ~/.ssh

# Set private key permissions
chmod 400 ~/.ssh/linux-infrastructure-lab.pem
```

The EC2 private key is stored locally and is not included in this repository.

---

## Networking Fundamentals

- **IP Addressing:** Identifies a device on a network and allows communication between hosts.
- **CIDR:** Defines network ranges. For example, `10.0.0.0/24` represents a network with 256 total IPv4 addresses.
- **DNS:** Translates domain names into IP addresses.
- **Ports:** Identify services running on a server. Common examples include `22` for SSH, `80` for HTTP, and `443` for HTTPS.
- **AWS Security Groups:** Stateful virtual firewalls that control inbound and outbound traffic for EC2 instances.
- **UFW:** A Linux host-based firewall used to manage network access at the operating-system level.

A service can be running locally but still inaccessible externally if the required network traffic is blocked.

---

## Deployment Log

### 1. Create VM

- **Cloud Provider:** AWS
- **Service:** EC2
- **AMI:** Ubuntu Server 26.04.1 LTS
- **Instance Type:** t3.micro
- **Region:** us-east-2 (Ohio)

### 2. Configure Linux

Update the package list and install available updates:

```bash
sudo apt update
sudo apt upgrade -y
```

Create a separate user and grant sudo access:

```bash
sudo adduser deploy
sudo usermod -aG sudo deploy

# Verify user and group information
id deploy
groups deploy
```

### 3. Connect through SSH

From the local Kubuntu machine:

```bash
ssh -i ~/.ssh/linux-infrastructure-lab.pem ubuntu@<EC2_PUBLIC_IP>
```

Verify the server environment:

```bash
whoami
hostname
uname -a
lsb_release -a
```

### 4. Deploy Nginx

Install Nginx and configure it to start automatically:

```bash
sudo apt install nginx -y

sudo systemctl enable nginx
sudo systemctl start nginx
sudo systemctl status nginx
```

### 5. Test connectivity

Test the web server locally:

```bash
curl -I http://localhost
```

Test access from the local machine:

```bash
curl -I http://<EC2_PUBLIC_IP>
```

External access requires Nginx to be running and HTTP traffic on port `80` to be allowed by the EC2 Security Group.

---

## Results & Evidence

Add screenshots of your actual work to the `screenshots/` directory.

Suggested evidence:

- EC2 instance details showing the instance type and region.
- Successful SSH connection to the Ubuntu server.
- Linux system information from terminal commands.
- User and group configuration.
- Nginx service status.
- Browser or terminal test showing the Nginx page.

Do not upload private keys, passwords, access tokens, or other sensitive information.

---

## Key Learnings

- Using Linux CLI commands to inspect and manage a remote server.
- Understanding file permissions, users, and groups.
- Connecting to AWS EC2 through SSH.
- Understanding IP addressing, CIDR, ports, and DNS.
- Learning how AWS Security Groups control network access.
- Installing and managing Nginx with `systemctl`.
- Understanding the difference between a running service and one enabled at boot.

---

## Repository Structure

```text
linux-networking-cloud-infrastructure/
├── docs/
├── scripts/
├── screenshots/
├── .gitignore
└── README.md
```

**Author:** Amr Mohamed  
**GitHub:** [THEcrOw3000](https://github.com/THEcrOw3000)
