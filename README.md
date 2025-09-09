# Bastion-host-on-AWS-All-in-one-Bash-script-AWS-CLI-
Today I automated a Bastion Host setup on AWS using a single Bash script
Steps I followed:

 🔹Step 1 — Create a VPC
CIDR: 12.0.0.0/16
This VPC will contain both public and private subnets.
 🔹Step 2 — Create Subnets
 Public Subnet → 12.0.1.0/24
 The public subnet will host the Bastion Host EC2.
 Private Subnet → 12.0.2.0/24
 The private subnet will host the target EC2 insta
 🔹Step 3 — Launch a Bastion Host (EC2)
Deploy an EC2 instance inside the public subnet.

Attach a public IP to this EC2 instance.

Enable SSH (Port 22) in the security group, but restrict access only to trusted IPs 

 🔹Step 4 — Launch Private EC2 Instance
Deploy another EC2 instance inside the private subnet.

Do not assign a public IP.

Security group allows SSH only from the Bastion Host EC2, not from the internet.

 🔹 Step 5 — Configure Internet Gateway
Create an Internet Gateway and attach it to the VPC.

Update the Route Table for the public subnet to allow internet access through the Internet Gateway.
 🔹Step 6 — Configure Route Tables
Public Subnet Route Table → Has a route to the Internet Gateway.

Private Subnet Route Table → Does not have a direct route to the Internet. Access is allowed only via the Bastion Host.
 🔹 Step 7 — Connect to the Private Instance
 1. Connect to the Bastion Host EC2 using SSH:
 ssh -i bastion-key.pem ec2-user@<Bastion-Public-IP>
 2. From the Bastion Host, connect to the Private EC2:
 ssh -i private-key.pem ec2-user@<Private-EC2-IP>
