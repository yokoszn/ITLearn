## Requirements

[](https://github.com/Orange-Cyberdefense/GOAD#requirements)

- Used space
    
    - The lab takes about 77GB (but you have to get the space for the vms vagrant images windows server 2016 (22GB) / windows server 2019 (14GB) / ubuntu 18.04 (502M))
    - The total space needed for the lab is ~115 GB (and more if you take snapshots)
- Linux operating system
    
    - The lab intend to be installed from a **Linux host** and was tested only on this.
    - Some people have successfully installed the lab from a windows OS, to do that they create the VMs with vagrant and have done the ansible provisioning part from a linux machine.
    - In this case the linux machine used to do the provisioning must be setup with one adapter on NAT and one adapter on the same virtual private network as the lab.

### tldr; quick install

[](https://github.com/Orange-Cyberdefense/GOAD#tldr-quick-install)

- You are on linux, you already got virtualbox, vagrant and docker installed on your host and you know what you are doing, just run :

```shell
./goad.sh -t check -l GOAD -p virtualbox -m docker
./goad.sh -t install -l GOAD -p virtualbox  -m docker
```

[[Virtual Machines to Hack - VulnHub]]  [[hacking]] #hands-on 

[GitHub - Orange-Cyberdefense/GOAD: game of active directory](https://github.com/Orange-Cyberdefense/GOAD)

## Installation

[](https://github.com/Orange-Cyberdefense/GOAD#installation)

- Installation depend of the provider you use, please follow the appropriate guide :
    
    - [Install with Virtualbox](https://github.com/Orange-Cyberdefense/GOAD/blob/main/docs/install_with_virtualbox.md)
    - [Install with VmWare](https://github.com/Orange-Cyberdefense/GOAD/blob/main/docs/install_with_vmware.md)
    - [Install with Proxmox](https://github.com/Orange-Cyberdefense/GOAD/blob/main/docs/install_with_proxmox.md)
    - [Install with Azure](https://github.com/Orange-Cyberdefense/GOAD/blob/main/docs/install_with_azure.md)
- Installation is in three parts :
    
    1. Templating : this will create the template to use (needed only for proxmox)
    2. Providing : this will instantiate the virtual machines depending on your provider
    3. Provisioning : it is always made with ansible, it will install all the stuff to create the lab