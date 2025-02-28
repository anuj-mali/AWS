#iam #best-practices #guidelines
- do not use root account except for AWS account setup
- One physical user = one AWS user
- assign user to groups and assign permission to groups
- create strong password policy
- use and enforce MFA
- create and use Roles for providing permission to AWS Services
- use access keys for programmatic access (CLI/SDK)
- audit permissions of account using IAM Credentials Report & IAM Access Advisor
- Never share IAM users & Access keys