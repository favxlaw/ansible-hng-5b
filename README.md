 # NestJS Boilerplate Deployment with Ansible

This project offers an Ansible playbook for deploying a NestJS boilerplate application, complete with PostgreSQL, RabbitMQ, and Nginx.

## Prerequisites
- Ansible installed on the control machine
- SSH access to the target host(s)
- Git installed on the control machine

## Setup

1. **Generate an SSH key pair on the control machine:**
   ```sh
   ssh-keygen 
   ```

## 2. ** Install Ansible:**

```sh
Copy code
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible -y
```

## 3 Clone the repository:

```sh
Copy code
git clone https://github.com/Rob-in-son/hng_boilerplate_nestjs.git
cd hng_boilerplate_nestjs
git checkout devops
cd ansible
```
## 4 Configure the inventory file:
Create or edit inventory.yml with the following structure in the ansible directory:

```yaml
all:
  hosts:
    <host_name>:
      ansible_host: <host_ip>
      ansible_user: <username>
      ansible_ssh_private_key_file: <private_key_path>
```

## Playbook Structure
main.yml: The main Ansible playbook
nginx.conf.j2: Nginx configuration template
nestjs.service.j2: Systemd service configuration template
Deployment
To deploy the application, run:
```sh
Copy code
ansible-playbook main.yml -i inventory.cfg -b
```

## What the Playbook Does
Sets up a new user for the application
Installs necessary dependencies (Node.js, PostgreSQL, Nginx, RabbitMQ)
Clones the application repository
Sets up the PostgreSQL database
Configures the application environment
Sets up Nginx as a reverse proxy
Configures UFW firewall
Sets up the application as a systemd service
Configuration
The playbook uses several customizable variables in the vars section of main.yml, including:

## Database credentials
Application port
JWT settings
And more

## Logging
# Application logs are stored in:
/var/log/stage_5b/out.log
/var/log/stage_5b/error.log

# Nginx logs are stored in: 
/var/log/nginx/stage_5b_access.log
/var/log/nginx/stage_5b_error.log

## Security
UFW is configured to allow only SSH (port 22) and HTTP (port 80) traffic
The application runs on port 3000, which is not directly accessible from outside
PostgreSQL credentials are stored in /var/secrets/pg_pw.txt
