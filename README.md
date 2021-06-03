# Packer, Ansible, and Terraform Demo

This is a demo using ansible code for provisioning a static website using nginx during the Packer baking process. Nginx needs to be enabled in systemctl and this starts on every boot so it is ready to process once the instance starts. Tags are assigned during the bake process to AMI. This tag is used by Terraform to identify the latest AMI available and use it for EC2 instance creation. In packer.json you need to provide subnet id to packer builder so it can use this subnet id to create the AMI. For now, the IaC terraform code is divided into two parts. The first contains all the network details, such as the VPC, subnet, security groups, and other network details. The second part creates the EC2 instance inside the created network using the AMI generated by Packer.

## Getting Started

Step 1: Setup a network using Terraform

Step 2: Create AMI using packer and ansible inside the above-created network

Step 3: Setup EC2 instance inside the network with packer AMI

Provide access key and token in Terraform and Packer code.

### Command to run network Terraform

Go in folder networkTerraform, run command: 

1. terraform init

2. terraform plan

3. terraform apply

### Command to run Packer

Provide subnet id created in network terraform in packer.json

packer build packer.json

### Command to run main Terraform

Go in folder terraform, run command: 

1. terraform init

2. terraform plan

3. terraform apply

### Additional notes 

1. When in networkTerraform you need to generate key-pairs:  ssh-keygen -f keyPair (if you change this name, you need to change this in TF files also where that is specified)

2. Be sure to include subnet_id in packer.json when this is returned after running terraform apply in networkTerraform

3. Got some red initially on ssh'ing into ec2 instance so may get this but ami still built and was able to connect