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

### Variable
- Input variables:
  - ```var.<name>```
- Local Variables
  - ```local.<name>```
- Output variables
  - For example, getting a public IP from ```terraform apply``` and using it later in the config
- Setting input variables:
  - Manual entry during plan/apply
  - Default value in declaration block
  - TF_VAR_<name> environment variables
  - ```terraform.tfvars``` file
  - ```*.auto.tfvars``` file
  - Command line ```-var``` or ```-var-file```
- Primitave Types:
  - string
  - number
  - bool
- Complex types:
  - list(<type>)
  - set(<type>)
  - map(<type>)
  - object
  - tuple
- Sensitive Data:
  - To mark a variable as sensitive, use ```sensitive = true```
  - Pass to terraform apply with:
    - ```TV_VAR_variable```
    - ```-var``` (retrieved from secret manager at runtime)
  - External secret stores (AWS Secrets Manager, for example)
## Advanced Features
- Template strings
- Operators
- Conditionals (cond ? true : false)
- For
- Splat
- Dynamic blocks
- Constraints (type & version)
- Functions:
  - Numeric
  - String
  - Collection
  - Encoding
  - Filesystem
  - Date / time
  - Hash / crypto
  - IP Network
  - Type conversion
### Meta Arguments
- ```depends_on```
  - If two resources depend on each other, this specifices the dependency to enforce ordering
- ```count```
  - Allows for creation of multiple resources/modules from a single block
  - When multiple necessary resources are nearly identical
- ```for_each```
  - Same as count, but allows for more control to customize each resource
- ```lifecycle```
  - Set of meta args to control terraform behavior for specific resources
    - ```create_before_destroy``` helps with zero downtime deployments
    - ```ignore_changes``` stops Terraform from trying to revert metadata from being set elsewhere
    - ```prevent_destroy``` causes Terraform to _reject_ any plan which would destroy this resource
### Provisioners
- Perform action on local or remote machine

## Project Organization and Modules
### Modules
- Modules are containers for multiple resources that are used together.
- Collection of ```.tf``` + ```.tf.json``` in a single directory
- The main way to take Terraform config and reuse / share them
- Types:
  - Root: default module w/ all .tf files in main working directory
  - Child: separate, external module referred to from .tf file
- Sources:
  - Local paths
  - Terraform registry - specify source and version
  - GitHub - HTTPS or SSH
  - BitBucket - 
  - Generic Git, Mercurial repos
  - HTTP URLs
  - S3 buckets
  - GCS buckets
  - etc...
- What makes a good module?
  - Group resources into a logical fashion
  - Useful defaults
### Multiple Environments
- We want both a staging and prod environment
- Maybe even a dev environment?
- But we don't want to rewrite our config file...
- Workspaces: multiple named sections within a single backend
- File structure: directory layout provides separation, modules provide reuse
### Terragrunt
- Tool that provides utilities to make Terraform use cases easier
- [https://terragrunt.gruntwork.io/](https://terragrunt.gruntwork.io/)
### Testing Terraform Code?
Built in features:
- terraform fmt
- terraform validate
- terraform plan
- custom validation rules
External features:
- tflint 
- checkov, tfsec, terrascan, terraform-compliance, snyk
- Terraform Sentinal (enterprise only)
