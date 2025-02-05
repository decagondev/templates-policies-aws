# Deploying Live Streaming Solution on AWS with Broad Permissions

## Overview

This guide will walk you through the deployment of a live streaming solution on AWS using a CloudFormation template. You'll create a broad IAM policy to grant the necessary permissions for the deployment. This setup is intended for educational environments where the principle of least privilege is relaxed to facilitate learning.

## Prerequisites

- An AWS account
- Access to the AWS Management Console with credentials that allow you to create IAM roles, policies, and CloudFormation stacks.

## Step-by-Step Deployment

### 1. Create an IAM Policy

First, you will create an IAM policy that grants all necessary permissions to deploy and manage the live-streaming resources. The following policy document should be used:

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
        "s3:PutEncryptionConfiguration",
        "s3:ListBucket",
        "s3:PutObject",
        "s3:GetObject",
        "s3:DeleteObject",
        "s3:PutBucketLogging",
        "s3:PutBucketLifecycleConfiguration"
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
        "medialive:CreateChannel",
        "medialive:UpdateChannel",
        "medialive:DeleteChannel",
        "medialive:DescribeChannel",
        "medialive:CreateInput",
        "medialive:DeleteInput",
        "medialive:DescribeInput",
        "medialive:CreateInputSecurityGroup",
        "medialive:DeleteInputSecurityGroup",
        "medialive:DescribeInputSecurityGroup"
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
        "ssm:PutParameter",
        "ssm:GetParameter",
        "ssm:DeleteParameter",
        "ssm:DescribeParameters"
      ],
      "Resource": "*"
    }
  ]
}
```

#### Steps to Create the Policy:

1. Go to the IAM Dashboard in AWS Management Console.
2. Click on **Policies** in the navigation pane.
3. Click the **Create policy** button.
4. Choose **JSON** and paste the above policy document.
5. Click **Review policy**.
6. Enter a policy name, like `LiveStreamingBroadAccessPolicy`.
7. Optionally, provide a description.
8. Click **Create policy** to save it.

### 2. Create an IAM Role

Now, you will create an IAM role that uses this policy:

1. Go to the IAM Dashboard.
2. Click on **Roles** in the navigation pane.
3. Click the **Create role** button.
4. Select **AWS service** and choose **EC2**.
5. Click **Next: Permissions**.
6. Search for and select the `LiveStreamingBroadAccessPolicy` you just created.
7. Click **Next: Tags**, and add optional tags if desired.
8. Click **Next: Review**.
9. Provide a role name, such as `LiveStreamingRole`.
10. Click **Create role**.

### 3. Deploy the CloudFormation Template

With the role and policy ready, you can deploy the CloudFormation template:

1. Navigate to the AWS CloudFormation service.
2. Click on **Create stack** and choose **With new resources (standard)**.
3. Upload your live-streaming CloudFormation template file or specify the Amazon S3 URL where it is stored.
4. Provide a stack name (e.g., `LiveStreamingStack`).
5. Configure the stack options as needed.
6. For the **Specify stack details** section, ensure you input values for parameters such as `InputType`, `EncodingProfile`, and `ChannelStart`.
7. Click **Next** through the rest of the configuration and review pages.
8. Click on **Create stack** to start the deployment.

### 4. Monitoring and Accessing Outputs

- You can monitor the progress of the stack in the CloudFormation console.
- Once the stack deployment is complete, navigate to the **Outputs** tab of the stack to access the relevant resources, URLs, and identifiers for your live streaming setup.