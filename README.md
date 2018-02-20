## AWS Developer Workshop

This is a workshop to get developers started on AWS using the cloud native primitives. This workshop is designed as a self paced lab which incrementally increases in expertise

We will build a simple web app based on microservices using the 12 factor methodology, deploy it on the cloud and try some debug steps.

We will do this workshop in a pair programming mode. So find a buddy.

**Pre-requisite**

1. [Setup AWS account ](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)
1. [SetUp Development Environment](http://docs.aws.amazon.com/codestar/latest/userguide/getting-started.html)

The modules build on each other and are intended to be executed linearly.

## Theme A - **Serverless application**

|Module| Description |
|--|--|
|[Writing your first AWS Lambda Function on AWS Cloud9](https://amazon.awsapps.com/workdocs/index.html#/document/f589ed8c8010f39de92c2ae0a4ee7472848d94e5345a2c07d4ca6e795b08343c)|Add a new service using SAM Local to a serverless application which was created by from AWS CodeStar|
|[Deploying Your Function using AWS SAM and AWS CodeDeploy](https://amazon.awsapps.com/workdocs/index.html#/document/f589ed8c8010f39de92c2ae0a4ee7472848d94e5345a2c07d4ca6e795b08343c)|Deploy Function to Cloud using AWS developer Tools.|
|[Debugging and Monitoring your function](https://amazon.awsapps.com/workdocs/index.html#/document/f589ed8c8010f39de92c2ae0a4ee7472848d94e5345a2c07d4ca6e795b08343c)|Debug and monitor your application using Cloud9, CodeStar and xRay and Cloudwatch |
|[Build a Continuous Deployment Pipeline]((https://aws.amazon.com/blogs/compute/implementing-canary-deployments-of-aws-lambda-functions-with-alias-traffic-shifting/))|Using AWS CodeCommit, AWS CodePipeline, and AWS CodeBuild, create a continuous deployment pipeline to automatically deploy changes to our application|

## Theme B -  **Containerized application**

|Module| Description |
|--|--|
| [Getting Started with Amazon ECS using AWS Fargate](http://running-containers-on-aws-fargate.s3-website-us-east-1.amazonaws.com/getting-started-with-amazon-ecs-using-aws-fargate.html) | Create a new Amazon ECS cluster using the AWS Management Console. At the end of this module, we’ll have a new ECS cluster and supporting infrastructure such as a VPC and subnets and a small Hello World application running |
|[Create a Docker Image Repository](http://running-containers-on-aws-fargate.s3-website-us-east-1.amazonaws.com/create-a-docker-image-repository.html)|Create a new Docker registry repository for workshop images in Amazon ECR.
|[Build and Push a Docker Image](http://running-containers-on-aws-fargate.s3-website-us-east-1.amazonaws.com/build-and-push-a-docker-image.html)|Fork a sample application from GitHub which uses an Amazon DynamoDB table to store notable quotations and build it as a Docker container image and push it to your new Docker image repository.
|[Create a Service](http://running-containers-on-aws-fargate.s3-website-us-east-1.amazonaws.com/create-a-service.html)|Fork a sample application from GitHub which uses an Amazon DynamoDB table to store notable quotations and build it as a Docker container image and push it to your new Docker image repository.
|[Build a Continuous Deployment Pipeline](http://running-containers-on-aws-fargate.s3-website-us-east-1.amazonaws.com/build-a-continuous-deployment-pipeline.html)|Using AWS CodeCommit, AWS CodePipeline, and AWS CodeBuild, create a continuous deployment pipeline to automatically deploy changes to our application|

## **Advanced Topics**

|Module| Description |
|--|--|
|[Cross Regions/Cross Account Pipeline](https://aws.amazon.com/blogs/devops/building-a-cross-regioncross-account-code-deployment-solution-on-aws/)|Build an automated cross-region code deployment solution using AWS CodePipeline, AWS CodeDeploy , and AWS Lambda |
|[Deploying Deep Learning Functions on ECS](https://github.com/awslabs/ecs-mxnet-example)|Create an automated workflow that will provision, configure and orchestrate a pipeline triggering deployment of any changes to your AI model or application code.|
|[Deploying Deep Learning Functions on Lambda](https://github.com/awslabs/mxnet-lambda)|Predict labels along with their probablities for an image using a pre-trained model with Apache MXNet deployed on AWS Lambda|
|[Containers - Blue-Green Deployment](https://github.com/awslabs/ecs-canary-blue-green-deployment)|Execute a canary deployment for Amazon EC2 Container Service. In order to provide an automated and safe method of migrating traffic from a blue deployment to a green one, this solution leverages Route53 weights to adjust the traffic flow from one ECS service to another.|
## License

This repository contains multiple directories, each individually licensed. Please see the LICENSE file in each directory. 
