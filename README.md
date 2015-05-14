#### Build Amazon AMI with Packer

[Packer](http://packer.io/) configures Amazon AMI and [Vagrant](https://www.vagrantup.com) box.

```bash
packer build -var-file aws-access.json packer-ami-vagrant.json
```

Create *aws-access.json*

```javascript
{
  "aws_access_key": "[YOUR AWS ACCESS KEY]",
  "aws_secret_key": "[YOUR AWS SECRET KEY]"
}
```

#### Deploy AWS EC2 with Vagrant

Install using standard Vagrant 1.1+ plugin installation methods. After installing, vagrant up and specify the aws provider. An example is shown below.

```bash
$ vagrant plugin install vagrant-aws
$ vagrant up --provider=aws
```

#### Convert EC2 AMI to VMDK for Vagrant

http://smashingboxes.com/ideas/how-to-convert-ec2-ami-to-vmdk-for-vagrant
