# 🌐 Hosting a Static Website on AWS S3 Using Terraform

A beginner-friendly Infrastructure as Code project that provisions an
Amazon S3 bucket with Terraform and uses it to host a simple static
website.

The project demonstrates how Terraform can be used to create and
configure AWS infrastructure instead of setting up the resources
manually through the AWS Management Console.

## 🏗️ Architecture
![Image Alt](image_url)



## 🏗️ Architecture Overview
 
``` text
                    ┌─────────────────────┐
                    │     Web Browser     │
                    └──────────┬──────────┘
                               │
                               │ HTTP
                               ▼
                 ┌──────────────────────────┐
                 │       Amazon S3           │
                 │                          │
                 │   Static Website Hosting │
                 │                          │
                 │  ┌────────────────────┐  │
                 │  │    index.html     │  │
                 │  │    error.html     │  │
                 │  └────────────────────┘  │
                 └────────────▲─────────────┘
                              │
                              │ Terraform
                              │
                 ┌────────────┴─────────────┐
                 │        Terraform         │
                 │                          │
                 │  • S3 Bucket              │
                 │  • Ownership Controls     │
                 │  • Public Access Settings │
                 │  • Bucket ACL             │
                 │  • S3 Objects             │
                 │  • Website Configuration  │
                 └──────────────────────────┘
```

## 🧰 Technologies Used

-   **Amazon S3** --- Static website hosting and object storage
-   **Terraform** --- Infrastructure as Code
-   **AWS Provider for Terraform** --- Creates and manages AWS resources
-   **HTML5** --- Static website content
-   **VS Code** --- Development environment

## ☁️ AWS Resources

The Terraform configuration creates and manages:

  ---------------------------------------------------------------------------
  Resource                                Purpose
  --------------------------------------- -----------------------------------
  `aws_s3_bucket`                         Creates the S3 bucket

  `aws_s3_bucket_ownership_controls`      Defines object ownership

  `aws_s3_bucket_public_access_block`     Configures public access settings

  `aws_s3_bucket_acl`                     Applies the public-read ACL

  `aws_s3_object`                         Uploads `index.html` and
                                          `error.html`

  `aws_s3_bucket_website_configuration`   Enables S3 static website hosting
  ---------------------------------------------------------------------------

## 📁 Project Structure

``` text
s3-terraform-website/
│
├── provider.tf
├── main.tf
├── variables.tf
├── index.html
└── error.html
```

### `provider.tf`

Defines the Terraform AWS provider and configures the AWS region.

The project uses:

``` hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}
```

### `variables.tf`

Defines the S3 bucket name:

``` hcl
variable "bucket_name" {
  default = "Unique name for the S3 bucket"
}
```

S3 bucket names must be globally unique.

### `main.tf`

Contains the AWS infrastructure configuration, including:

-   S3 bucket
-   Ownership controls
-   Public access configuration
-   Public-read ACL
-   Website files
-   Static website hosting configuration

### `index.html`

The main page of the static website.

### `error.html`

The error page displayed by the S3 website configuration.

## 🚀 Getting Started

### Prerequisites

Install and configure:

-   An AWS account
-   Terraform
-   AWS CLI
-   VS Code or another code editor
-   AWS credentials with permissions to create the required S3 resources

Verify Terraform:

``` bash
terraform version
```

Verify AWS CLI:

``` bash
aws --version
```

Verify your AWS identity:

``` bash
aws sts get-caller-identity
```

## 1. Clone the Repository

``` bash
git clone <your-repository-url>
cd s3-terraform-website
```

## 2. Configure the Bucket Name

Open `variables.tf` and replace the default value with a globally unique
S3 bucket name.

Example:

``` hcl
variable "bucket_name" {
  default = "my-unique-terraform-static-website"
}
```

## 3. Initialize Terraform

Run:

``` bash
terraform init
```

This initializes the Terraform project and downloads the required AWS
provider.

## 4. Review the Infrastructure

Run:

``` bash
terraform plan
```

This shows the resources Terraform intends to create before making
changes.

## 5. Deploy the Infrastructure

Run:

``` bash
terraform apply -auto-approve
```

Terraform will create the S3 bucket and configure the required
resources.

## 6. Access the Website

After the website configuration has been created:

1.  Open the AWS Management Console.
2.  Go to **Amazon S3**.
3.  Open your bucket.
4.  Go to **Properties**.
5.  Find **Static website hosting**.
6.  Open the displayed website endpoint.

The `index.html` page should load in your browser.

## 🔄 Updating the Website

Modify `index.html` or `error.html`, then run:

``` bash
terraform apply -auto-approve
```

Terraform compares the current configuration with the deployed
infrastructure and updates the S3 objects when changes are detected.

## 🧹 Destroy the Infrastructure

To remove the resources managed by Terraform:

``` bash
terraform destroy -auto-approve
```

⚠️ **Warning:** `terraform destroy` deletes resources created by
Terraform. Use it carefully.

## 🔐 Important Security Note

This project intentionally configures the S3 bucket for public access
because the goal is to demonstrate basic S3 static website hosting.

The configuration includes:

``` hcl
acl = "public-read"
```

and disables the relevant public-access blocking settings.

This approach is suitable for this learning project, but public S3
access should be considered carefully for production workloads. A
production architecture may use additional security and delivery
services rather than exposing an S3 bucket directly.

## 🧠 What I Learned

This project demonstrates practical concepts including:

-   Infrastructure as Code (IaC)
-   Terraform project initialization
-   Terraform AWS provider configuration
-   Creating AWS resources with Terraform
-   S3 static website hosting
-   S3 bucket ownership controls
-   S3 public-access configuration
-   S3 object management through Terraform
-   Terraform dependencies with `depends_on`
-   `terraform plan`
-   `terraform apply`
-   `terraform destroy`

## 🔄 Infrastructure as Code Workflow

The basic workflow used in this project is:

``` text
Write Terraform Configuration
            ↓
      terraform init
            ↓
      terraform plan
            ↓
      terraform apply
            ↓
       AWS Resources
            ↓
      Hosted Website
```

This demonstrates the core idea of Infrastructure as Code: defining
cloud infrastructure in configuration files and managing it through
repeatable commands.

## 📚 Medium Article

I documented the complete build process in a Medium article:

**Hosting a Static Website on AWS S3 Using Terraform**

https://medium.com/@luthirapeiris1/hosting-a-static-website-on-aws-s3-using-terraform-b328f4fcc378

The article covers the project step by step, including:

-   Creating the project
-   Configuring the AWS provider
-   Initializing Terraform
-   Creating the S3 bucket
-   Configuring ownership
-   Configuring public access
-   Adding the public-read ACL
-   Creating HTML files
-   Uploading objects to S3
-   Enabling static website hosting
-   Accessing the website
-   Updating and destroying the infrastructure

## 🎯 Project Goal

The main goal of this project was to gain practical experience with
**AWS, Terraform, and Infrastructure as Code** by deploying a simple
static website without manually creating the infrastructure through the
AWS Console.

## 👨‍💻 Author

**Luthira Peiris**

-   GitHub: https://github.com/LuthiraPeiris
-   Medium: https://medium.com/@luthirapeiris1
-   LinkedIn: https://www.linkedin.com/in/luthirapeiris/

------------------------------------------------------------------------

⭐ If you found this project useful, consider giving the repository a
star.

**AWS • Terraform • Infrastructure as Code**
