# AWS Identity and Access Management (IAM)


It is a web service that helps you securely control access to AWS resources. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.

If we breakdown the term Identity and Access Management,

**Identity** — stands for Authentication, and

**Access**  — stands for Authorization.

## Components of IAM
**Users —** Using IAM, we can create and manage AWS users and use permissions to allow and deny their access to AWS resources.

**Groups —**  The users created can also be divided into groups and then the rules and policies that apply on the group will also apply on the user level as well.

**Roles —**  An IAM role is an IAM entity that defines a set of permissions for making AWS service requests. Trusted entities such as IAM users, applications or AWS services like EC2, Lambda etc. assumes these roles to carry out the task on our behalf.

**Policies —**  We create policies to assign permission to a user, group, role or resource. It is a document that explicitly lists the permissions.

The policy would contain the following information:

1.  Who can access it
2.  What actions that user can take
3.  Which AWS resources that user can access
4.  When they can be accessed

IAM role has two main parts —  **Permission Policy**  and **Trust Policy**.These policies are  **JSON objects**. **Permission Policy**  describes the permission of the role and  **Trust Policy**  describes who can assume that role.

### Main policy types
#### **_Service control policies (SCPs)_**

These are a type of organization policy that we can use to manage permissions in our organization. SCPs offer central control over the maximum available permissions for all accounts in our organization. SCPs help us to ensure our accounts stay within our organization’s access control guidelines. An SCP defines a  **guardrail**, or sets limits, on the actions that the account’s administrator can delegate to the IAM users and roles in the targeted accounts.

#### **_Identity-based policies_**

These are attached to an IAM user, group, or role. These policies let us specify what that identity can do (its permissions). For example, we can attach the policy to the IAM user named Ram, stating that he is allowed to perform the Amazon DynamoDB  `getItem`  action.

#### **_Resource-based policies_**

With  resource-based policies, we can specify who has access to the resource and what actions they can perform on it. These policies are attached to a resource and not to the principal.


###  Concepts
**Principal**  is an identity in IAM. It is somebody who can make API calls to access AWS resources. It is the thing that we may not see very often because we mostly attach policies to principals (eg. IAM users or IAM roles). So, we don’t have to specify it.

**Action**  is the type of access that is allowed or denied.

**Resource**  is the Amazon resource on which specified Action will act.

**Condition**  defines the condition under the access defined is valid.

### Demo: Create an S3 Bucket Using the MFA Feature

**Problem statement:**  To create an S3 bucket for a company in which each user can read and write data with multifactor authentication.

**Task:**  To create policies and assign permissions for a user and a group.

-   Provide access (read and write) to the developer group.
-   Provide a policy in which a user is allowed to read or denied permission to write an object in an S3 bucket.

This is a very good use case if you have sensitive data in an S3 bucket and you want only privileged or MFA-authenticated users to make changes to those buckets. For those privileged users, you would enable multifactor authentication.
