## Day 95 - Create Security Group Using Terraform

## Task Details:

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition.

To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

Use Terraform to create a security group under the default VPC with the following requirements:

1) The name of the security group must be `xfusion-sg`

2) The description must be `Security group for Nautilus App Servers`

3) Add an inbound rule of type `HTTP`, with a port range of `80`, and source CIDR range `0.0.0.0/0`

4) Add another inbound rule of type `SSH`, with a port range of `22`, and source CIDR range `0.0.0.0/0`

     > Ensure that the security group is created in the `us-east-1` region using Terraform. The Terraform working directory is `/home/bob/terraform`. Create the `main.tf` file (do not create a different `.tf` file) to accomplish this task.

## Steps:

1. Ensure you're in the correct directory i.e `/home/bob/terraform`
```
pwd
```

2. Create the `main.tf` file and paste the following Terraform configuration.
```
data "aws_vpc" "default" {
  default = true
}

resource "aws_security_group" "xfusion_sg" {
  name        = "xfusion-sg"
  description = "Security group for Nautilus App Servers"
  vpc_id      = data.aws_vpc.default.id

  ingress {
    description = "HTTP"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    description = "SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
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
