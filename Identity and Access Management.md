- global service
# Users & Groups
- users are people in the organization and can be grouped
- groups can only contain users and not other groups
- users do not need to be a part of a group
- users can belong to multiple groups
![[Pasted image 20250224111540.png]]
# Permissions
- Users or Groups can be assigned JSON documents called policies
- describes that a user or group is allowed to do
- policies define the permission of users
- **apply the least privilege principle**
![[Pasted image 20250224111951.png]]
# IAM Policies Inheritance
![[Pasted image 20250224132325.png]]
## Policies Structure
- consists of
	- Version: policy language version
	- Id: identifier for policy (optional)
	- Statement: one or more individual statements (required)
- Statement consists of
	- Sid: an identifier for the statement (optional)
	- Effect: whether the statement allows or denies access (Allow, Deny)
	- Principal: account/user/role to which this policy applies to
	- Action: list of actions the policy allows or denies
	- Resource: list of resources to which the actions applied to
	- Condition: conditions for when this policy is in effect (optional)
	![[Pasted image 20250224141354.png]]
# Password Policy
- can setup password policy with different options:
	- Set a minimum password length
	- require specific character types:
		- uppercase letters
		- lowercase letters
		- numbers
		- non-alphanumeric characters
	- Allow all IAM users to change their own passwords
	- Require users to change their password after some time (password expiration)
	- prevent password re-use
# Multi Factor Authentication - MFA
- MFA = password *you know* + security device *you own*
- **if a password is stolen or hacked, the account is not compromised**
![[Pasted image 20250224142530.png]]
## MFA Device options
- Virtual MFA Device
	- Support for multiple tokens on a single device
	- *Example*: Google Authenticator, Authy, ...
- Universal 2nd Factor (U2F) Security Key
	- Physical device
	- support for multiple root and IAM users using a single security key
	- *Example*: YubiKey
- Hardware Key Fob MFA Device
- Hardware Key Fob MFA Device for AWS GovCloud (US)
# Accessing AWS
- AWS Management Console
	- protected by password + MFA
- AWS Command Line Interface (CLI)
	- protected by access keys
	- tool that enables users to interact with AWS Services using commands through terminal
	- direct access to the public APIs of AWS services
	- can develop scripts to manage resources
- AWS Software Developer Kit (SDK)
	- for code: protected by access keys
	- Language specific APIs
	- access and manage AWS services programmatically
	- embedded within application
	- Supports
		- SDKs (JavaScript, Python, PHP, .NET, Ruby, Java, Go, Node.js, C++)
		- Mobile SDKs (Android, iOS, ...)
		- IoT Device SDKs (Embedded C, Arduino, ...)
- Access keys are generated through the AWS Console
- Users manage their own access keys
- *Access keys ~= username*
- *Secret keys ~= password*
# IAM Roles
- some AWS services will need to perform actions on our behalf
- to do so, we will need to assign permissions to AWS services using IAM Roles
- Common roles:
	- EC2 Instance Roles
	- Lambda Function Roles
	- Roles for CloudFormation
![[Pasted image 20250224144655.png]]
# IAM Security Tools
- IAM Credentials Report (account-level)
	- report that lists all our account's users and the status of their various credentials
- IAM Access Advisor (user-level)
	- shows the service permissions granted to a user and when those services were last accessed
	- can use this info to revise policies
# IAM Guidelines & Best Practices
- do not use root account except for AWS account setup
- One physical user = one AWS user
- assign user to groups and assign permission to groups
- create strong password policy
- use and enforce MFA
- create and use Roles for providing permission to AWS Services
- use access keys for programmatic access (CLI/SDK)
- audit permissions of account using IAM Credentials Report & IAM Access Advisor
- Never share IAM users & Access keys
# Shared Responsibility Model
![[Pasted image 20250224145318.png]]
# Summary
![[Pasted image 20250224145332.png]]
