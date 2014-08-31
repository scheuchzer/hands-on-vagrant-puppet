## Infrastructure as Code
### Vagrant and Puppet
in software development



https://github.com/scheuchzer/hands-on-vagrant-puppet



## Setup

- 	Install Java
	
	http://www.oracle.com/technetwork/java/javase/downloads/index.html
	
- 	Install Maven
	
	http://maven.apache.org/download.cgi


- Install Virtualbox
	
	https://www.virtualbox.org/wiki/Downloads

- 	Install Vagrant
	
	http://www.vagrantup.com/downloads.html


-	Download a VM to speed up the examples later on.
	
	Execute the commands:
	```bash
	# This is a bug in Vagrant for Windows. Add an additional PATH 
	# directory. Not needen on Linux.
	$ set PATH=c:\HashiCorp\Vagrant\embedded\mingw\bin;%PATH%
	```
	```
	# Install a basic vm
	$ vagrant box add hashicorp/precise32
	```
