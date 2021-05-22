# Supported Platforms

The following virtual network devices are supported by **config-generate**:

| Virtual network device | netsim device type |
|------------------------|--------------------|
| Arista vEOS            | eos                |
| Arrcus ArcOS           | arcos              |
| Cisco IOSv             | iosv               |
| Cisco CRS 1000v        | csr                |
| Cisco Nexus 9300v      | nxos               |
| Cumulus Linux          | cumulus            |
| FRR 7.5.0              | frr                |
| Juniper vSRX 3.0       | vsrx               |

**Notes:**
* **netsim-tools** support FRR containers with **containerlab**. It seems that the FRR build tools changed the file system layout after release 7.5.0, crashing **containerlab** deployment process.

To specify the device type of a node in your virtual lab:

* Specify **device** property in node data

```
nodes:
- name: c_ios
  device: iosv
- name: c_csr
  device: csr
```

* Use **defaults.device** setting in lab topology

```
defaults:
  device: cumulus

nodes: [ s1, s2, s3 ]
```

## Supported Virtualization Providers

**config-generate** script can generate configuration files for these virtualization providers:

* [vagrant-libvirt](https://github.com/vagrant-libvirt/vagrant-libvirt), including support for *veryisolated* private networks (link type: **lan**) and P2P tunnels (link type: **p2p**).
* [Vagrant VirtualBox provider](https://www.vagrantup.com/docs/providers/virtualbox)
* [Containerlab](https://containerlab.srlinux.dev/)

You cannot use all supported network devices with all virtualization providers:

| Virtual network device | Vagrant<br />Libvirt | Vagrant<br />Virtualbox | Containerlab |
|------------------------|:-:|:-:|:-:|
| Arista vEOS            | ✅ | ✅ | ✅ |
| Arrcus ArcOS           | ✅ | ❌ | ❌ |
| Cisco IOSv             | ✅ | ❌ | ❌ |
| Cisco CRS 1000v        | ✅ | ❌ | ❌ |
| Cisco Nexus 9300v      | ✅ | ✅ | ❌ |
| Cumulus Linux          | ✅ | ✅ | ❌ |
| FRR 7.5.0.             | ❌ | ❌ | ✅ |
| Juniper vSRX 3.0       | ✅ | ❌ | ❌ |

**Notes:**
* It's possible to run Cisco IOSv/CSR or Juniper vSRX under Virtualbox if you build your own Vagrant boxes.
* After building Vagrant boxes, edit **devices** section of **topology-defaults.yml** file to add Virtualbox support for individual network devices.
* If you feel like building a downloadable Vagrant box for FRR, please send us the box name and we'll add it to **topology-defaults.yml** file.

## Configuration Deployments

Ansible playbooks included with **netsim-tools** can deploy and collect device configuration on these network operating systems:

| Operating system | Deploy configuration | Collect configuration |
|------------------------|:-:|:-:|
| Arista EOS             | ✅ | ✅ |
| Arrcus ArcOS           | ✅ | ✅ |
| Cisco IOS / IOS XE     | ✅ | ✅ |
| Cisco Nexus OS         | ✅ | ✅ |
| Cumulus Linux          | ✅ | ✅ |
| FRR container          | ✅ | ❌ |
| Juniper vSRX 3.0       | ✅ | ✅ |

## Initial Device Configurations

The following system-wide features are configured on supported network operating systems as part of initial device configuration:

| Operating system | Hostname | IPv4 hosts | LLDP | Loopback<br />IPv4 address|Loopback<br />IPv6 address |
|------------------------|:-:|:-:|:-:|:-:|:-:|
| Arista EOS             | ✅ | ✅ | ✅ | ✅ | ✅ |
| Arrcus ArcOS           | ✅ | ❌ | ✅ | ✅ | ✅ |
| Cisco IOS/IOS XE       | ✅ | ✅ | ✅ | ✅ | ✅ |
| Cisco Nexus OS         | ✅ | ✅ | ✅ | ✅ | ✅ |
| Cumulus Linux          | ✅ | ✅ | ✅ | ✅ | ✅ |
| FRR 7.5.0              | ✅ | ❌ | ❌ | ✅ | ✅ |
| Juniper vSRX 3.0       | ✅ | ✅ | ✅ | ✅ | ✅ |

The following interface parameters are configured on supported network operating systems as part of initial device configuration:

| Operating system | IPv4<br />addresses | IPv6<br />addresses | Unnumbered<br />interfaces | Interface<br />description | Interface<br />bandwidth |
|------------------------|:-:|:-:|:-:|:-:|:-:|
| Arista EOS             | ✅ | ✅ | ✅ | ✅ | ✅ |
| Arrcus ArcOS           | ✅ | ✅ | ❌ | ❌ | ❌ |
| Cisco IOS/IOS XE       | ✅ | ✅ | ✅ | ✅ | ✅ |
| Cisco Nexus OS         | ✅ | ✅ | ✅ | ✅ | ✅ |
| Cumulus Linux          | ✅ | ✅ | ✅ | ✅ | ✅ |
| FRR 7.5.0              | ✅ | ✅ | ❌ | ✅ | ✅ |
| Juniper vSRX 3.0       | ✅ | ✅ | ✅ | ✅ | ✅ |

## Supported Configuration Modules

Individual **netsim-tools** configuration modules are supported on these devices:

| Operating system | OSPF | IS-IS | BGP | SR-MPLS |
|------------------------|:-:|:-:|:-:|:-:|
| Arista EOS             | ✅ | ✅ | ✅ | ✅ 
| Arrcus ArcOS           | ✅ | ❌ | ❌ | ❌ |
| Cisco IOS/IOS XE       | ✅ | ✅ | ✅ | ✅ |
| Cisco Nexus OS         | ✅ | ✅ | ✅ | ❌ |
| Cumulus Linux          | ✅ | ❌ | ✅ |  ❌ |
| FRR 7.5.0              | ✅ | ✅ | ✅ | ❌ |
| Juniper vSRX 3.0       | ✅ | ✅ | ✅ | ❌ |

### Vagrant with VirtualBox

* Most networking vendors don't ship Vagrant boxes, and I had no interest in building VirtualBox boxes from scratch after setting up a *libvirt*-based lab on an Intel NUC. The only boxes I could get with zero hassle were Cisco Nexus 9300v and Arista vEOS, and they both work fine. If you want to add other devices, you'll have to modify *topology-defaults.yml* file.
* The latest version of Arista vEOS available as Vagrant box for VirtualBox is 4.21.14M.
* Vagrantfile created by **create-topology** sets up port forwarding for SSH (22), HTTP (80) and NETCONF (830), but the corresponding Ansible inventory contains only **ansible_port** (SSH). You could edit the final inventory by hand, add extra file to `host_vars`, or fix my code. Should you decide to do the latter, please contact me in advance to discuss the necessary data structures.

### Containerlab

* The only devices currently supported are Arista cEOS and FRR
* Feel free to extend the templates and defaults to support other network devices
