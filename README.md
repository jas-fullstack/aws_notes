# Chapter 1: Identity and Access Management (IAM)

### Overview
IAM is a **global service** used to manage secure access to AWS resources.
- **Root Account**: Unlimited access to all resources. Enable **MFA** and avoid sharing credentials.
- **Best Practice**: Use IAM users with the least privilege principle; do not share the root account.

---

### Key Components

#### Users
- Represents a person or application.
- Can have programmatic access (via access keys) and/or management console access.

#### Groups
- Collections of users sharing common permissions.
  - A group can only contain users, not other groups.
  - A user can belong to multiple groups.

#### Roles
- Delegates permissions to entities (users, applications, services).
- No long-term credentials; roles can be assumed by trusted entities.
  - Example: Grant an EC2 instance access to S3 using a role.

#### Policies
- JSON documents defining permissions. Types:
  - **AWS Managed**: Predefined by AWS.
  - **Customer Managed**: Created by you.
  - **Inline**: Directly attached to users, groups, or roles.
- Example Policy:
  ```json
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Action": "s3:ListBucket",
        "Resource": "arn:aws:s3:::example_bucket"
      }
    ]
  }
  ```
- **Evaluation Logic**: Explicit Deny > Explicit Allow > Implicit Deny.

#### Access Keys
- For programmatic access (CLI, SDKs).
- Rotate keys regularly, disable unused keys, and avoid hardcoding them.

#### IAM Credential Report
- Summary of all IAM users and their credentials (passwords, access keys).

---

### Security Best Practices
- Enable **MFA** for all users.
- Grant the least privilege required.
- Regularly review **IAM Credential Reports**.
- Use **service control policies (SCPs)** to manage permissions across accounts.
- Enforce strong passwords and regular rotation.
- Avoid root account credentials except for initial setup.

---

### Common Scenarios & Exam Questions

#### **Scenario 1**: EC2 Access to S3
Q: How do you securely allow an EC2 instance to access an S3 bucket?
- **Answer**: Create a role with S3 permissions and attach it to the EC2 instance.

#### **Scenario 2**: Recover Deleted IAM User
Q: A developer accidentally deleted an IAM user. How can you recover it?
- **Answer**: Deleted IAM users cannot be recovered. Recreate the user and reassign permissions.

#### **Scenario 3**: Third-Party Application Access
Q: How do you allow a third-party app to access an S3 bucket securely?
- **Answer**: Create a role and allow the app to assume it using AWS Security Token Service (STS). Add a resource-based policy to the S3 bucket.

#### **Scenario 4**: Compromised Access Key
Q: An IAM access key has been compromised. What do you do?
- **Answer**: Disable the compromised key, create a new one, update the application, and delete the old key.

#### **Scenario 5**: Enforce MFA
Q: How do you enforce MFA for all IAM users?
- **Answer**: Create a policy that explicitly requires MFA and attach it to all users/groups.

#### **Scenario 6**: Restrict Access by IP
Q: How can you restrict an IAM user to access S3 only from a specific IP address?
- **Answer**: Use the "aws:SourceIp" condition key in the policy.

#### **Scenario 7**: Monitor Unauthorized Access
Q: How do you monitor unauthorized access attempts?
- **Answer**: Use AWS CloudTrail and set up CloudWatch Alarms.

#### **Scenario 8**: Cross-Account Access
Q: A user needs access to resources in multiple accounts. How do you configure this?
- **Answer**: Set up roles in each account and allow the user to assume them.

#### **Scenario 9**: Use Case for Service Control Policies
Q: What is the purpose of Service Control Policies (SCPs) in AWS Organizations?
- **Answer**: SCPs define the maximum permissions for accounts in an organization, ensuring that no user or role exceeds those permissions.

---

### Sample Interactive Questions

#### **Question 1**: What is the best practice for granting an application access to S3 from an EC2 instance?
- A) Attach an access key to the instance.
- B) Create a role and attach it to the instance.
- C) Share the root account credentials.
- D) Use AWS Managed Policies.

**Answer**: B) Create a role and attach it to the instance.

#### **Question 2**: How can you enforce all IAM users to use MFA?
- A) Enable MFA for the root account only.
- B) Use SCPs to enforce MFA.
- C) Create an IAM policy that requires MFA and attach it to all users.
- D) Rotate all access keys.

**Answer**: C) Create an IAM policy that requires MFA and attach it to all users.

---

### Useful Links
- [IAM Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)
- [IAM Best Practices](https://aws.amazon.com/iam/resources/best-practices/)
- [IAM Policy Generator](https://awspolicygen.s3.amazonaws.com/policygen.html)
