Proxmox: Cloudbuntu
===================

An Ansible role that configures an Ubuntu VM template based on the cloud image with support for cloudinit on a Proxmox VE host.

Requirements
------------

N/A

Role Variables
--------------

**Required Variables**:

> These variables are required and the playbook will not run without them!

|             Variable             |  Type  |            Description            |
| :------------------------------: | :----: | :-------------------------------: |
|    `proxmox_cloudbuntu_vmid`     |  int   |        the VMID of the VM         |
| `proxmox_cloudbuntu_disk_device` | string | the storage device to hold the VM |

**Recommended Variables**:

> These variables are not required, but are most likely ones you will want to customize

|               Variable               |   Default    |                      Description                       |
| :----------------------------------: | :----------: | :----------------------------------------------------: |
|      `proxmox_cloudbuntu_name`       | `cloudbuntu` |                   the name of the VM                   |
|   `proxmox_cloudbuntu_ci_ipconfig`   |  `ip=dhcp`   |        the ip configuration in cloudinit format        |
|  `proxmox_cloudbuntu_ci_nameserver`  | `UNDEFINED`  |  the dns server to set in the cloudinit configuration  |
| `proxmox_cloudbuntu_ci_searchdomain` | `UNDEFINED`  | the searchdomain to set in the cloudinit configuration |
|     `proxmox_cloudbuntu_ci_user`     | `UNDEFINED`  |        the username to configure for cloudinit         |
|     `proxmox_cloudbuntu_ci_pass`     | `UNDEFINED`  |        the password to configure for cloudinit         |
|     `proxmox_cloudbuntu_ci_keys`     | `UNDEFINED`  |   a list of ssh keys to pass to the VM via cloudinit   |

To check the default variables, take a look at the [defaults](defaults/main.yml) file.

Dependencies
------------

N/A

Example Playbook
----------------

``` yaml
---
- hosts: pve
  remote_user: root

  roles:
    - role: mirceanton.proxmox_cloudbuntu
      vars:
        proxmox_cloudbuntu_vmid: 9000
        proxmox_cloudbuntu_name: ubuntu-22.04-cloud
        proxmox_cloudbuntu_disk_device: local-vm

        proxmox_cloudbuntu_ci_nameserver: 192.168.35.1
        proxmox_cloudbuntu_ci_searchdomain: local
        proxmox_cloudbuntu_ci_ipconfig: "ip=192.168.35.47/24,gw=192.168.35.1"

        proxmox_cloudbuntu_ci_user: srvadmin
        proxmox_cloudbuntu_ci_pass: test123
        proxmox_cloudbuntu_ci_keys:
          - <ssh-key-here>
          - <ssh-key-here>
```

License
-------

MIT

Author Information
------------------

A role developed by [Mircea-Pavel ANTON](https://www.mirceanton.com).
