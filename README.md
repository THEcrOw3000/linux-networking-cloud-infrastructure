# Linux Server Deployment — Module 2

Deploying and securing a Linux server on AWS EC2: from a bare virtual machine to a running, tested, internet-facing service.

**Flow:** Create VM → Configure Linux → Secure Access → Deploy Service → Test Connectivity

---

## Linux Fundamentals — Cheat Sheet

### File permissions

```bash
ls -l                         # View file permissions
chmod 755 file.sh             # Set rwx for owner, rx for others
chmod u+x file.sh             # Add execute permission for owner
chown user:group file.sh      # Change file ownership
```

Permission digits: 4 = read, 2 = write, 1 = execute.

- 7 = rwx
- 5 = r-x
- 4 = r--

### Users & groups

```bash
sudo adduser deploy           # Create a new user
sudo usermod -aG sudo deploy  # Add user to sudo group
groups deploy                 # Check group membership
id deploy                     # Display user and group IDs
cat /etc/passwd               # View user accounts
```

### Process management

```bash
ps aux                        # List running processes
top                           # Live process monitor
kill PID                      # Terminate a process
systemctl status nginx        # Check service status
sudo systemctl start nginx    # Start a service
sudo systemctl stop nginx     # Stop a service
sudo systemctl restart nginx  # Restart a service
sudo systemctl enable nginx   # Enable service at boot
journalctl -u nginx -f        # Follow service logs
```

### SSH keys

```bash
ssh-keygen -t ed25519 -C "deploy-key"   # Generate SSH key pair

chmod 400 ~/path/to/aws-key.pem        # Protect AWS private key

ssh -i ~/path/to/aws-key.pem ubuntu@PUBLIC_IP
```

Never upload private SSH keys (`.pem`) to GitHub.

---

## Networking Fundamentals

- **IP addressing / CIDR** — `10.0.0.0/24` represents a network with 256 total IPv4 addresses.
- **DNS** — A records map domain names to IPv4 addresses; CNAME records create aliases.
- **Ports** — 22 (SSH), 80 (HTTP), and 443 (HTTPS) are the main ports used in this lab.
- **Security Groups** — AWS instance-level stateful firewalls that control inbound and outbound traffic.
- **UFW** — Ubuntu host-level firewall that provides an additional security layer.
- **Connectivity** — A service must be listening, and every network firewall layer must allow the required traffic.

---

## Deployment Log

### 1. Create VM

- Provider: AWS EC2
- AMI: Ubuntu Server 24.04 LTS
- Instance type: To be selected based on account eligibility and cost
- Region: To be selected
- Storage: Minimum suitable EBS volume
- Access: SSH key pair

### 2. Configure Linux

```bash
sudo apt update
sudo apt upgrade -y

hostnamectl
uname -a
df -h
free -h

sudo adduser deploy
sudo usermod -aG sudo deploy

id deploy
```

### 3. Secure Access

- Connect to EC2 using the default Ubuntu account and downloaded AWS key.
- Create a dedicated `deploy` user.
- Configure SSH key authentication for the new user.
- Restrict SSH access to the trusted client IP.

Example SSH connection:

```bash
ssh -i ~/path/to/aws-key.pem ubuntu@PUBLIC_IP
```

After configuring the deploy user's authorized key:

```bash
ssh deploy@PUBLIC_IP
```

SSH hardening configuration:

```bash
sudo nano /etc/ssh/sshd_config
```

Recommended settings after verifying key-based access:

```text
PasswordAuthentication no
PermitRootLogin no
PubkeyAuthentication yes
```

Validate the configuration before reloading SSH:

```bash
sudo sshd -t
sudo systemctl reload ssh
```

**AWS Security Group inbound rules:**

- SSH (22): Restricted to My IP.
- HTTP (80): Open to `0.0.0.0/0` for public web access.
- HTTPS (443): Only when HTTPS is configured.

### 4. Configure Host Firewall

```bash
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw enable

sudo ufw status verbose
```

### 5. Deploy Nginx

```bash
sudo apt install nginx -y

sudo systemctl enable nginx
sudo systemctl start nginx

sudo systemctl status nginx
```

### 6. Test Connectivity

```bash
curl localhost
```

Check the HTTP response:

```bash
curl -I http://localhost
```

Test the public server:

```bash
curl -I http://PUBLIC_IP
```

Open the following address in a browser:

```text
http://PUBLIC_IP
```

Test SSH key-based access:

```bash
ssh deploy@PUBLIC_IP
```

Verify that password authentication is disabled only after confirming key-based access works.

---

## Results

Evidence will be added after completing the deployment.

| Screenshot | Description | Status |
|---|---|---|
| `ec2-instance.png` | AWS EC2 instance details | Pending |
| `ssh-connection.png` | Successful SSH connection | Pending |
| `linux-system-info.png` | Linux system information | Pending |
| `users-permissions.png` | User and permission configuration | Pending |
| `ufw-status.png` | Host firewall configuration | Pending |
| `nginx-status.png` | Nginx active and enabled | Pending |
| `browser-test.png` | Nginx page accessible through browser | Pending |

---

## Key Learnings

- Linux user and permission management.
- The difference between private and public IP addresses.
- SSH key-based authentication and secure remote access.
- The difference between AWS Security Groups and Linux UFW.
- Managing Linux services with `systemctl`.
- Deploying Nginx and testing HTTP connectivity.
- Documenting infrastructure deployment with practical evidence.
- Monitoring AWS resources to avoid unnecessary costs.

---

## Project Status

**In Progress** — Deployment and validation evidence will be updated as each lab stage is completed.

**Author:** Amr Mohamed  
**GitHub:** https://github.com/THEcrOw3000
