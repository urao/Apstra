## Tested below configuration on Ubuntu 24.04

### Create non-root user

```
* useradd bobby
* usermod -aG sudo bobby
```

### Create VLAN 

```
apt-get install vlan net-tools
vconfig add eth1 2115
ifconfig eth1.2115 10.10.10.1/24 up
``` 

### Create Bond Interface

```
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: true
      dhcp6: true
    eth1:
      dhcp4: false
      dhcp6: false
    eth2:
      dhcp4: false
      dhcp6: false
  bonds:
    bond0:
      dhcp4: false
      dhcp6: false
      interfaces:
        - eth1
        - eth2
      parameters:
        mode: 802.3ad
        primary: eth1 #
        mii-monitor-interval: 5000 #
```
