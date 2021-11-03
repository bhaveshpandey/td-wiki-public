# Raspberry Pi - Ubuntu

## Download and flash the image

## Figure out DHCP allotted IP addresses for hosts

Each host will be allotted a **dynamic** IP address which will change from time to time. This presents a challenge while trying to setup any kind of a server on the host. We can remedy this by configuring a **static** IP address on the host. However, for this we will also need to know the IP address of devices in the first place.

This can be accomplished by `arp-scan` command line tool. We can determine/filter the **Raspberry Pi** devices by searching for specific `MAC` address substrings which are unique to it. A bash example is shown below.

```shell

sudo arp-scan 192.168.1.0/24 | grep "e4:5f:01\|dc:a6:32\|3A:35:41" | awk '{print $1}'
```

## Prep hosts for Ansible
Copy ssh keys for communication with Ansible
 * ssh-copy-id ubuntu@192.168.1.xxx

## Configure using Ansible
* Set the host name supplied by the `new_hostname` variable.
