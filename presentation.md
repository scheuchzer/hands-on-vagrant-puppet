## Infrastructure as Code
### Vagrant and Puppet
in software development



https://github.com/scheuchzer/hands-on-vagrant-puppet



## Vagrant

```bash
$ vagrant up
```


## Thank you!



## Agenda
- Infrastructure as code
- Vagrant
- Puppet



## Infrastructure as code


### some buzz words

- Infrastructure as code
- Disposable environments
- Reproducible environments
- Virtualization
- Cloud
- Continous delivery
- DevOps


### some players

![vm-tools](vm-tools.png)
![ifrastructure-as-code-tools](infrastructure-tools.png)


### some players 

![vagrant](vagrant.png)

![docker](docker.jpeg)



## Vagrant
> Create and configure lightweight, reproducible, and portable development environments.

http://www.vagrantup.com/


### Vagrant 

- for reproducable virtual machines
- infrastructure code in plain text and versioned
- production like development environment
- simple dev setup
- enables automated builds of VMs


### What it does

- clone a VM (box)
- start/stop/delete VM
- calls provisioning tools
- export new VM 



## Vagrant
### basics


### Config

one single config file
```bash
Vagrantfile
```


### Commands for developers

```bash
vagrant up        # start vm(s)

vagrant ssh       # login 

vagrant halt      # stop vm(s)

vagrant destroy   # delete vm(s)
```


### Commands for system engineers

```bash
vagrant init

vagrant package   # create new box from current vm state 
```


### Exercise
#### Setup a VM
1. initialize new vagrant project
  - use the box ***hashicorp/precise32***
-  start the virtual machine
-  log into the virtual machine

#### need help?

- http://docs.vagrantup.com/v2/
- ```bash
vagrant
#or
vagrant help {command}
```


### Solution

```bash
mkdir vagrant-tutorial
cd vagrant-tutorial
vagrant init hashicorp/precise32
vagrant up 
vagrant ssh
```

Note:
- pwd
- top
- ls /vagrant
- exit
- vagrant halt



## Vagrant
### Configuration


### The Vagrantfile

```bash
Vagrantfile
```
- One single config file
- Configuration is written in Ruby 
- but you don't need any Ruby knowledge!


### The minimal config file
```ruby
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	config.vm.box = "hashicorp/precise32"
end
```


### Well documented config file

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "precise32"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  # config.vm.box_url = "http://domain.com/path/to/above.box"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network :forwarded_port, guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network :private_network, ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network :public_network

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  # config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider :virtualbox do |vb|
  #   # Don't boot with headless mode
  #   vb.gui = true
  #
  #   # Use VBoxManage to customize the VM. For example to change memory:
  #   vb.customize ["modifyvm", :id, "--memory", "1024"]
  # end
  #
  # View the documentation for the provider you're using for more
  # information on available options.

  # Enable provisioning with Puppet stand alone.  Puppet manifests
  # are contained in a directory path relative to this Vagrantfile.
  # You will need to create the manifests directory and a manifest in
  # the file precise32.pp in the manifests_path directory.
  #
  # An example Puppet manifest to provision the message of the day:
  #
  # # group { "puppet":
  # #   ensure => "present",
  # # }
  # #
  # # File { owner => 0, group => 0, mode => 0644 }
  # #
  # # file { '/etc/motd':
  # #   content => "Welcome to your Vagrant-built virtual machine!
  # #               Managed by Puppet.\n"
  # # }
  #
  # config.vm.provision :puppet do |puppet|
  #   puppet.manifests_path = "manifests"
  #   puppet.manifest_file  = "site.pp"
  # end

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  # config.vm.provision :chef_solo do |chef|
  #   chef.cookbooks_path = "../my-recipes/cookbooks"
  #   chef.roles_path = "../my-recipes/roles"
  #   chef.data_bags_path = "../my-recipes/data_bags"
  #   chef.add_recipe "mysql"
  #   chef.add_role "web"
  #
  #   # You may also specify custom JSON attributes:
  #   chef.json = { :mysql_password => "foo" }
  # end

  # Enable provisioning with chef server, specifying the chef server URL,
  # and the path to the validation key (relative to this Vagrantfile).
  #
  # The Opscode Platform uses HTTPS. Substitute your organization for
  # ORGNAME in the URL and validation key.
  #
  # If you have your own Chef Server, use the appropriate URL, which may be
  # HTTP instead of HTTPS depending on your configuration. Also change the
  # validation key to validation.pem.
  #
  # config.vm.provision :chef_client do |chef|
  #   chef.chef_server_url = "https://api.opscode.com/organizations/ORGNAME"
  #   chef.validation_key_path = "ORGNAME-validator.pem"
  # end
  #
  # If you're using the Opscode platform, your validator client is
  # ORGNAME-validator, replacing ORGNAME with your organization name.
  #
  # If you have your own Chef Server, the default validation client name is
  # chef-validator, unless you changed the configuration.
  #
  #   chef.validation_client_name = "ORGNAME-validator"
end
```

one missing config entry
```ruby
config.vm.hostname = "hello.example.com"
```


### Nice to know
- The base directory gets automatically mounted to 
```bash
/vagrant
```
- Reload config changes
```bash
vagrant reload
```
- If you've messed it up, just trash the vm and load it again!
```bash
vagrant destroy
vagrant up
```


## Exercise
### Modify your vm

- set ***jap1.zuehlke.ch*** as hostname
- set ip 192.168.33.11
- set vm memory to 512 mb
- add a ***helloWorld.txt*** file that is available inside the vm at ***/vagrant***
- (optional, if ssh available) login as user ***vagrant*** using a common ssh client


## Solution (1/2)

Edit the ``Vagrantfile``

add line 
```
config.vm.hostname = "jap1.zuehlke.ch"
```
uncomment and edit line
```
config.vm.network "private_network", ip: "192.168.33.11"
```
uncomment the section and edit the memory line
```
config.vm.provider "virtualbox" do |vb|
  vb.customize ["modifyvm", :id, "--memory", "512"]
end
```


## Solution (2/2)

Create a file
```
echo "Hello" > helloWorld.txt
```
test
```bash
$ vagrant up
$ vagrant ssh
$ hostname -f
$ top
$ ls /vagrant
$ exit
```
optional
```bash
ssh vagrant@192.168.33.11
Password: vagrant
```



## Vagrant
### Provisioning

> Provisioners in Vagrant allow you to automatically install software, alter configurations, 
> and more on the machine as part of the ***vagrant up*** process

[From the Vagrant documentation](http://docs.vagrantup.com/v2/provisioning/index.htm)


Supported provisioner:

- Shell
- File
- Ansible
- CF Engine
- Chef (solo/client)
- Docker
- Puppet (standalone/agent)
- Salt


The ``Vagrantfile`` already contains some examples

```
# Enable provisioning with Puppet stand alone.  Puppet manifests
# are contained in a directory path relative to this Vagrantfile.
# You will need to create the manifests directory and a manifest in
# the file default.pp in the manifests_path directory.
#
# config.vm.provision "puppet" do |puppet|
#   puppet.manifests_path = "manifests"
#   puppet.manifest_file  = "site.pp"
# end
```


## Example

Adding this line to the configuration...

```ruby
config.vm.provision "shell",
    inline: "echo Hello, World"
```


will print out a message on first startup

```bash
$ vagrant destroy
$ vagrant up
==> default: Hello, World

or
$ vagrant provision
```



## Puppet


### What is puppet?
> Puppet is a declarative, model-based approach to IT automation, helping you manage infrastructure throughout its lifecycle, 
from provisioning and configuration to orchestration and reporting. 

http://puppetlabs.com/puppet/what-is-puppet


> Using Puppet, you can easily automate repetitive tasks, ...


Puppet can run in two modes:

- standalone
- client/server

Note:
The standalone mode will be sufficent in many cases, even for maintaining multiple servers.


### Structure

- puppet
 - manifests
   - nodes.pp
   - site.pp
 - modules
   - module_xy
     - files
     - manifests
     - templates

``site.pp`` is the main() in puppet

Note:
- Define modules and reference them from nodes.pp
- Work with templates to reuse your module
  - Ruby templates
  - http://docs.puppetlabs.com/guides/templating.html



## Puppet
### for developers


Design your system by defining resources like:

- file
- package
- exec

[The documentation](http://docs.puppetlabs.com/references/latest/type.html) is your friend!


### Syntax

```ruby
type { 'resource-title':
  attribute => 'value'
}
```
The resource-title must be unique!?


```ruby
file { '/var/tmp/helloWorld.txt':
  mode => 644,
  user => vagrant,
  group => vagrant,
  ensure => file,
  content => 'Hello world!'
}
```


### Provision a specific node

- You can manage multiple server by defining nodes
- Inheritence is possible

```ruby
node 'basic-server' {
	file { '/etc/hosts':
		ensure => file,
		content => '
192.168.33.10 jap.zuehlke.ch
192.168.33.11 jap1.zuehlke.ch
192.168.33.12 jap2.zuehlke.ch
		'
	}
}

node 'jap1', 'jap1.zuehlke.ch' inherits 'basic-server' {
	package { 'curl':
		ensure => present
	}
}
```


## Excercise
- Update package definitions by putting
```bash
aptitude update
```
to the shell provisioning
- Enable Puppet provisioning
- Create ``manifests/site.pp``
- Install Tomcat7
- Create new welcome page at
```
/var/lib/tomcat7/webapps/ROOT/index.html
```


## Excercise
### Hints
1. Work with a single ``site.pp`` in this excercise!
2. Trigger provisioning from within VM
```bash
sudo puppet apply site.pp
```
3. Find packages with
```bash
aptitude search {text}
```
4. Define the installation order
```ruby
require 	=> Package['curl'],
```


## Solution

1. Update package definition
```ruby
config.vm.provision "shell",
    inline: "aptitude update"
```
2. Uncomment puppet standalone in Vagrantfile
```ruby
config.vm.provision "puppet" do |puppet|
	puppet.manifests_path = "manifests"
	puppet.manifest_file  = "site.pp"
end
```

3. ``manifests/site.pp``
```ruby
node 'jap1', 'jap1.zuehlke.ch' {
	package { 'tomcat7':
		ensure 		=> present
	}
	file { '/var/lib/tomcat7/webapps/ROOT/index.html':
		require 	=> Package['tomcat7'],
		content 	=> 'Hello JAP'
	}
}
```


## Putting it all together
### How to deploy my webapp?


Mount and link!

Note:
- Mount with Vagrant
- Link with Puppet


## Tutorial

- Create a webapplication
```bash
mvn archetype:generate \
	-DgroupId=ch.zuehlke.jap \
	-DartifactId=jap-app \
	-DarchetypeArtifactId=maven-archetype-webapp \
	-DinteractiveMode=false
```

- Build it
```bash
cd jap-app
mvn clean install
```

- Log into your VM
```bash
vagrant ssh
```


- Have a look at ``/vagrant``
- Use Puppet to create a link in
```
/var/lib/tomcat7/webapps
```
to the real war file.

```ruby
file { '/var/lib/tomcat7/webapps/jap-app.war':
	ensure => link,
	target => '/vagrant/jap-app/target/jap-app.war',
	require => Package['tomcat7']
}
```


- Run puppet to install the link
```bash
$ sudo puppet apply manifests/site.pp
```

-   Test your application. 
    Browse to http://192.168.33.11:8080/jap-app/


## And now throw it away!

- Delete your VM!
- Start it again!


```bash
$ vagrant destroy
$ vagrant up
```

Browse to:

- http://192.168.33.11:8080
- http://192.168.33.11:8080/jap-app/


## Reusing your VM

VMs can be exported and can be used as the base VM for other
Vagrant projects.

```bash
$ vagrant package
$ vagrant box add jap-app-dev package.box
$ vagrant box list
```
Use the new box
```bash
$ mkdir jap-box-demo
$ cd jap-box-demo
$ vagrant init jap-app-dev
```


###Please note##

- A good point to package your VM is after all server packages have been installed 
- Create a new Vagrant project for your application and do the linking of the war file there 
- This way the box is really reusable



## What's next?

Think about:

- Jenkins integration
- Build the base server box daily with the latest package upgrades
  - Packages: tomcat7, splunk, load-balancer,...
- Building the dev box daily based on the server box
- Building the test/prod box daily based on the server box that installs the WAR-files
- Automatically start the test-box and run tests



## do it!
