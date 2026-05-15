# Atlantis Templates and Scripts Platform

## 63Klabs Atlantis Templates and Scripts Platform for Serverless Application Development and Deployment on AWS

Atlantis is a free and open source platform that provides opinionated templates, scripts, starter code, and design patterns to build, maintain, and deploy serverless applications providing best practices in security, observability, and performance. The platform promotes [Infrastructure as Code](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/infrastructure-as-code.html), [Principle of Least Privilege](https://docs.aws.amazon.com/prescriptive-guidance/latest/least-privilege-cloudformation/best-practices.html), and the [Well Architected Framework](https://aws.amazon.com/architecture/well-architected/) as models for development and deployment.

## Ready-to-deploy-and-run

- **Infrastructure as Code (IaC)** - Library of CloudFormation Templates and Application Starter Code maintained by platform engineers with best practices in security, observability, and well-architected design patterns built in.
- **Continuous Integration/Continuous Deployment/Delivery (CI/CD)** - AWS CodePipeline or GitHub Actions automation scripts and tests to ensure GitOps and reliable deployments.
- **Enhanced SAM Configuration management** - Advanced scripts make deploying infrastructure such as pipelines and storage easy, maintainable, and scalable without shadow databases or data stores. Uses a config repository and AWS API to check the current state of your infrastructure in real-time.
- **Tutorials** - Documentation and step-by-step tutorials assist in learning not only how to use Atlantis, but also how to develop and deploy production-level serverless applications using CI/CD, IaC, and the Well-Architected Framework. Even if your organization doesn't use Atlantis as its production platform, it is an easy way to teach, learn, and experiment.
- **MCP Server** - AI-assisted development tools to discover, validate, and utilize CloudFormation templates, starter code, and documentation.

## Provisions

The Atlantis Platform consists of:
- [SAM Configuration Scripts](https://github.com/63Klabs/atlantis-sam-config-scripts)
- [Infrastructure Templates](https://github.com/63Klabs/atlantis-sam-templates)
- [Atlantis MCP Server](https://github.com/63Klabs/atlantis-mcp)
- [Application Starter Code](./README.md#application-starters)

The [Atlantis Platform Administration for Organizations](https://github.com/63Klabs/atlantis-platform-admin) repository provides instructions to Platform Engineering and Developer Experience teams for provisioning Atlantis within your organization.

## Free, Open Source, Easy to Start

Getting started is simple; it starts with a SAM Configuration repository. Connections to public CloudFormation libraries and application starter code are all available from the command line. 

Templates and scripts are pulled from the public 63Klabs repositories, there is no platform to manage.

This makes learning and experimentation quick and easy for small shops, individuals, and those just starting out.

Over time, you can develop your own private and custom templates to use alongside the public repositories. 

Or, you can move it all in-house and self-host the entire platform (including the MCP server).

## Get Started

To start, provide a private [Atlantis SAM Config Scripts](https://github.com/63Klabs/atlantis-sam-config-scripts) repository within your organization for developers to access, configure application repos, and deploy application pipelines.

**If you are a DEVELOPER** and your organization is already using Atlantis, the place to start is cloning your organization's internal Atlantis SAM Configuration repository. Follow the `docs/getting-started-for-developers.md` file found in the repository.

**If you are an ADMINISTRATOR (personal, cloud engineer, or instructor)** setting up or evaluating Atlantis for personal, organizational, team, or classroom use, then review [Atlantis Platform Administration for Organizations](https://github.com/63Klabs/atlantis-platform-admin) repository for instructions and scripts to provision access to your developers.

## Tutorials

[Tutorials are available](https://github.com/63Klabs/atlantis-tutorials) to help you use the Application Starter Code and get the most out of the Atlantis Platform.

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

You can also add the [Atlantis MCP Server](https://mcp.atlantis.63klabs.net) to your AI Assistant, tell it what you want to develop using the Atlantis Platform and it will provide recomendations for what starter code to use and how it can be modified to suit your needs!

### Available Application Starters

- [00 Basic API Gateway with Lambda Function Written in Node.js](https://github.com/63Klabs/atlantis-starter-00-basic-apigw-lambda-nodejs)
- [01 Basic API Gateway with Lambda Function Written in Python](https://github.com/63Klabs/atlantis-starter-01-basic-apigw-lambda-py)
- [02 API Gateway with Lambda utilizing 63klabs/cache-data Written in Node.js](https://github.com/63Klabs/atlantis-starter-02-apigw-lambda-cache-data-nodejs)
- [03 Scheduled CodeBuild Container](https://github.com/63Klabs/atlantis-starter-03-serverless-codebuild-container)

### Built on Atlantis: *Ready-to-Deploy-and-Run*

- [Atlantis MCP Server](https://github.com/63klabs/atlantis-mcp) (63klabs/atlantis-mcp)
- [Serverless Multi-Bucket CloudFront Invalidation Service](https://github.com/63Klabs/serverless-cloudfront-cache-invalidation) (63klabs/serverless-cloudfront-cache-invalidation)
- [Serverless Video Conversion using AWS Elemental MediaConvert](https://github.com/chadkluck/serverless-video-converter) (chadkluck/serverless-video-converter)
- [Serverless Image Resizing using Sharp on Lambda](https://github.com/chadkluck/serverless-image-resizer) (chadkluck/serverless-image-resizer)
- [Serverless Remote Falcon API Proxy](https://github.com/chadkluck/serverless-remote-falcon-api-proxy) (chadkluck/serverless-remote-falcon-api-proxy)

### Create Repos that are *Ready-to-Deploy-and-Run*

All starters and **Ready-to-Deploy-and-Run** applications are configured to deploy and run immediately.

Application Starters are available directly from the `create_repo.py` script.

Creating and seeding a repository with code from another GitHub repository is easy:

```bash
./cli/create_repo.py my-new-repo --source https://github.com/63Klabs/serverless-cloudfront-cache-invalidation
```

**`create_repo.py` supports:**
- Creation of both CodeCommit and GitHub repositories
- Importing of Starter code, GitHub repositories, GitHub repository release, local or remote zip files

> **CAUTION:** Only install code from trusted sources!

After you have your repo, use `config.py` to create and deploy a pipeline off the `test` branch and you've got your first deployment! Add additional branches, pipelines, and resources as needed!

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

Principle of Least Privilege and Separation of Stacks by Concern

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

## Atlantis MCP Server

A publicly accessible [Atlantis MCP server](https://mcp.atlantis.63klabs.net) is available to assist in using the Atlantis Platform. Use it to discover documentation, starter code, and templates.
