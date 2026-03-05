# Atlantis

## 63Klabs Atlantis Templates and Scripts Platform for Serverless Deployments on AWS

Ready-to-deploy-and-run:

- **Infrastructure as Code (IaC)** - Library of CloudFormation Templates and Application Starter Code maintained by platform engineers with best practices in security, observability, and well-architected design patterns built in.
- **Continuous Integration/Continuous Deployment/Delivery (CI/CD)** - AWS CodePipeline or GitHub Actions automation scripts and tests to ensure GitOps and reliable deployments.
- **Enhanced SAM Configuration management** - Advanced scripts make deploying infrastructure such as pipelines and storage easy, maintainable, and scalable without shadow databases or data stores. Uses a config repository and AWS API to check the current state of your infrastructure in real-time.
- **Tutorials** - Documentation and step-by-step tutorials assist in learning not only how to use Atlantis, but also how to develop and deploy production-level serverless applications using CI/CD, IaC, and the Well-Architected Framework. Even if your organization doesn't use Atlantis as its production platform, it is an easy way to teach, learn, and experiment.

## Use Public Repository or Self-Host

Getting started is simple; it starts with a SAM Configuration repository. Connections to public CloudFormation libraries and application starter code are all available from the command line.

This makes learning and experimentation quick and easy for small shops, individuals, and those just starting out.

Over time, you can add your own templates using your own private repositories alongside the public repositories. Or move it all in-house and self-host the entire platform.

## Get Started

To start, all you need is a single Atlantis SAM Config Repository, as everything flows from there.

**If you are a developer** and your organization is already using Atlantis, the place to start is to clone your organization's private Atlantis SAM Configuration repository and follow the:\
**Instructions for Developers:** Setting Up Your Organization's Atlantis SAM Config Repo on Your Local Machine. 

**If you are an individual, cloud engineer, or instructor** setting up or evaluating Atlantis for personal, organizational, team, or classroom use, then follow the:\
**Instructions for Account Owners**: Setting Up Your Organization's Atlantis SAM Config Repository.

## Tutorials

[Tutorials are available](https://github.com/63Klabs/atlantis-tutorials) to help you use the Application Starter Code.

## Application Starters

Unsure of what to build or how to start?

Atlantis makes it easy with fully functional serverless solutions for Web APIs written in Node and Python, already instrumented with X-Ray, caching, logging, and alarms.

From within your organization's SAM Config repository, run the script:

```bash
./cli/create_repo.py your-repo-name
```

The script will then ask you to choose which application starter to use and will seed your repository with that code!

Then, configure and deploy an AWS CodePipeline or GitHub Action to deploy your new application:

```bash
./cli/config.py pipeline <prefix> your-cool-app test
```

Finally, clone your application repository and get started coding! Commit and push your change to the  `test` branch, and the deployment pipeline kicks in!

GitOps and Best Practices from the start!

### Available Application Starters

- [00 Basic API Gateway with Lambda Function Written in Node.js](https://github.com/63Klabs/atlantis-starter-00-basic-apigw-lambda-nodejs)
- [01 Basic API Gateway with Lambda Function Written in Python](https://github.com/63Klabs/atlantis-starter-01-basic-apigw-lambda-py)
- [02 API Gateway with Lambda utilizing 63klabs/cache-data Written in Node.js](https://github.com/63Klabs/atlantis-starter-02-apigw-lambda-cache-data-nodejs)
- [Serverless Multi-Bucket CloudFront Invalidation Service](https://github.com/63Klabs/atlantis-starter-03-serverless-cloudfront-cache-invalidation)

### 3rd Party Application Starters

- [Serverless Video Conversion using AWS Elemental MediaConvert](https://github.com/chadkluck/serverless-video-converter) (chadkluck/serverless-video-converter)

### Host Your Own Application Starters

You can add `--source` to the `create_repo.py` command and bring in code from any GitHub repository, a hosted ZIP file from S3, or a ZIP file stored locally.

Your organization can also configure the `create_repo.py` script to automatically list starter code from your internal S3 buckets.

## CloudFormation Templates

Each application includes an application template to deploy your application's CloudFormation stack.

However, there is a central repository for deploying supporting infrastructure, such as pipelines, storage, and networking stacks.

- **Pipeline**: Allows users to set up pipelines that perform automated deployments when they commit and push code to GitHub or CodeCommit.
- **Storage**: Allows users to deploy S3 buckets and DynamoDB infrastructure outside of an application stack for caching or static web hosting.
- **Networking**: Allows users to deploy CloudFront and Route53 resources.

These are templates not typically managed by developers but rather by DevOps and Platform Engineering teams. While made available to developers through the `config.py` script, they are not directly editable by developers. This reduces cognitive load and allows each team to focus on their area of expertise while ensuring all developers have access to the most current, validated, organization-approved infrastructure templates.

If a platform engineering team updates a template, it is placed in a central S3 bucket, which is consumed by the `config.py` script. When the `config.py` script is run, it checks the current version and notifies the developer if a new version exists. They can either choose to update or continue with the older version.

By default, the templates are sourced from the 63klabs S3 bucket. All templates are available for review from [Atlantis CloudFormation Template Repository for Serverless Deployments on AWS](https://github.com/63Klabs/atlantis-cfn-template-repo-for-serverless-deployments). Organizations are free to copy, host, and maintain the repository and S3 bucket internally.

## Roles and Security Built-In

Separation of Stacks by Concern and Principle of Least Privilege

For developers or engineers to deploy infrastructure stacks from the SAM Config repository, they must have the appropriate permissions.

1. For the `create_repo.py` script, users will need access to manage CodeCommit repositories (Create, Modify, Tag (Delete is optional)).
2. For the `config.py` script, users will need read access to the S3 bucket that houses the templates, and read access to CodeCommit repositories (including tags).
3. For the `deploy.py` script, users will need to have permission to PASS the appropriate Atlantis service role for:
   - pipeline management
   - storage management
   - networking management

A user may possess permission for any or all of the actions above. You may let a developer run the scripts to create repositories and deploy pipelines and storage, but not to deploy network resources. 

Scripts automatically support the `--profile` option for AWS and SAM CLI commands, as well as the `aws sso login` process for expired credentials.

Templates and starter code already include best practices in security and permissions, with ready-to-use, scoped-down Lambda Execution roles, SSM Parameter and Secrets Manager integration, and resource naming and tagging policies to use with any number of permission sets.
