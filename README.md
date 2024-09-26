# Test RootKit

This repository is a test rootkit for educational purposes. It is not intended to be used for malicious purposes.

## Vagrant

We are using Vagrant to create a virtual machine to test the rootkit. To start the virtual machine, run the following command:

Please note that in my case i'm using KVM as the virtualization provider, so you may need change the provider in the following command based on your virtualization provider.

To use the Libvirt provider, you need some additional dependencies. You can install them by running the following command:

```bash
vagrant plugin install vagrant-libvirt
vagrant plugin install vagrant-mutate
```

```bash
vagrant up --provider=libvirt
```

By default, the virtual machine will be provisioned with 1 CPU and 1024 MB of RAM and also some default packages such as :

- build-essential
- linux-headers-$(uname -r)
- git

The virtual machine will also have the rootkit source code cloned in the `~/src` directory. To automatically sync the rootkit source code with the virtual machine, you can run the following command:

```bash
vagrant rsync-auto
```

> This will watch for any changes in the rootkit source code and automatically sync them with the virtual machine.

After the virtual machine is up and running, you can ssh into it by running the following command:

```bash
vagrant ssh
```

To stop the virtual machine, run the following command:

```bash
vagrant halt
```

To destroy the virtual machine, run the following command:

```bash
vagrant destroy
```

### Ressources

- [Vagrant](https://www.vagrantup.com/)
- [Vagrant Libvirt KVM](https://ostechnix.com/how-to-use-vagrant-with-libvirt-kvm-provider/)

## Rootkit

The rootkit is a simple kernel module for now.

### Build

To build the rootkit, run the following command:

```bash
make
```

### Load

To load the rootkit, run the following command:

```bash
sudo insmod test_rootkit.ko
```

### Unload

To unload the rootkit, run the following command:

```bash
sudo rmmod test_rootkit
```

### Logs

To view the logs, run the following command:

```bash
dmesg
```

### Clean

To clean the rootkit, run the following command:

```bash
make clean
```

### Ressources

- [Rootkit Tutorial using Vagrant](https://xcellerator.github.io/posts/linux_rootkits_01/)