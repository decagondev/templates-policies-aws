# Live Streaming and Video on Demand Solutions on AWS

This repository contains AWS CloudFormation templates and resources to deploy Live Streaming and Video on Demand (VoD) solutions on AWS. These templates provide an educational platform to understand and implement media processing and distribution services using AWS.

## Purpose

The purpose of these templates is to:

- **Live Streaming**: Facilitate the deployment of a live streaming setup using AWS MediaLive, CloudFront, and related services, ideal for real-time content delivery.
- **Video on Demand**: Enable the setup of a Video on Demand solution using AWS MediaConvert, S3, and CloudFront, perfect for delivering pre-recorded media content.

## Documentation

we havce the step by step for each of the templates in the documentation folder:
- **Live Streaming**: [Live Streaming Steps](documentation/deploy-instructions-live-streaming.md)
- **Video on Demand**: [Video Of Demoand Steps](documentation/deploy-instructions-video-on-demand.md)

For detailed setup instructions and additional documentation, please refer to the official AWS Solutions Implementation guides:

- **Live Streaming on AWS**: [AWS Live Streaming Solution Guide](https://docs.aws.amazon.com/solutions/latest/live-streaming/index.html)
- **Video on Demand on AWS**: [AWS Video on Demand Solution Guide](https://docs.aws.amazon.com/solutions/latest/video-on-demand-on-aws/index.html)

These guides provide comprehensive instructions on prerequisites, deployment, and configuration to ensure a successful implementation of each solution.

## Important Notes

- These templates are intended for educational and testing purposes.
- Before using these templates in production, ensure that all security and operational best practices are reviewed and implemented according to your organization's requirements.
- Permissions utilized in the deployment scripts are broad to facilitate learning and should be restricted in live environments. Always follow AWS's least privilege principle.

For additional information and support, visit the respective official AWS documentation or reach out to AWS support.
