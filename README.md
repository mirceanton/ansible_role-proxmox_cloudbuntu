Proxmox: Cloud VM Template
==========================

This role automatically downloads the cloud image file and configures a VM template for you to use on your Proxmox system, paving your way into the world of IaC.

Requirements
------------

N/A

Role Variables
--------------

**Required Variables**:

> These variables are required and the playbook will not run without them!

|   Variable   |                  Description                   |
| :----------: | :--------------------------------------------: |
|  `vm_vmid`   |               the VMID of the VM               |
|  `vm_name`   | the name of the VM (will also be the hostname) |
| `vm_storage` |       the storage device to hold the VM        |

**Recommended Variables**:

> These variables are not required, but are most likely ones you will want to customize

|        Variable         |                                     Default                                     |                              Description                              |
| :---------------------: | :-----------------------------------------------------------------------------: | :-------------------------------------------------------------------: |
|       `vm_net_ip`       |                                    `ip=dhcp`                                    |               the ip configuration in cloudinit format                |
|     `vm_nameserver`     |                                   `UNDEFINED`                                   |         the dns server to set in the cloudinit configuration          |
|    `vm_searchdomain`    |                                   `UNDEFINED`                                   |        the searchdomain to set in the cloudinit configuration         |
|   `vm_cloudinit_user`   |                                   `UNDEFINED`                                   |                the username to configure for cloudinit                |
| `vm_cloudinit_password` |                                   `UNDEFINED`                                   |                the password to configure for cloudinit                |
| `vm_cloudinit_ssh_keys` |                                   `UNDEFINED`                                   |          a list of ssh keys to pass to the VM via cloudinit           |
|    `cloud_image_url`    | `https://cloud-images.ubuntu.com/jammy/current/jammy-server-cloudimg-amd64.img` | the link to the cloud image file to download, ubuntu 22.04 by default |
|   `cloud_image_dest`    |            `/var/lib/vz/template/iso/ubuntu-server-jammy-cloud.img`             |          the destination path to store the downloaded image           |

**Optional Variables**:

> These variables are most likely fine to be left with their defaults

|         Variable          |        Default         |                  Description                  |
| :-----------------------: | :--------------------: | :-------------------------------------------: |
|        `vm_ostype`        |         `l26`          |          the os type of the machine           |
|       `vm_machine`        |          `pc`          |        the machine type, `q35` or `pc`        |
|         `vm_cpu`          |         `host`         |      the cpu type to set to the machine       |
|        `vm_cores`         |          `1`           |              number of CPU cores              |
|         `vm_ram`          |         `1024`         |        RAM in megabytes, 1G by default        |
|      `vm_net_driver`      |        `virtio`        |       the driver for the network device       |
|      `vm_net_bridge`      |        `vmbr0`         |        the bridge to assign to the NIC        |
|        `vm_scsihw`        |   `virtio-scsi-pci`    |               the scsi hardware               |
|       `vm_disksize`       |          `4G`          |           the size of the boot disk           |
|         `vm_bios`         |       `seabios`        |      the bios type, `seabios` or `ovmf`       |
|  `proxmox_snippets_path`  | `/var/lib/vz/snippets` |    the path to store cloud-config snippets    |
| `proxmox_snippets_device` |        `local`         | the storage device assigned to store snippets |

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
        vm_vmid: 9000
        vm_name: ubuntu-22.04-cloud
        vm_storage: local-vm

        vm_nameserver: 192.168.35.1
        vm_searchdomain: local
        vm_net_ip: "ip=192.168.35.47/24,gw=192.168.35.1"

        vm_cloudinit_user: srvadmin
        vm_cloudinit_password: test123
        vm_cloudinit_ssh_keys:
          - <ssh-key-here>
          - <ssh-key-here>
```

License
-------

MIT

Author Information
------------------

A role developed by [Mircea-Pavel ANTON](https://www.mirceanton.com).
