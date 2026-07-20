## Day 98 - Launch EC2 in Private VPC Subnet Using Terraform

## Task Details:

The Nautilus DevOps team is expanding their AWS infrastructure and requires the setup of a private Virtual Private Cloud (VPC) along with a subnet.

This VPC and subnet configuration will ensure that resources deployed within them remain isolated from external networks and can only communicate within the VPC.

Additionally, the team needs to provision an EC2 instance under the newly created private VPC. This instance should be accessible only from within the VPC, allowing for secure communication and resource management within the AWS environment.

1. Create a VPC named `datacenter-priv-vpc` with the CIDR block `10.0.0.0/16`.

2. Create a subnet named `datacenter-priv-subnet` inside the VPC with the CIDR block `10.0.1.0/24` and `auto-assign` IP option must not be `enabled`.

3. Create an EC2 instance named `datacenter-priv-ec2` inside the subnet and instance type must be `t2.micro`.

4. Ensure the security group of the EC2 instance allows access only from within the VPC's CIDR block.

5. Create the `main.tf` file (do not create a separate `.tf` file) to provision the VPC, subnet and EC2 instance.

6. Use variables.tf file with the following variable names:

    - KKE_VPC_CIDR` for the VPC CIDR block.
    - `KKE_SUBNET_CIDR` for the subnet CIDR block.

7. Use the outputs.tf file with the following variable names:

    - `KKE_vpc_name` for the name of the VPC.
    - `KKE_subnet_name` for the name of the subnet.
    - `KKE_ec2_private` for the name of the EC2 instance.

## Steps:

1. Ensure you're in the correct directory i.e `/home/bob/terraform`
     ```
     pwd
     ```

2. Create the `variables.tf` file and paste the following configuration.
    ```
    vi variables.tf
    ```
     ```
      variable "KKE_VPC_CIDR" {
        description = "CIDR block for the VPC"
        type        = string
        default     = "10.0.0.0/16"
      }
      
      variable "KKE_SUBNET_CIDR" {
        description = "CIDR block for the subnet"
        type        = string
        default     = "10.0.1.0/24"
      }
      ```
    > defines the CIDR blocks for your VPC and Subnet.

3. Create the `main.tf` file and paste the following configuration.
    ```
    vi main.tf
    ```
    ```
    # Dynamically grab the latest Amazon Linux 2 AMI
    data "aws_ami" "amazon_linux" {
      most_recent = true
      owners      = ["amazon"]
    
      filter {
        name   = "name"
        values = ["amzn2-ami-hvm-*-x86_64-gp2"]
      }
    }
    
    # 1. Create the VPC
    resource "aws_vpc" "datacenter_vpc" {
      cidr_block = var.KKE_VPC_CIDR
    
      tags = {
        Name = "datacenter-priv-vpc"
      }
    }
    
    # 2. Create the Subnet (Auto-assign IP disabled)
    resource "aws_subnet" "datacenter_subnet" {
      vpc_id                  = aws_vpc.datacenter_vpc.id
      cidr_block              = var.KKE_SUBNET_CIDR
      map_public_ip_on_launch = false
    
      tags = {
        Name = "datacenter-priv-subnet"
      }
    }
    
    # 3. Create a Security Group restricting access to VPC CIDR only
    resource "aws_security_group" "datacenter_sg" {
      name        = "datacenter-priv-sg"
      description = "Allow internal VPC traffic"
      vpc_id      = aws_vpc.datacenter_vpc.id
    
      ingress {
        description = "Allow all inbound traffic from within VPC"
        from_port   = 0
        to_port     = 0
        protocol    = "-1" # "-1" means all protocols
        cidr_blocks = [var.KKE_VPC_CIDR]
      }
    
      egress {
        description = "Allow all outbound traffic"
        from_port   = 0
        to_port     = 0
        protocol    = "-1"
        cidr_blocks = ["0.0.0.0/0"]
      }
    }
    
    # 4. Create the EC2 Instance
    resource "aws_instance" "datacenter_ec2" {
      ami                    = data.aws_ami.amazon_linux.id
      instance_type          = "t2.micro"
      subnet_id              = aws_subnet.datacenter_subnet.id
      vpc_security_group_ids = [aws_security_group.datacenter_sg.id]
    
      tags = {
        Name = "datacenter-priv-ec2"
      }
    }
    ```
    > this file handles the provider, dynamically fetch the AMI, and build the VPC, Subnet, Security Group, and EC2 instance

4. Create the `outputs.tf` file and paste the following configuration.
    ```
    vi outputs.tf
    ```
    ```
    output "KKE_vpc_name" {
      description = "Name of the VPC"
      value       = aws_vpc.datacenter_vpc.tags["Name"]
    }
    
    output "KKE_subnet_name" {
      description = "Name of the Subnet"
      value       = aws_subnet.datacenter_subnet.tags["Name"]
    }
    
    output "KKE_ec2_private" {
      description = "Name of the EC2 Instance"
      value       = aws_instance.datacenter_ec2.tags["Name"]
    }
    ```

5. Initialize Terraform
    ```
    terraform init
    ```

6. Validate the configuration
    ```
    terraform validate
    ```

7.  Review before applying changes
    ```
    terraform plan
    ```

8. Apply the configuration
    ```
    terraform apply -auto-approve
    ``` 
