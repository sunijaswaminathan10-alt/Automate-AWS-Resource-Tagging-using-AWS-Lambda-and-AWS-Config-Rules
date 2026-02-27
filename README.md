# Automate-AWS-Resource-Tagging-using-AWS-Lambda-and-AWS-Config-Rules
Automatically enforce, audit, and remediate resource tags across your AWS environment using Lambda, EventBridge, and AWS Config.

# Project Overview
This project implements automated governance in AWS by enforcing mandatory tags on EC2 instances using AWS Config, EventBridge, Lambda, and SNS.

When an EC2 instance is launched without required tags (Environment, Owner, CostCenter), the system:

- Detects non-compliance

- Automatically applies missing tags

- Sends email notification to administrators

- Re-evaluates compliance status

This ensures proper cost allocation, ownership tracking, and governance compliance in AWS environments.

# Architecture Services Used

- Amazon EC2

- AWS Config

- Amazon EventBridge

- AWS Lambda

- Amazon SNS

- Amazon CloudWatch

- IAM (Roles & Permissions)

# Architecture Flow Diagram

EC2 Instance (No Tags)
        │
        ▼
AWS Config Rule (Required Tags)
        │
        ▼
Marked as NON_COMPLIANT
        │
        ▼
Amazon EventBridge Rule
        │
        ├───────────────┐
        ▼               ▼
AWS Lambda          Amazon SNS
(Add Required Tags)  (Send Email Alert)
        │
        ▼
AWS Config Re-evaluation
        │
        ▼
Marked as COMPLIANT

# Required Tags Enforced

# Tag Key	                 Purpose
Environment	              Identifies Dev/Test/Production
Owner	                    Identifies the responsible team/person
CostCenter	              Tracks billing allocation

# Example Tags Applied:
  Environment = Production
  Owner = DevOps
  CostCenter = 1234

# Implementation Steps
# 1️. AWS Config Rule

- Created "Required Tags" rule

- Scoped to EC2 Instances

# Required tags:

- Environment

- Owner

- CostCenter

# 2️. EventBridge Rule

- Event Source: aws.config

- Event Type: Compliance Change

- Filter: NON_COMPLIANT

- Targets:

- Lambda (Auto-remediation)

- SNS (Alerting)

# 3️. Lambda Function (Python 3.10)

# The Lambda function:

- Extracts resource ID

- Checks compliance status

- Adds required tags using EC2 API

# 4️. SNS Notification

- Created SNS Topic

- Subscribed email endpoint

- Sends real-time alert for NON_COMPLIANT resources

# 5️. CloudWatch Logs

Used to verify successful tagging:

Ex: Successfully tagged EC2 instance

# Use Case

In enterprise environments:

- Developers may launch resources without proper tagging

- Finance teams cannot track billing accurately

- Security teams cannot identify ownership

This solution ensures:

--> Automated governance enforcement
--> Cost tracking compliance
--> Real-time alerting
--> Reduced manual intervention

# Screenshots Included

## AWS Config rule configuration

## EventBridge rule configuration

## Lambda function setup

## SNS topic & subscription

## EC2 before tagging

## EC2 after auto-tagging

## CloudWatch logs

## Email notification sample
