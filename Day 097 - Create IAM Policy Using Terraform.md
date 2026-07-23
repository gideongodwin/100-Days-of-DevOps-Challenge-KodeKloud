## Day 97 - Create IAM Policy Using Terraform

## Task Details:

When establishing infrastructure on the AWS cloud, Identity and Access Management (IAM) is among the first and most critical services to configure. IAM facilitates the creation and management of user accounts, groups, roles, policies, and other access controls.

The Nautilus DevOps team is currently in the process of configuring these resources and has outlined the following requirements.

Create an IAM policy named `iampolicy_anita` in `us-east-1` region using Terraform. It must allow read-only access to the EC2 console, i.e., this policy must allow users to view all instances, AMIs, and snapshots in the Amazon EC2 console.

The Terraform working directory is `/home/bob/terraform`. Create the `main.tf` file (do not create a different `.tf` file) to accomplish this task.

## Steps:

1. Ensure you're in the correct directory i.e `/home/bob/terraform`
     ```
     pwd
     ```

2. Create the `main.tf` file and paste the following Terraform configuration.
    ```
    resource "aws_iam_policy" "iampolicy_anita" {
      name        = "iampolicy_anita"
      description = "Provides read-only access to the EC2 console"
    
      policy = jsonencode({
        Version = "2012-10-17"
        Statement = [
          {
            Effect   = "Allow"
            Action   = [
              "ec2:Describe*"
            ]
            Resource = "*"
          }
        ]
      })
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
