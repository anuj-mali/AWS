#iam #policies
- Users or Groups can be assigned JSON documents called policies
- describes that a user or group is allowed to do
- policies define the permission of users
- **apply the least privilege principle**
![[Pasted image 20250224111951.png]]
## IAM Policies Inheritance
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
## Password Policy
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