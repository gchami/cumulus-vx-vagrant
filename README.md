# ceng-packer-vagrant
Packer &amp; Vagrant configuration for building Vagrant boxes from Cumulus VM Lite OVA file

[Packer](https://www.packer.io/) is a popular tool for modifying and provisioning virtual machines, particularly virtual machine images intended for use with [Vagrant](https://www.vagrantup.com/).

Vagrant is a lightweight virtual machine abstraction layer that can create, provision and manage virtual machines across platforms and hypervisors.

## Files

There are three files in this repository:

### packer/cumulus.json

The Packer build configuration. Contains the information Packer needs to produce the Vagrant box file(s) from the OVA.

### scripts/setup.sh

Invoked during the Packer build process during the provisioning step. This script runs *inside* of the virtual machine as it is being built.

### vagrant/Vagrantfile

An example Vagrantfile for use with the Vagrant box file produced by Packer.

## Dependencies

* [VirtualBox](https://www.virtualbox.org/)
* [Packer](https://www.packer.io/)
* Enough disk space for both the OVA and the box file, and enough memory to create 1GB virtual machine.

## Building a Vagrant box file

* Place the Cumulux VX 2.5.3 OVA image in the same directory as this README. Name the file `CumulusLinux-2.5.3.ova`
* Run Packer with `packer build packer/cumulus.json`
* Packer will produce a Vagrant "box" file named `cumulus-vx-2.5.3.box`

Currently the configuration is hard-coded into the Packer configuration and setup script. If you wish to make any changes to the build process, modify the `packer/cumulus.json` and `scripts/setup.sh` files and re-run the build process.

## Using the Vagrant box file

* Import the `cumulus-vx-2.5.3.box` into Vagrant with `vagrant box add cumulux-vx cumulus-vx-2.5.3.box`
* Copy (or symlink) the `vagrant/Vagrantfile` file to a working directory and run `vagrant up`
* When Vagrant has started the virtual machine, you can log in with `vagrant ssh`.
* When you are finished, you can destroy the virtual machine instance with `vagrant destroy`