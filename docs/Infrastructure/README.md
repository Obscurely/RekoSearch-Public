# Infrastructure

Here you will find documentation about the infrastructure choices made and how everything connects.

<!--toc:start-->

- [Terraform](#terraform)
- [AWS](#aws)
  - [AWS Flow](#aws-flow)
    - [CDN](#cdn)
    - [Authentication](#authentication)
    - [API](#api)
    - [API Routes](#api-routes)
    - [Other](#other)
- [Kubernetes](#kubernetes)
<!--toc:end-->

## Terraform

At the core of everything sits Terraform. The infrastructure is too complicated to replicate by even looking at a live implementation and trying to copy it over.

## AWS

I chose AWS (Amazon Web Services) because I have two certifications related to it and am most comfortable and knowledgeable about it.

### AWS Flow

#### CDN

At the forefront of the setup are Route53 and CloudFront, serving as the CDN and DNS router for the application. A proper AWS WAF (Firewall) is in place to ensure that bad actors are blocked, and only individuals from authorized regions can access the Dashboard.

#### Authentication

For authentication, I am using AWS Cognito with the OAuth 2.0 flow, ensuring maximum security and best practices.

#### API

For the API, I use API Gateway with the simple HTTP API version, having designed an RPC API.

The reasons for not using a REST API are cost-related, as running the bare bones HTTP API provides much lower costs at the expense of not having a more advanced API, which in this case is not a problem, as it's quite simple.

#### API Routes

All of the API Routes resolve to AWS Lambda or ARM, as it is incredibly cheap to run and is more than enough for any of the APIs.

#### Other

- S3 for storing files and accessing them fast.
- DynamoDB for storing job and user data.
- SQS for queuing jobs.
- SES for emails.
- Event Bridge for handling when all the files for a job have been uploaded
- Rekognition, Textract, and Transcribe are used for processing the files.
- CloudWatch for metrics and logs.
- ACM for certificates
- IAM for security

## Kubernetes

For hosting the Frontend, Job Processor, Queue Processor, Stats Dashboard, and Analytics Dashboard, I have decided to go with a Kubernetes cluster because I am very comfortable with Kubernetes (I even have the CKAD), it's cloud agnostic if I ever decide to switch things. It allows me to manage them better.

See [K3S.md](./K3S.md) for more information about the K3S cluster.
