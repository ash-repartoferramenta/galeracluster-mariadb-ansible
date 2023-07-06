# Automate the deploy of a simple Galera Cluster running on Centos 9 Stream

## Before we begin
**Requirements**
- HashiCorp Vagrant for building and deploying virtual inftractructures
>  https://developer.hashicorp.com/vagrant/downloads
- Virtualbox as virtualization engine  (the selected vagrant box supports also paralles, libvirt, hyperv and VMware workstation but you need to edit vagrant file accordingly)
> https://www.virtualbox.org/wiki/Downloads
- Ansible for provisioning the VMs
>  https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

**Disclaimer** 
The following project has been realised for training and learning purpose and the material here provided  is only suitable for testing and learning enviroments;
please review the code carefully before utilizing it for any other scope.

## Implementation description

![galera-ansible](https://github.com/ash-repartoferramenta/galeracluster-mariadb-ansible/assets/135543207/435f8056-f92d-4ff1-99e8-2171112e94a6)

## Vagrant

The  vagrant file available in the Vagrant folder deploy and builds recursivelty the number of VMs specified by the NODESNUMBER variable. 
The Vm's will be running the generic/centos9s box from Vagrant Cloud and the v.memory variable will define how much memory each node of the cluster will have.
Subsequently vagrant will set up a private network where the application will run and launch an ansible playbook for provisioning
the required applications.
For running the vagrant file you must travel to the Vagrant folder and use 
```
vagrant up
```
Vagrant will auto-generate an inventory for ansible with the informations provided in its Vagrantfile.
It's therefore important to set up correctly some variables.


**Security concerns:**
For the sake of ease of use, this Vagrantfile is set to utilize the default insecure ssh key provided by Vagrant

**Variables**
- v.memory: how much memory will be allocated to each VMs
- NODESNUMBER : number of nodes (and VM'd) vagrant will build
- IPSTART: host part of the ipv4 adress from which vagrant will start assigning addresses to galera nodes (see example)
- VNETWORK: Network part of the ipv4 address vagrant will use to assign addresses to galera nodes (see example)

> Example:
> if NODESNUMBER is 3, VNETWORK is 192.168.1 and IPSTART is 5, 3 VMs will be created with the following addresses assigned:
> 192.168.1.6 , 192.168.1.7 , 192.168.1.8


