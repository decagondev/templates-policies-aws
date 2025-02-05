# Deploying Video on Demand (VoD) Solution on AWS with Broad Permissions

## Overview

This guide provides step-by-step instructions for deploying a Video on Demand solution on AWS using a CloudFormation template. You will create an IAM policy with broad permissions, suitable for educational and learning environments.

## Prerequisites

- An AWS account
- Access to the AWS Management Console with the ability to create IAM roles, policies, and CloudFormation stacks.

## Step-by-Step Deployment

### 1. Create an IAM Policy

First, you'll need to create an IAM policy that grants broad permissions necessary for deploying and operating the VoD resources. Use the policy below:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cloudformation:CreateStack",
        "cloudformation:UpdateStack",
        "cloudformation:DeleteStack",
        "cloudformation:DescribeStacks",
        "cloudformation:ListStackResources",
        "cloudformation:DescribeStackEvents",
        "cloudformation:GetTemplate"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:CreateBucket",
        "s3:PutBucketPolicy",
        "s3:GetBucketPolicy",
        "s3:ListBucket",
        "s3:PutObject",
        "s3:GetObject",
        "s3:DeleteObject",
        "s3:PutBucketLogging",
        "s3:PutBucketCors"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "cloudfront:CreateDistribution",
        "cloudfront:UpdateDistribution",
        "cloudfront:GetDistribution",
        "cloudfront:GetDistributionConfig",
        "cloudfront:DeleteDistribution"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "mediaconvert:DescribeEndpoints",
        "mediaconvert:CreateJob",
        "mediaconvert:GetJob"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "iam:CreateRole",
        "iam:AttachRolePolicy",
        "iam:PutRolePolicy",
        "iam:DeleteRole",
        "iam:GetRole",
        "iam:PassRole"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "lambda:CreateFunction",
        "lambda:InvokeFunction",
        "lambda:DeleteFunction",
        "lambda:GetFunction",
        "lambda:UpdateFunctionCode",
        "lambda:UpdateFunctionConfiguration",
        "lambda:AddPermission",
        "lambda:RemovePermission"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents",
        "logs:DescribeLogStreams",
        "logs:DescribeLogGroups"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "sns:CreateTopic",
        "sns:Publish",
        "sns:Subscribe",
        "sns:DeleteTopic",
        "sns:GetTopicAttributes",
        "sns:SetTopicAttributes"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "events:PutRule",
        "events:DeleteRule",
        "events:DescribeRule",
        "events:PutTargets",
        "events:RemoveTargets"
      ],
      "Resource": "*"
    }
  ]
}
```

#### Steps to Create the Policy:

1. Navigate to the IAM Dashboard in the AWS Management Console.
2. Click on **Policies** in the left navigation pane.
3. Click the **Create policy** button.
4. Select the **JSON** tab, and paste the policy document above.
5. Click **Review policy**.
6. Enter a name for the policy, such as `VODBroadAccessPolicy`.
7. Optionally, add a description.
8. Click **Create policy** to create the policy.

### 2. Create an IAM Role

Next, you will create an IAM role and attach the policy you just created:

1. In the IAM Dashboard, click on **Roles** from the left navigation pane.
2. Click the **Create role** button.
3. Choose **AWS service** and select **EC2**.
4. Click **Next: Permissions**.
5. Find and select the `VODBroadAccessPolicy`.
6. Click **Next: Tags** to add any optional tags.
7. Click **Next: Review**.
8. Name the role, such as `VODRole`.
9. Click **Create role**.

### 3. Deploy the CloudFormation Template

With the role and policy ready, you can proceed to deploy the CloudFormation template:

1. Open the AWS CloudFormation console.
2. Click on **Create stack** and select **With new resources (standard)**.
3. Choose to upload your template file or specify the Amazon S3 URL where the template is stored.
4. Assign a name to your stack, like `VODStack`.
5. Configure the stack options as required, and make sure to input values for parameters such as `emailAddress`.
6. Review your configurations as you proceed through the steps.
7. Click **Create stack** to initiate the deployment.

### 4. Monitoring and Accessing Outputs

- Monitor the deployment progress from the CloudFormation console.
- Once complete, view the **Outputs** tab of the stack to access endpoint URLs and other important resource identifiers for your Video on Demand setup.