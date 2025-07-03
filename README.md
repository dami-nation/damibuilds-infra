# damibuilds-infra

This repository contains the Terraform code for deploying and managing the infrastructure behind [damibuilds.com](https://damibuilds.com), a static website hosted on AWS.

## Infrastructure Overview

The site is hosted using the following AWS services:

- **S3** — Static website file storage
- **CloudFront** — Global CDN with HTTPS and domain aliasing
- **ACM** — TLS certificate for HTTPS
- **Route 53** — DNS routing for domain and subdomain


This repository contains
- main.tf # Main Terraform configuration
- outputs.tf # Output variables
- bucket-policy.json # S3 bucket to allow CloudFront access
-.gitignore # Ignore local artifacts and and state files
- README.md # This file


##  Features

- Automatic TLS via ACM and CloudFront
- Secure access: S3 bucket is private, CloudFront OAC is used
- HTTPS redirect for `www.damibuilds.com` and root domain
- Fully managed via Infrastructure as Code (IaC)

##  Deployment Steps

To deploy or update the infrastructure:

```bash
terraform init
terraform plan
terraform apply
```

Ensure your AWS credentials are configured locally (~/.aws/credentials or via environment variables).

### Sensitive Info
This repo excludes sensitive values. Make sure to:

Replace ACCOUNT-ID, CERTIFICATE-ID, and DISTRIBUTION-ID placeholders in main.tf and bucket-policy.json.

Never commit .terraform/ or .tfstate to GitHub.


### Lessons Learned
CloudFront and ACM certificates must be in us-east-1.

You must manually validate domain ownership when using ACM for custom domains.

CloudFront distribution changes take time (~5–10 mins).

Be careful committing .terraform/ — it bloats the repo and breaks GitHub pushes.

### Cleanup
To destroy the infrastructure:


`terraform destroy`
 
