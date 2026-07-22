## Day 100 - Create and Configure Alarm Using CloudWatch Using Terraform

## Task Details:

The Nautilus DevOps team has been tasked with setting up an EC2 instance for their application. To ensure the application performs optimally, they also need to create a CloudWatch alarm to monitor the instance's CPU utilization

The alarm should trigger if the CPU utilization exceeds 90% for one consecutive 5-minute period. To send notifications, use the SNS topic named `datacenter-sns-topic`, which is already created.

- Launch EC2 Instance: Create an EC2 instance named `datacenter-ec2` using any appropriate Ubuntu AMI (you can use AMI `ami-0c02fb55956c7d316`).

- Create CloudWatch Alarm: Create a CloudWatch alarm named `datacenter-alarm` with the following specifications:

    - Statistic: Average
    - Metric: CPU Utilization
    - Threshold: >= 90% for 1 consecutive 5-minute period
    - Alarm Actions: Send a notification to the `datacenter-sns-topic` SNS topic.

- Update the `main.tf` file (do not create a separate .tf file) to create a EC2 Instance and CloudWatch Alarm.

- Create an `outputs.tf` file to output the following values:

    - `KKE_instance_name` for the EC2 instance name.
    - `KKE_alarm_name` for the CloudWatch alarm name.

Before submitting the task, ensure that terraform plan returns No changes. Your infrastructure matches the configuration.

## Steps:

1. Ensure you're in the correct directory i.e `/home/bob/terraform`
     ```
     pwd
     ```

2. Open the `main.tf` and add the following configurations
    ```
    vi main.tf
    ```
    ```
    # Fetch the existing SNS topic
    data "aws_sns_topic" "sns_topic" {
      name = "datacenter-sns-topic"
    }
    
    # Create the EC2 instance
    resource "aws_instance" "ec2_instance" {
      ami           = "ami-0c02fb55956c7d316"
      instance_type = "t2.micro" # Standard free-tier instance type
    
      tags = {
        Name = "datacenter-ec2"
      }
    }
    
    # Create the CloudWatch Metric Alarm
    resource "aws_cloudwatch_metric_alarm" "cpu_alarm" {
      alarm_name          = "datacenter-alarm"
      comparison_operator = "GreaterThanOrEqualToThreshold"
      evaluation_periods  = 1
      metric_name         = "CPUUtilization"
      namespace           = "AWS/EC2"
      period              = 300 # 5 minutes in seconds
      statistic           = "Average"
      threshold           = 90
      alarm_description   = "Monitor EC2 CPU utilization and trigger at 90%"
      
      # Trigger the alarm action to the existing SNS topic
      alarm_actions       = [data.aws_sns_topic.sns_topic.arn]
    
      # Link the alarm to the specific EC2 instance
      dimensions = {
        InstanceId = aws_instance.ec2_instance.id
      }
    }
    ```

3. Create the `outputs.tf` file and add the following configurations
    ```
    vi outputs.tf
    ```
    ```
    output "KKE_instance_name" {
      description = "The EC2 instance name"
      value       = aws_instance.ec2_instance.tags["Name"]
    }
    
    output "KKE_alarm_name" {
      description = "The CloudWatch alarm name"
      value       = aws_cloudwatch_metric_alarm.cpu_alarm.alarm_name
    }
    ```

4.  Initialize Terraform
    ```
    terraform init
    ```

5.  Review before applying changes
    ```
    terraform plan
    ```

6. Apply the configuration
    ```
    terraform apply -auto-approve
    ```
7. You should see: "No changes. Your infrastructure matches the configuration."
    ```
    terraform plan
    ```
