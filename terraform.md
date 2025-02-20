# Terraform - IaC
## Overview
```
Terraform State 
                  --> AWS Provider/Cloudflare Provider --> AWS/Cloudflare
Terraform Config 
```
## Terraform Setup
1. Install Terraform: [https://developer.hashicorp.com/terraform/install](https://developer.hashicorp.com/terraform/install)
2. Authenticate to your cloud service provider:
- Create a user with the following policies:
  - RDS FullAccess
  - EC2 FullAccess
  - IAM FullAccess
  - Route53 FullAccess
  - DynamoDB FullAccess
  - S3 FullAccess

### !! NOTE !! - This is just an example.

3. Install the AWS CLI (or whatever CSP you're using)
4. ```aws configure```
- Paste in the access / secret keys
- Select a default region
- json is fine for the output format

5. ```~/.aws``` will contain the credentials to auth to AWS
6. Let's creat a simple Terraform file:
```
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "~> 3.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami = "ami-xyz"
  instance_type = "t2.micro"
}
```
Make sure to replace "ami-xyz" to your desired AMI.
7. Now, we can run ```terraform init``` inside of the folder you saved the .tf file in.
8. Next, run ```terraform plan```. This will generate an execution plan, used to show you what will actually change.
9. ```terraform apply``` does exactly what you think it does.
10. You can use ```terraform destroy``` to delete whatever you created earlier.

## Basic Usage
### State File
- Terraform's representation of the world
- JSON file w/ info about every resource and data object
- It has sensitive info! Make sure the file is encrypted w/ the correct permissions
- Can be stored locally or remotely
### Local Backend
- ✅ Easiest way to get started
- ❌ Sensitive values are in **plain text**
- ❌ Uncollaborative
- ❌ Manual
### Remote Backend
- Terraform has a managed offering (Terraform Cloud) which will store state files, etc
- Alternative: self-hosted remote backend (S3)
- ✅ Sensitive data encrypted
- ✅ Collaboration possible!
- ✅ Automation possible! (GitHub Actions, other automation pipelines)
- ❌ Increased complexity
### Plan
- Taking the Terraform config (desired state)
- Compares to Terraform state (actual state)
- ```terraform apply``` will change the state to match the config file
### Terraform Cloud
- Managed by HashiCorp
```
terraform {
  backend "remote {
    organization = "example-org"

    workspaces {
      name = "example-name"
    }
  }
}
```
### Self-Managed Backend
- AWS uses S3 and DynamoDB
- S3 = state file, DynamoDB = locking
- For example, you could put your DynamoDB and S3 buckets in a state file to ensure they're up
- 
