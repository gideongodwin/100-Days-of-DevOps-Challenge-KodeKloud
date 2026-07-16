## Day 94 - Create VPC Using Terraform

## Task Details:

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition.

To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

- Create a VPC named `xfusion-vpc` in region `us-east-1` with any `IPv4` CIDR block through terraform.

- The Terraform working directory is `/home/bob/terraform`. Create the `main.tf` file (do not create a different `.tf` file) to accomplish this task.

    > Right-click under the EXPLORER section in VS Code and select Open in Integrated Terminal to launch the terminal.

## Steps:

1. Right-click under the EXPLORER section >  Open in Integrated Terminal

2. Create the `main.tf` file in the terraform directory
    ```
    touch main.tf
    ```

3. Open the `main.tf` file and paste the following Terraform configuration.
    ```
    resource "aws_vpc" "xfusion_vpc" {
      cidr_block = "10.0.0.0/16"
    
      tags = {
        Name = "xfusion-vpc"
      }
    }
    ```

4. Initialize Terraform
    ```
    terraform init
    ```

5. Review before applying changes
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
