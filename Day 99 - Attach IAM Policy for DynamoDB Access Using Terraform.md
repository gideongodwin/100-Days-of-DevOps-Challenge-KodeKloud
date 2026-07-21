## Day 99 - Attach IAM Policy for DynamoDB Access Using Terraform

## Task Details:

The DevOps team has been tasked with creating a secure DynamoDB table and enforcing fine-grained access control using IAM. This setup will allow secure and restricted access to the table from trusted AWS services only.

As a member of the Nautilus DevOps Team, your task is to perform the following using Terraform:

- Create a DynamoDB Table: Create a table named `xfusion-table` with minimal configuration.

- Create an IAM Role: Create an IAM role named `xfusion-role` that will be allowed to access the table.

- Create an IAM Policy: Create a policy named `xfusion-readonly-policy` that should grant read-only access (GetItem, Scan, Query) to the specific DynamoDB table and attach it to the role.

- Create the `main.tf` file (do not create a separate `.tf` file) to provision the table, role, and policy.

- Create the `variables.tf` file with the following variables:

    `KKE_TABLE_NAME:` name of the DynamoDB table
  
    `KKE_ROLE_NAME:` name of the IAM role
  
    `KKE_POLICY_NAME:` name of the IAM policy
  

- Create the outputs.tf file with the following outputs:

    `kke_dynamodb_table:` name of the DynamoDB table
    
    `kke_iam_role_name:` name of the IAM role
    
    `kke_iam_policy_name:` name of the IAM policy

- Define the actual values for these variables in the `terraform.tfvars` file.

Ensure that the `IAM policy` allows only read access and restricts it to the specific `DynamoDB` table created.

## Steps:

1. Ensure you're in the correct directory i.e `/home/bob/terraform`
     ```
     pwd
     ```

2. Create the `variables.tf` file to define the required variables for your resource names..
    ```
    vi variables.tf
    ```
    ```
    variable "KKE_TABLE_NAME" {
      description = "name of the DynamoDB table"
      type        = string
    }
    
    variable "KKE_ROLE_NAME" {
      description = "name of the IAM role"
      type        = string
    }
    
    variable "KKE_POLICY_NAME" {
      description = "name of the IAM policy"
      type        = string
    }
    ```

3. Create the `terraform.tfvars` file to assign the actual values.
    ```
    vi terraform.tfvars
    ```
    ```
    KKE_TABLE_NAME  = "xfusion-table"
    KKE_ROLE_NAME   = "xfusion-role"
    KKE_POLICY_NAME = "xfusion-readonly-policy"
    ```

4. Create the `outputs.tf` file to explicitly return the names of the resources once they are created.
    ```
    vi outputs.tf
    ```
    ```
    output "kke_dynamodb_table" {
      description = "name of the DynamoDB table"
      value       = aws_dynamodb_table.xfusion_table.name
    }
    
    output "kke_iam_role_name" {
      description = "name of the IAM role"
      value       = aws_iam_role.xfusion_role.name
    }
    
    output "kke_iam_policy_name" {
      description = "name of the IAM policy"
      value       = aws_iam_policy.xfusion_policy.name
    }
    ```

5. Create the `main.tf` file
    ```
    # 1. DynamoDB Table with minimal configuration
    resource "aws_dynamodb_table" "xfusion_table" {
      name         = var.KKE_TABLE_NAME
      billing_mode = "PAY_PER_REQUEST"
      hash_key     = "id"
    
      attribute {
        name = "id"
        type = "S"
      }
    }
    
    # 2. IAM Role allowing trusted AWS services (e.g., EC2)
    resource "aws_iam_role" "xfusion_role" {
      name = var.KKE_ROLE_NAME
    
      assume_role_policy = jsonencode({
        Version = "2012-10-17"
        Statement = [
          {
            Action = "sts:AssumeRole"
            Effect = "Allow"
            Principal = {
              Service = "ec2.amazonaws.com"
            }
          }
        ]
      })
    }
    
    # 3. IAM Policy for Read-Only access specifically restricted to the table
    resource "aws_iam_policy" "xfusion_policy" {
      name        = var.KKE_POLICY_NAME
      description = "Read-only access to specific DynamoDB table"
    
      policy = jsonencode({
        Version = "2012-10-17"
        Statement = [
          {
            Effect = "Allow"
            Action = [
              "dynamodb:GetItem",
              "dynamodb:Scan",
              "dynamodb:Query"
            ]
            # Restricts access directly to the ARN of the table created above
            Resource = aws_dynamodb_table.xfusion_table.arn 
          }
        ]
      })
    }
    
    # 4. Attach the IAM Policy to the IAM Role
    resource "aws_iam_role_policy_attachment" "xfusion_attach" {
      role       = aws_iam_role.xfusion_role.name
      policy_arn = aws_iam_policy.xfusion_policy.arn
    }
    ```
      > This file provisions the DynamoDB table with a minimal configuration (Pay-Per-Request billing), an IAM role trusted by AWS services (using EC2 as the trusted entity), the strictly scoped read-only IAM policy, and the attachment linking the policy to the role.
6. Initialize Terraform
    ```
    terraform init
    ```

7.  Review before applying changes
    ```
    terraform plan
    ```

8. Apply the configuration
    ```
    terraform apply -auto-approve
    ```
9. Confirm there are "No changes. Your infrastructure matches the configuration."
    ```
    terraform plan
    ```
