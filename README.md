# AWS Attribute-Based Access Control (ABAC) Tutorial

This project was created while following the AWS tutorial on Attribute-Based Access Control (ABAC): [AWS ABAC Tutorial](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_attribute-based-access-control.html#tutorial_abac_step6). The tutorial demonstrates how to use ABAC in AWS Identity and Access Management (IAM) to control permissions dynamically using user attributes.

## Overview
This repository walks through the step-by-step implementation of ABAC in AWS, covering user creation, policy definition, role assignments, and secret management in AWS Secrets Manager.

## Steps

### Step 1: Create Test Users
Create the following IAM users with specific tags:
- **access-Arnav-peg-eng**
  - `access-project = peg`
  - `access-team = eng`
  - `cost-center = 987654`
- **access-Mary-peg-qas**
  - `access-project = peg`
  - `access-team = qas`
  - `cost-center = 987654`
- **access-Saanvi-uni-eng**
  - `access-project = uni`
  - `access-team = eng`
  - `cost-center = 123456`
- **access-Carlos-uni-qas**
  - `access-project = uni`
  - `access-team = qas`
  - `cost-center = 123456`
 
  ![four users created](https://github.com/user-attachments/assets/d51edeee-617f-4061-9753-b3a082834108)


### Step 2: Create the ABAC Policy
Create an IAM permissions policy named **access-same-project-team** that allows actions based on tag conditions.

### Step 3: Create Roles
- Define IAM roles with tags that match the user attributes.
- Attach the **access-same-project-team** policy to each role.
- Example roles:
  - `access-peg-engineering`
  - `access-peg-quality-assurance`
  - `access-uni-engineering`
  - `access-uni-quality-assurance`

![roles](https://github.com/user-attachments/assets/052ce0e4-52d6-444e-a4ee-03ae2a2b5444)

### Step 4: Test Creating Secrets
- Sign in as an IAM user.
- Attempt to create secrets with various tag combinations.
- Validate that secrets can only be created if tags match the assigned role’s conditions.

### Step 5: Test Viewing Secrets
- Sign in with IAM users.
- Verify that users can only view secrets associated with their team and project.

### Step 6: Test Scalability
- Add a new project **Centaur**.
- Create a new IAM role **access-cen-engineering**.
- Create a new user **access-Nikhil-cen-eng** with the following tags:
  - `access-project = cen`
  - `access-team = eng`
  - `cost-center = 101010`
- Validate secret creation and viewing for Nikhil.
- Modify **access-Saanvi-uni-eng** user permissions to allow assuming multiple roles (Pegasus and Centaur projects).

## Conclusion
This tutorial demonstrates how ABAC simplifies permission management in AWS by dynamically enforcing access controls based on user attributes. It enables seamless scalability as new users, projects, and teams are added.

## References
- [AWS ABAC Tutorial](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_attribute-based-access-control.html#tutorial_abac_step6)

