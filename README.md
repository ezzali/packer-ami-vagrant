[Packer](http://packer.io/) configures Amazon AMI and [Vagrant](https://www.vagrantup.com) box.

```bash
packer build -var-file access.json packer-ami-vagrant.json
```

Convert EC2 AMI to VMDK for Vagrant

http://smashingboxes.com/ideas/how-to-convert-ec2-ami-to-vmdk-for-vagrant
