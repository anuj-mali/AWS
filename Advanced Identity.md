# AWS STS (Security Token Service)
- allows to create temporary, limited-privileges credentials to access AWS resources
- short-term credentials: can configure expiration period
- provides access key, security access key and a session key which is limited in time
- use cases
	- **identity federation**
		- manage user identities in external system and provide them with STS tokens to access AWS resources
	- **IAM Roles for cross/same account access**
	- **IAM Roles for Amazon EC2**
		- provide temporary credentials for EC2 instances to access AWS resources
![[Pasted image 20250225155252.png]]
# Amazon Cognito (Simplified)
- provide identity for Web and Mobile applications users (potentially millions)
- Instead of creating them an IAM user, create a user in Cognito
	- IAM users are only for people in the company who need to user AWS directly
![[Pasted image 20250225160512.png]]
# Directory Services
## AWS Managed Microsoft AD
- Create own [[Microsoft Active Directory]] in AWS
- manage users locally
- supports MFA
- establish "trust" connections with on-premises [[Microsoft Active Directory]]
![[Pasted image 20250225161211.png]]
## AD Connector
- Directory Gateway (proxy) to redirect to on-premise [[Microsoft Active Directory|AD]]
- supports MFA
- Users are managed on the on-premise [[Microsoft Active Directory|AD]]
![[Pasted image 20250225161318.png]]
## Simple AD
- AD-compatible managed directory on AWS
- cannot be joined with on-premise AD
![[Pasted image 20250225161403.png]]
# AWS IAM Identity Center
- successor to AWS Single Sign-On (SSO)
- One login for all
	- AWS accounts in AWS Organizations
	- Business cloud applications
	- SAML2.0-enabled applications
	- EC2 Windows Instances
- Identity providers
	- built-in identity store on IAM Identity Center
	- 3$^{rd}$ party: [[Microsoft Active Directory]], OneLogin, Okta... 
## Login Flow
![[Pasted image 20250225162548.png]]
# Summary
![[Pasted image 20250225162619.png]]