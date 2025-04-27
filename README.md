## AWS CloudFormation CI/CD Pipeline for Java Hello World App

This project demonstrates how to deploy a simple Java Hello World application using AWS services (CodeCommit, CodeBuild, CodeDeploy, CodePipeline) fully provisioned via CloudFormation.

### Project Overview

This project demonstrates a full CI/CD pipeline built using AWS services:
- **AWS CodeCommit** — Source repository
- **AWS CodeBuild** — Build automation
- **AWS CodeDeploy** — Deployment automation
- **AWS CodePipeline** — Orchestration
- **AWS CloudFormation** — Infrastructure as Code (IaC)

### Project Structure

| Folder/File         | Purpose                                    |
|:---------------------|:-------------------------------------------|
| `cloudformation/`    | CloudFormation templates for infrastructure |
| `src/`               | Java Hello World Application Source Code  |
| `scripts/`           | EC2 startup scripts for CodeDeploy         |
| `buildspec.yml`      | CodeBuild build instructions               |
| `appspec.yml`        | CodeDeploy deployment instructions         |
| `README.md`          | Project documentation                     |

### Prerequisites

- AWS CLI installed and configured
- Existing EC2 Key Pair (for SSH access)
- Basic AWS IAM permissions for CloudFormation, EC2, CodeDeploy, CodePipeline, CodeBuild, and CodeCommit

### Steps to Deploy

1. Deploy EC2 instace stack using AWS CloudFormation
   ```
   aws cloudformation deploy --template-file cloudformation/ec2-stack.yml --stack-name ec2-stack --parameter-overrides KeyName=your-key-name
   ```

2. Deploy CI/CD Pipeline stack using AWS CloudFormation
   ```
   aws cloudformation deploy --template-file cloudformation/cicd-stack.yml --stack-name cicd-stack
   ```

3. Code Commit and Push
   - Clone the CodeCommit repository after deployment:
    ```
    git clone https://git-codecommit.<region>.amazonaws.com/v1/repos/HelloWorldAppRepo
    cd HelloWorldAppRepo
    ```
   - Add the provided Java app (src/HelloWorldApp), buildspec.yml, appspec.yml, and scripts/. Then commit and push:
     ```
	 git add .
     git commit -m "Initial commit"
     git push origin main
     ```
	 
4. How it works
   - Pushing code triggers CodePipeline.
   - CodeBuild compiles the Java app.
   - CodeDeploy deploys the artifact to the EC2 instance automatically.

### Cleaning Up

To delete the resources:

```
aws cloudformation delete-stack --stack-name cicd-stack
aws cloudformation delete-stack --stack-name ec2-stack
```

---

