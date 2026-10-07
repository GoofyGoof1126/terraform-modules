# VPC Basic — Terraform Module

## What this deploys

A minimal AWS network stack in `af-south-1` (Cape Town): one VPC, one public subnet, an internet gateway, a route table associating the two, and a security group restricting inbound access.

## Security group rules

| Rule | Rationale |
|---|---|
| Ingress TCP 22 from `<home IP>/32` | SSH access restricted to a single known management IP — no open `0.0.0.0/0` |
| Egress all traffic | Standard outbound for lab management tooling and OS updates |

## How to run
terraform init
terraform plan
terraform apply

Uses the `terraform-lab` named AWS CLI profile (least-privilege IAM user, not root/admin credentials). Credentials are never stored in this file.

## Lessons from building this

- The AWS tutorial's default `owners` filter for the Canonical Ubuntu AMI pointed at the wrong account ID; Canonical's actual AWS account ID is `099720109477`.
- `t2.micro` is not free-tier eligible in `af-south-1` — use `t3.micro` instead. Free-tier eligibility varies by region.
