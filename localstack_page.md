## Project: Local Cloud Development with Localstack

**Project description:** With LocalStack, we can run our AWS applications or Lambdas entirely on our local machine without connecting to a remote cloud provider! Whether we are testing complex CDK applications or Terraform configurations, or just beginning to learn about AWS services, LocalStack helps speed up and simplify our testing and development workflow.

We will build a website using EC2 instances, Cognito, and DynamoDB, then use Gremlin to break the system. We’ll take down a single server, create network black holes, overload the CPU, and even simulate an AWS AZ or region failure, and observe the impacts. By triggering failures intentionally in a controlled way, we can be confident that our systems can deal with those failures before they occur (especially in the middle of the night, when we least expect it). Let’s unleash the gremlins and embrace the chaos!

### An example terraform provider configuration:

main.tf
```terraform
variable "ami" {
  default = "ami-06178cf087598769c"

}
variable "instance_type" {
  default = "t3.micro"

}
variable "region" {
  default = "eu-west-2"

}
resource "aws_instance" "test-servers" {
  ami           = var.ami
  instance_type = var.instance_type

}
```
provider.tf
```terraform
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "4.15.0"
    }
  }
}

provider "aws" {
  region                      = var.region
  skip_credentials_validation = true
  skip_requesting_account_id  = true

  endpoints {
    apigateway     = "http://aws:4566"
    cloudformation = "http://aws:4566"
    cloudwatch     = "http://aws:4566"
    dynamodb       = "http://aws:4566"
    es             = "http://aws:4566"
    firehose       = "http://aws:4566"
    iam            = "http://aws:4566"
    kinesis        = "http://aws:4566"
    lambda         = "http://aws:4566"
    route53        = "http://aws:4566"
    redshift       = "http://aws:4566"
    s3             = "http://aws:4566"
    secretsmanager = "http://aws:4566"
    ses            = "http://aws:4566"
    sns            = "http://aws:4566"
    sqs            = "http://aws:4566"
    ec2            = "http://aws:4566"
    ssm            = "http://aws:4566"
    stepfunctions  = "http://aws:4566"
    sts            = "http://aws:4566"
  }
}
```
