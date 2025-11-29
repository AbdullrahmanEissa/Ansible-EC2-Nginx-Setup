Ansible EC2 Nginx Setup

![Ansible Logo](https://img.icons8.com/color/48/000000/ansible.png)  
Automate deployment of Nginx on multiple Ubuntu EC2 instances using Ansible from a local control node.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Architecture](#architecture)
- [Requirements](#requirements)
- [Setup Instructions](#setup-instructions)
- [Usage](#usage)
- [Verification](#verification)
- [License](#license)

---

## Project Overview

This project demonstrates how to use **Ansible** to automate the installation and configuration of **Nginx** on multiple **Ubuntu EC2 instances**.  

Features:

- Deploy Nginx across multiple servers in one command.
- Use a single keypair for SSH access.
- Ensure Nginx service is running and enabled on boot.
- Easily extendable for Docker, Load Balancers, or other software.

---

## Architecture

```

```
         +-----------------+
         |   Control Node  |
         |  (Laptop / PC)  |
         +--------+--------+
                  |
        SSH over keypair
                  |
   +--------------+--------------+
   |              |              |
```

+------+-----+ +------+-----+ +------+-----+
|  EC2 Web1  | |  EC2 Web2  | |  EC2 Web3  |
| Ubuntu 24  | | Ubuntu 24  | | Ubuntu 24  |
| Nginx      | | Nginx      | | Nginx      |
+------------+ +------------+ +------------+

````

---

## Requirements

- Ansible >= 2.16  
- Python 3.x on control node  
- Ubuntu 20.04+ EC2 instances  
- SSH Keypair for accessing EC2 instances  
- Internet access for EC2 instances  

---

## Setup Instructions

1. Clone this repository:

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
````

2. Make your private key readable only by you:

```bash
chmod 400 /path/to/key1.pem
```

3. Edit the `hosts.ini` file with your EC2 public DNS/IPs:

```ini
[web]
ec2-13-51-158-37.eu-north-1.compute.amazonaws.com
ec2-16-170-203-30.eu-north-1.compute.amazonaws.com
ec2-13-60-104-240.eu-north-1.compute.amazonaws.com

[web:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=/path/to/key1.pem
```

---

## Usage

Run the Ansible playbook:

```bash
ansible-playbook -i hosts.ini install_nginx.yml
```

* Installs Nginx
* Updates apt cache
* Ensures Nginx is running and enabled

---

## Verification

Check that Nginx is running by visiting any of your EC2 public IPs in a browser:

```
http://13.51.158.37
http://16.170.203.30
http://13.60.104.240
```

You should see the **default Nginx welcome page**.

---

## License

This project is licensed under the MIT License.

