---
title: "2 – Build images in a fast and repeatable way"
weight: 10
---

In this module we use the AWS Cloud Development Kit (CDK) to define a deployment pipeline to host hosts an application that builds Yocto images in a fast and repeatable way. 

### What is the AWS Cloud Development Kit (CDK)?

The AWS Cloud Development Kit (CDK) is a software development framework for defining cloud infrastructure in code and provisioning it through AWS CloudFormation. The AWS CDK lets you easily define applications in the AWS Cloud using your programming language of choice.  Creating a new application is just the first step. Applications constantly evolve and changes need to be made to them. Tools like AWS CodeCommit, AWS CodeBuild, AWS CodeDeploy, and AWS CodePipeline and work together to create a deployment pipeline for your application. 
CDK Pipelines is a construct library module for continuous delivery of AWS CDK applications. Whenever you check your AWS CDK app's source code in to AWS CodeCommit, GitHub, or BitBucket, CDK Pipelines can automatically build, test, and deploy your new version.
CDK Pipelines are self-updating: if you add new application stages or new stacks, the pipeline automatically reconfigures itself to deploy those new stages and/or stacks.

Note: CDK Pipelines is currently in developer preview, and its API is subject to change. Breaking API changes will be announced in the AWS CDK Release Notes.
https://github.com/aws/aws-cdk/releases

{{% notice note %}}
You must have a GitHub account to fork an existing repo. If you do not have an account create one by following these instructions:[here](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account)
{{% /notice %}}


### Step - Get the reference implementation for continuous integration for meta-aws

The meta-aws-ci project was built to provide mechanisms for meta-aws and meta-aws-demos continuous integration and pull request verification. It can also be used to provide mechanisms for OEM/ODM customers wanting to streamline Embedded Linux delivery. In addition, it provides a reference implementation that illustrates how to integrate and maintain AWS device software throughout the IoT product lifecycle.


{{% notice warning %}}
You must have a GitHub account to fork an existing repo. If you do not have an account create one by following these instructions:[here](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account)
{{% /notice %}}


1. Using your web browser navigate to the __aws/meta-aws-ci__ repository.

2. Click __Fork__ button in the top-right corner of the page and choose your user name

### Step 2 - Get GitHub and Docker Hub secrets in your account

1. A Gihub token is used to by the pipeline Stack and the Iiage builder when interacting with Github. On your Github account, go to __Settings → Developer Settings → Personal access tokens__ and generate a new token. The token should have __workflow__ scope selected

![GitHub personal access tokens](/images/02_build_images_github_personal_token.png)

2. Create a new secret by going to __AWS Console → AWS Secrets Manager__ and click on __Store a new secret__ then choose __Other type of secrets__, click on the __Plantext__ tab and copy/paste your GitHub personal token in the text box. This secret needs to be named `github_personal_token`

![GitHub personal access tokens](/images/02_build_images_secrets_github.png) 

3. DockerHub credentials are used by the image builder when pulling upstream images from Docker Hub. Create a new secret by going to __AWS Console → AWS Secrets Manager__ and click on __Store a new secret__ then choose __Other type of secrets__, click on the __Secret key/value__ tab and create a `username` and `password` key/value pair. This secret needs to be named `dh` 

![GitHub personal access tokens](/images/02_build_images_secrets_dockerhub.png) 

### Step 3 - Compile and deploy the CDK project

1. Clone the project

```
git clone git@github.com:franccan/meta-aws-ci.gi
```

2. Navigate to the __cdk__ directory and install dependencies

```
cd meta-aws-ci/cdk
npm update
```

3. Deploy the project

```
cdk deploy
```

### Step 4 - download the image from S3

```
aws s3 cp 
```