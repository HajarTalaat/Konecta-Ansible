Ansible Setup Instructions for Multi-Machine Integration

1. Infrastructure Overview
Public Instance: Acts as the Ansible control node.
Private Instances: Managed nodes where configurations are applied.
SSH Configuration: The control node establishes SSH connections with the private instances using key-based authentication.

2. Setting Up the Instances
Step 1: Launching EC2 Instances
Launch one public instance and two private instances in AWS.
Assign a security group to allow:
Public instance: SSH (port 22) from your IP, and outbound access to private instances.
Private instances: Allow SSH only from the public instance.

Step 2: Generate an SSH Key Pair
On the control node (public instance), generate an SSH key pair:
ssh-keygen -t rsa -b 4096 -C "ansible-control"
Copy the public key to the private instances:
ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@<private-instance-ip>

Step 3: Configure SSH Access:
Test SSH access from the control node:
ssh ubuntu@<private-instance-ip>

Step 4: Configure Ansible Inventory
Create an inventory.ini file:
[frontend]
private-instance-1 ansible_host=<private-ip-1> ansible_user=ubuntu

[Docker]
private-instance-2 ansible_host=<private-ip-2> ansible_user=ubuntu

Ensure Ansible is installed on the control node:
sudo apt update && sudo apt install -y ansible

Step 5: Test Ansible Connectivity:
ansible all -i inventory.ini -m ping



