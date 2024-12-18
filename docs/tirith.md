# Tirith - StackGuardian Policy Engine

Tirith scans declarative Infrastructure as Code (IaC) configurations like Terraform against policies defined using JSON.

## Content

<!-- - [Feature Road-Map](#feature-road-map) -->
<!-- - [Local Development Environment](#local-development-environment) -->

- [Features](#features)
- [Usage](#usage)
- [Example Tirith policies](#example-tirith-policies)
- [Want to contribute?](#want-to-contribute)
  - [Getting an issue assigned](#getting-an-issue-assigned)
  - [A bug report](#a-bug-report)
  - [Opening a Pull Request and getting it merged](#opening-a-pull-request-and-getting-it-merged)
- [Submitting a feedback](#submitting-a-feedback)
- [Support](#support)
- [License](#license)

## Features

- An easy to read and simple way to define policy as code against structured formats.
- Use providers to define policies for terraform plan, infracost or any abstract JSON.
- Easily evaluate inputs against policy using pre-defined evaluators like ContainedIn, Equals, RegexMatch etc.
- Write your own provider (plugin) by leveraging a highly extensible and pluggable architecture to support any input formats.

<!-- ## Feature Road-map

This is only a list of approved features that will be included in Tirith over the next iterations.

- Extended support for Terraform Plan
- Support for Cloudformation and ARM
- Extended library of evaluator functions -->

## Usage

```
usage: tirith [-h] [-policy-path PATH] [-input-path SOURCE-TYPE] [--json] [--verbose] [--version]

Tirith (StackGuardian Policy Framework)

optional arguments:
  -h, --help               show this help message and exit
  -policy-path PATH        Path containing Tirith policy as code
  -input-path SOURCE-TYPE  Input file path
  --json                   Only print the result in JSON form (useful for passing output to other programs)
  --verbose                Show detailed logs of from the run
  --version                show program's version number and exit
```

## Example Tirith policies

[Examples using various providers](tests/providers)

1. VPC and EC2 instance policy (using Terraform plan provider)

- AWS VPC instance_tenancy is "default"
- EC2 instance cannot be destroyed

```json
{
  "meta": {
    "required_provider": "stackguardian/terraform_plan",
    "version": "v1"
  },
  "evaluators": [
    {
      "id": "check_ec2_tags_are_present",
      "provider_args": {
        "operation_type": "attribute",
        "terraform_resource_type": "aws_vpc",
        "terraform_resource_attribute": "instance_tenancy"
      },
      "condition": {
        "type": "Equals",
        "value": "default"
      }
    },
    {
      "provider_args": {
        "operation_type": "action",
        "terraform_resource_type": "aws_instance"
      },
      "condition": {
        "type": "ContainedIn",
        "value": ["destroy"]
      },
      "id": "destroy_ec2"
    }
  ],
  "eval_expression": "check_ec2_tags_are_present && !destroy_ec2"
}
```

2. Cost control policy (using Infracost provider)

- EC2 instance cost is lower than 100 USD per month

```json
{
  "meta": {
    "required_provider": "stackguardian/infracost",
    "version": "v1"
  },
  "evaluators": [
    {
      "provider_args": {
        "operation_type": "total_monthly_cost",
        "resource_type": ["aws_ec2"]
      },
      "condition": {
        "type": "LessThanEqualTo",
        "value": 100
      },
      "id": "ec2_cost_below_100_per_month"
    }
  ],
  "eval_expression": "ec2_cost_below_100_per_month"
}
```

3. StackGuardian Workflow Policy (using SG workflow provider)

- Terraform Workflow should require an approval to create or destroy resources

```json
{
  "meta": {
    "required_provider": "stackguardian/sg_workflow",
    "version": "v1"
  },
  "evaluators": [
    {
      "provider_args": {
        "operation_type": "attribute",
        "workflow_attribute": "approvalPreApply"
      },
      "condition": {
        "type": "Equals",
        "value": true
      },
      "id": "require_approval_before_creating_ec2"
    }
  ],
  "eval_expression": "require_approval_before_creating_ec2"
}
```

4. Make sure that AWS ELBs are attached to security group (using Terraform plan provider)

```json
{
  "meta": {
    "version": "v1",
    "required_provider": "stackguardian/terraform_plan"
  },
  "evaluators": [
    {
      "id": "aws_elbs_have_direct_references_to_security_group",
      "provider_args": {
        "operation_type": "direct_references",
        "terraform_resource_type": "aws_elb"
      },
      "condition": {
        "type": "Contains",
        "value": "aws_security_group",
        "error_tolerance": 2
      }
    }
  ],
  "eval_expression": "aws_elbs_have_direct_references_to_security_group"
}
```

5. Kubernetes (using Kubernetes provider)

- Make sure that all pods have a liveness probe defined

```json
{
  "meta": {
    "version": "v1",
    "required_provider": "stackguardian/kubernetes"
  },
  "evaluators": [
    {
      "id": "kinds_have_null_liveness_probe",
      "provider_args": {
        "operation_type": "attribute",
        "kubernetes_kind": "Pod",
        "attribute_path": "spec.containers.*.livenessProbe"
      },
      "condition": {
        "type": "Contains",
        "value": null,
        "error_tolerance": 2
      }
    }
  ],
  "eval_expression": "!kinds_have_null_liveness_probe"
}
```
