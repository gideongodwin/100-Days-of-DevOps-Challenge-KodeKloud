## Day 96 - Create EC2 Instance Using Terraform

## Task Details:

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. 

To achieve this, they have segmented large tasks into smaller, more manageable units.

For this task, create an EC2 instance using `Terraform` with the following requirements:

- The EC2 instance must use the value `devops-ec2` as its Name tag, which defines the instance name in AWS.

- Use the `Amazon Linux` `ami-0c101f26f147fa7fd` to launch this instance.
  
  - The Instance type must be `t2.micro`.

- Create a new RSA key named `devops-kp`.

- Attach the default (available by default) security group.

- The Terraform working directory is `/home/bob/terraform` Create the `main.tf` file (do not create a different `.tf` file) to provision the instance.

## Steps:  

1. Ensure you're in the correct directory i.e `/home/bob/terraform`
     ```
     pwd
     ```

2. Create the `main.tf` file and paste the following Terraform configuration.
    ```
    # 1. Create a new RSA key
    resource "tls_private_key" "devops_key" {
      algorithm = "RSA"
      rsa_bits  = 4096
    }
    
    # 2. Create the AWS Key Pair using the generated RSA key
    resource "aws_key_pair" "devops_kp" {
      key_name   = "devops-kp"
      public_key = tls_private_key.devops_key.public_key_openssh
    }
    
    # 3. Provision the EC2 Instance
    resource "aws_instance" "devops_ec2" {
      ami             = "ami-0c101f26f147fa7fd"
      instance_type   = "t2.micro"
      key_name        = aws_key_pair.devops_kp.key_name
      
      # Note: By omitting the security_groups or vpc_security_group_ids 
      # attribute, AWS automatically attaches the default security group.
    
      tags = {
        Name = "devops-ec2"
      }
    }
    ```

3. Initialize Terraform
    ```
    terraform init
    ```

4. Validate the configuration
    ```
    terraform validate
    ```

5.  Review before applying changes
    ```
    terraform plan
    ```

6. Apply the configuration
    ```
    terraform apply -auto-approve
    ```

7. Verify the resource
    ```
    terraform state list
    ```
