# The goal is to deploy grafana using ansible 🍟🍟


 Setting up SSH Key Authentication for Ansible

 Why SSH Key Authentication? SSH key authentication eliminates the need to enter passwords for each SSH connection, making it less vulnerable to brute-force attacks.

-  **Generate an SSH key pair on ansible node:**
   
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   

-  **Copy Public Key to intended grafana host**:
   
   ssh-copy-id -i ~/.ssh/id_rsa.pub waris(replaceme)@192.168.1.100 also try to test if the ssh connection works "ssh 'waris(replaceme)@192.168.1.100

- **Update Ansible inventory file (`gra_servers`) add your SSH user and private key also add the user to /etc/sudoers**


waris(changeme)  ALL=(ALL) NOPASSWD:ALL


### Deploy Grafana using Ansible Magic happens here..

- **ansible-playbook -i gra_servers grafana-deployment.yml**

This command will deploy Grafana on the selected hosts listed in your Ansible inventory file also opens Firewall port on the target host if its not already open.

try accessing it with your ip:3000 also check the service on the host side **systemctl status grafana-server
Use admin/admin to login and change the password


**Additionally use rm_grafana.yml to remove it from target instance 😊**


- **ansible-playbook -i gra_servers rm_grafana.yml**


/Waris
