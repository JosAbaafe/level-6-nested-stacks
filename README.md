# Level 6 – Building Reusable Infrastructure with Nested Stacks

## Overview

As CloudFormation templates grow larger, maintaining a single monolithic template becomes difficult. In this project, I learned how to split infrastructure into reusable building blocks using Nested Stacks.

The infrastructure was divided into three templates:

* Network Template
* Compute Template
* Root Template 

The root template orchestrates the deployment by creating the child stacks and passing outputs from the network stack as parameters to the compute stack.

---

## Objectives

* Build reusable CloudFormation templates.
* Deploy infrastructure using nested stacks.
* Pass outputs between child stacks.
* Store templates in Amazon S3.
* Create a complete environment from a single parent template.

---

## Technologies Used

* AWS CloudFormation
* Amazon S3
* Amazon EC2
* Amazon VPC
* Nested Stacks

---

## Architecture

```text
Root Stack
   │
   ├──────────────┐
   ▼              ▼
Network Stack   Compute Stack
      │               │
      ▼               ▼
VPC + Subnet      EC2 Instance
```

---

## What I Learned

Nested stacks allow infrastructure to be organized into reusable modules.

Instead of duplicating networking code in every template, the network resources are created once and reused by multiple applications.

The parent stack manages the deployment while child stacks focus on specific responsibilities.

---

## Screenshots

### 1. CloudFormation Parent Stack

The root stack orchestrates the deployment of the nested network and compute stacks.

![Parent Stack](screenshots/parent-stack.png)

---

### 2. Nested Stacks

CloudFormation automatically creates the child stacks after deploying the parent stack.

![Nested Stacks](screenshots/nested-stacks.png)

---

### 3. Amazon S3 Bucket

The child templates (`network.yaml` and `compute.yaml`) were uploaded to an S3 bucket before deploying the parent stack.

![S3 Bucket](screenshots/s3-templates.png)

---

### 4. Root Stack Outputs

The parent stack exposes the public IP address of the EC2 instance created by the compute stack.

![Root Stack Outputs](screenshots/root-stack-outputs.png)

---

### 5. EC2 Instance

The compute nested stack successfully launched the EC2 instance inside the VPC created by the network stack.

![EC2 Instance](screenshots/ec2-instance.png)

---


## Benefits of Nested Stacks

* Modular infrastructure
* Easier maintenance
* Reusable templates
* Simplified deployments
* Better collaboration between teams

---

## Challenge Completed

A future enhancement is to introduce a third nested stack dedicated to security resources.

The architecture becomes:

* Network Stack
* Security Stack
* Compute Stack

This mirrors how enterprise cloud teams separate responsibilities across networking, security, and application infrastructure.

---

## Key Takeaways

* Nested stacks improve template organization.
* Outputs from one stack become inputs to another.
* Child templates must be stored in Amazon S3.
* Parent templates coordinate the deployment of reusable infrastructure components.
