AWS CI/CD Pipeline for Static Website

Project Overview

This project demonstrates an end-to-end CI/CD pipeline for a static
website using GitHub, AWS CodePipeline, AWS CodeBuild, and Amazon S3.

Whenever a developer pushes code changes to the GitHub repository, AWS
CodePipeline automatically retrieves the latest source code, triggers
the build and test stages, and deploys the resulting website files to an
Amazon S3 bucket configured for static website hosting.

Architecture



High-level flow:

Developer
   |
   | git push
   v
GitHub
   |
   | Source
   v
AWS CodePipeline
   |
   +--> Build -----> AWS CodeBuild
   |
   +--> Test  -----> AWS CodeBuild
   |
   +--> Deploy ----> Amazon S3
                         |
                         v
                  Static Website
                         |
                         v
                        Users

Project Objectives

Build a practical AWS CI/CD project.

Automate static website deployments.

Integrate GitHub with AWS CodePipeline.

Use AWS CodeBuild for build and test execution.

Host the final website using Amazon S3 static website hosting.

Eliminate manual file uploads after code changes.

Demonstrate an end-to-end DevOps workflow suitable for real-world
projects.

AWS Services Used

Service                             Purpose

GitHub                          Stores and manages the website
source code.

AWS CodePipeline                Orchestrates the CI/CD workflow
from source to deployment.

AWS CodeBuild                   Builds and processes the source
code and runs configured build/test
commands.

Amazon S3                       Stores and hosts the static website
files.

CI/CD Workflow

1. Developer pushes code to GitHub

The developer makes a change to the website and pushes it to the
configured branch.

git add .
git commit -m "Updated website"
git push origin main

2. CodePipeline detects the change

The GitHub source integration provides the latest revision to AWS
CodePipeline.

The pipeline's Source stage retrieves the source artifact.

3. Build stage

AWS CodePipeline triggers the configured AWS CodeBuild project.

CodeBuild executes the project's configured build commands/build
specification and prepares the files that should be passed to the next
pipeline stage.

4. Test stage

The pipeline includes a test stage using AWS CodeBuild.

This stage can be used to run automated tests, validation commands,
linting, or other quality checks. A production implementation can expand
this stage with a dedicated automated test suite.

5. Deploy stage

After the required stages succeed, CodePipeline deploys the build
artifact to the configured Amazon S3 bucket.

The S3 deployment is configured to extract the artifact before
deployment so that the website files are placed into the bucket rather
than leaving the application as a single ZIP archive.

6. Website hosting

Amazon S3 is configured for static website hosting.

Users can access the website through the S3 website endpoint.

Pipeline Configuration

Pipeline

Pipeline name: S3-static-website

AWS Region: ap-south-1 (Asia Pacific - Mumbai)

Source

Provider: GitHub via GitHub App

Source: GitHub repository

Branch: main

Build

Build provider: AWS CodeBuild

CodeBuild project: StaticWebsiteBuild

Environment: Amazon Linux managed image

Build artifact: BuildArtifact

Test

Provider: AWS CodeBuild

Used for automated validation/testing as configured in the pipeline.

Deploy

Provider: Amazon S3

Bucket: revanth-aws-cicd-project-343779419117-ap-south-1-an

Deployment: Extract artifact before deployment

Hosting: S3 Static Website Hosting

Example Project Structure

A simple static website can be organized as follows:

aws-cicd-s3-project/
├── index.html
├── style.css
├── script.js
├── images/
│   └── ...
├── buildspec.yml
└── README.md

The exact files can vary depending on the website.

How to Deploy a Change

After the initial pipeline has been created:

Modify the website source code.

Commit the changes.

Push the changes to the configured GitHub branch.

CodePipeline detects the new revision.

The Source stage retrieves the new code.

CodeBuild runs the build stage.

The test stage runs the configured checks.

CodePipeline deploys the successful artifact to S3.

Refresh the S3-hosted website to verify the change.

Code Change
     |
     v
Git Push
     |
     v
GitHub
     |
     v
CodePipeline Trigger
     |
     v
Build
     |
     v
Test
     |
     v
S3 Deployment
     |
     v
Updated Website

Key DevOps Concepts Demonstrated

Continuous Integration

Developers continuously push code changes to a shared source repository.
The pipeline automatically processes the new revision and can run build
and validation steps.

Continuous Deployment

After the pipeline stages succeed, the website is automatically deployed
to Amazon S3 without manually uploading the files.

Infrastructure and Service Integration

The project demonstrates how multiple services can work together:

GitHub
  ↓
CodePipeline
  ↓
CodeBuild
  ↓
CodeBuild Test
  ↓
Amazon S3
  ↓
Static Website

Security Considerations

Use IAM roles instead of embedding AWS access keys in source code.

Follow the principle of least privilege for CodePipeline and
CodeBuild roles.

Keep the S3 bucket configuration restricted to the access model
required by the website.

Avoid storing secrets, credentials, or sensitive configuration files
in GitHub.

For a production deployment, consider using Amazon CloudFront in
front of S3 and HTTPS with AWS Certificate Manager.

Future Enhancements

This project can be extended into a more production-oriented
architecture by adding:

Amazon CloudFront for CDN and improved global performance.

AWS Certificate Manager (ACM) for HTTPS.

Amazon Route 53 for a custom domain.

Amazon SNS for pipeline success/failure notifications.

Manual approval before production deployment.

Amazon CloudWatch for monitoring and logs.

S3 Versioning for recovery and rollback.

Separate development, staging, and production environments.

Automated security and code-quality scanning.

Infrastructure as Code using Terraform.

Advantages

Fully automated deployment.

Repeatable and consistent release process.

Reduced manual errors.

Fast deployment of website changes.

Clear execution history through CodePipeline.

Serverless and cost-effective hosting for a static website.

Easy to extend into a more advanced DevOps architecture.

Interview Explanation

I built an end-to-end CI/CD pipeline for a static website using
GitHub, AWS CodePipeline, AWS CodeBuild, and Amazon S3. GitHub acts as
the source repository. When a developer pushes a change, CodePipeline
detects the new revision and retrieves the source code. It then
triggers CodeBuild to build and validate the application. After the
pipeline stages succeed, CodePipeline deploys the build artifact to an
S3 bucket configured for static website hosting. This automates the
deployment process and removes the need for manual S3 uploads.

Short Resume Description

AWS CI/CD Static Website Deployment | GitHub, CodePipeline,
CodeBuild, S3

Designed and implemented an automated CI/CD pipeline using GitHub,
AWS CodePipeline, and AWS CodeBuild.

Automated build, test, and deployment of a static website to Amazon
S3.

Configured S3 static website hosting and artifact-based deployment.

Implemented an event-driven deployment workflow where source-code
changes are automatically propagated to the hosted website.

Project Result

The completed pipeline successfully executes:

GitHub → CodePipeline → CodeBuild → Test → Amazon S3

The website is automatically updated after successful pipeline
execution.
