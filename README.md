#### Build Amazon AMI with Packer

[Packer](http://packer.io/) configures Amazon AMI and [Vagrant](https://www.vagrantup.com) box.

```bash
$ packer build -var-file aws-access.json packer-ami-vagrant.json
```

Create *aws-access.json*

```javascript
{
  "aws_access_key": "[YOUR AWS ACCESS KEY]",
  "aws_secret_key": "[YOUR AWS SECRET KEY]"
}
```

#### Deploy AWS EC2 with Vagrant

Install using standard Vagrant 1.1+ plugin installation methods. After installing, vagrant up and specify the aws provider. 

```bash
$ vagrant plugin install vagrant-aws

$ vagrant init ubuntu-aws packer_amazon-ebs_aws.box 
```

Modify *Vagrantfile* according to the following file

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu-aws"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "build/ubuntu_12.04_amd64_aws.box"

  config.vm.provider :aws do |aws, override|
    aws.access_key_id = "YOUR KEY"
    aws.secret_access_key = "YOUR SECRET KEY"
    aws.keypair_name = "KEYPAIR NAME"

    aws.region = "ap-southeast-2"
    
    override.ssh.username = "ubuntu"
    override.ssh.private_key_path = "PATH TO YOUR PRIVATE KEY"
  end
end
```

Start EC2 instance via Vagrant

```bash
$ vagrant up --provider=aws

$ vagrant ssh
```

#### Alternative: Convert EC2 AMI to VMDK for Vagrant

http://smashingboxes.com/ideas/how-to-convert-ec2-ami-to-vmdk-for-vagrant
