# Multi-cloud

## Overview

Multi-cloud refers to the use of multiple cloud computing and storage services in a single heterogeneous architecture. This approach allows organizations to leverage the strengths of different cloud providers, avoid vendor lock-in, and optimize their cloud strategy for performance, cost, and compliance.

## Multi-cloud Computing

Multi-cloud computing involves deploying applications and services across multiple cloud environments. This can include a mix of public clouds (such as AWS, Azure, and Google Cloud), private clouds, and on-premises infrastructure.

### IaC (Infrastructure as Code)

IaC provides a consistent way to manage and provision infrastructure across multiple cloud providers. By defining infrastructure in code, you can automate deployments, ensure consistency, and reduce errors.

Several tools support IaC for multi-cloud environments:

- **AWS CloudFormation:** Automates the setup and deployment of AWS resources using templates. It allows you to describe your infrastructure as code and manage it through AWS Management Console or APIs.

- **Azure Resource Manager (ARM):** Provides a unified management layer for Azure resources, allowing you to deploy, manage, and monitor resources using declarative templates.

- **Google Cloud Deployment Manager:** Enables you to create and manage Google Cloud resources using configuration files written in YAML or Python.

## Terraform

Terraform is an open-source infrastructure as code software tool that provides a consistent CLI workflow to manage hundreds of cloud services. It codifies cloud APIs into declarative configuration files.

### Terraform CLI

The Terraform CLI is the primary tool for interacting with Terraform. It provides commands for managing your infrastructure, from initializing configurations to applying changes.

- **Commands:** [developer.hashicorp.com/terraform/cli](https://developer.hashicorp.com/terraform/cli)

## Exercises

1. Write a Terraform configuration to deploy an AWS EC2 instance:

```tf
provider "aws" {
    region = "us-west-2"
}

resource "aws_instance" "example" {
    ami           = "ami-0c55b159cbfafe1f0"
    instance_type = "t2.micro"

    tags = {
        Name = "ExampleInstance"
    }
}
```

2. Initialize Terraform and apply the configuration:

```sh
# Initialize Terraform
terraform init

# Apply the configuration
terraform apply
```
