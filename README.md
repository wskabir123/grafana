# The goal is to deploy grafana using ansible 🍟🍟


 Setting up SSH Key Authentication for Ansible

SSH key authentication provides a secure and efficient way to connect to remote servers from your Ansible control node. Follow these steps to set up SSH key authentication for your Grafana servers and configure Ansible to use them:

 Why SSH Key Authentication?

- **Security**: SSH key authentication eliminates the need to enter passwords for each SSH connection, making it less vulnerable to brute-force attacks.


  ** Generate an SSH key pair on ansible node:
   ```
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```

2. **Copy Public Key to Grafana Servers**:
   ```
   ssh-copy-id -i ~/.ssh/id_rsa.pub waris(replaceme)@192.168.1.100
   Now try logging into the machine, with:   "ssh 'waris(replaceme)@192.168.1.100'"```
3. **Configure Inventory File**:
   Create or update your Ansible inventory file (`gra_servers`) add your SSH user and private key

   [grafana_servers]
   grafana-server-1 ansible_host=192.168.1.100

   [grafana_servers:vars]
   ansible_user=waris(replaceme)
   ansible_ssh_private_key_file=~/.ssh/id_rsa
   ```
Edit sudoers file on the host: Log in to the remote host as a user with sudo privileges
**waris(changeme)  ALL=(ALL) NOPASSWD:ALL

# Deploy Grafana using Ansible

After the following steps:

- SSH key authentication
- Configuring the inventory file

You can deploy grafana using ansible to your traget machine.

Magic happens here..

ansible-playbook -i gra_servers grafana-deployment.yml
```
### This command will deploy Grafana on the selected hosts listed in your Ansible inventory file.

**try accessing it with your ip:3000 also check the service on the host side **systemctl status grafana-server
Use admin/admin to login and change the password


Additionally use rm_grafana.yml to remove it from target instance :) 

ansible-playbook -i gra_servers rm_grafana.yml
