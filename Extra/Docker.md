- software development platform to deploy apps
- apps are packaged into containers which can be run on any OS
- Portable
- Predictable behavior for apps
- easily scale containers up and down

#### Where Docker images are stored?
- stored in Docker repositories
- Public: [Docker Hub](https://hub.docker.com) 
	- find base images for many technologies:
	- Ubuntu
	- MySQL
	- NodeJS, Java...
- Private: [[Compute Services#ECR|Amazon ECR]]

#### Docker versus Virtual Machines
- In docker, resources are shared with the host => many containers on one server.
![[Pasted image 20250217143628.png]] 
