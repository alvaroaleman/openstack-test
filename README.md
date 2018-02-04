# Openstack test

A simple dev environment to play around with Packstack and new
Openstack versions.

Uses pike with OVN at the time of writing.

## Requirements

* A Linux box because of libvirt
* 12GiB of RAM
* [Vagrant](https://www.vagrantup.com/downloads.html)
* [Vagrant libvirt](https://github.com/vagrant-libvirt/vagrant-libvirt)
* [Ansible](https://docs.ansible.com/ansible/latest/intro_installation.html)

## Usage

* Clone the rep and run `vagrant up`
* Have some patience, provisioning takes ~30 minutes
