# DevCloud Mac

DevCloud Appliance for Mac OS (Apple Silicon) CloudStack-KVM development and testing.

This is a specially built VM appliance that can run on Mac OS 15+ with M3 or newer chip. The VM appliance is run as a KVM host and NFS server, while the host OS (Mac) is used to run CloudStack management/usage server, MySQL database, and npm/UI server, as well as IDEs and other tools for [CloudStack development](https://github.com/shapeblue/hackerbook/blob/main/2-dev.md). Advanced users may also use the appliance to create all-in-a box setup to try out CloudStack while on Mac.

The x86/Linux users and developers, can continue to use mbx: https://github.com/shapeblue/mbx or DIY their own appliance.

<img width="924" alt="Screenshot 2024-12-10 at 2 12 57 PM" src="https://github.com/user-attachments/assets/b0ac1e90-d25c-4dc7-9db2-f8a15842eeab">

## Requirements

* Apple Mac OS 15 or above, with M3 processor or newer, minimum 8GB spare memory and 100G disk space
* UTM v4.6 and above https://github.com/utmapp/UTM/releases

## Usage

TODO: (to test/fix)

* Download and import the .utm appliance in the UTM app, start the machine.
* The pre-built appliance has two users: `root` and `devcloud`, the password for both the users is `password`.
* To ssh use:
```
  ssh root@devcloud.local
```
* For Cockpit UI, visit: `https://devcloud.local:9090`.

## DIY Notes

Advanced DIY users and developers can use the following to build their own:

* Download Fedora or similar distro's AARCH64/ARM64 ISO which has latest Linux kernel with support for M-series CPU & KVM
* Example, ISO URL: https://archive.fedoraproject.org/pub/fedora/linux/releases/41/Server/aarch64/iso/
* Download and install UTM 4.6 or later
* Create a new VM using the downloaded ISO and select "Apple Virtualisation", and at least 4 CPU cores and 4GB RAM and 100G disk on shared network
* UTM shared network is usually on the host-only subnet: `192.168.64.0/24`, otherwise using `ifconfig` on Mac Terminal to find the bridge/network
* Install Fedora Server, and other dependencies as they would on a rpm/EL-based distro to use the appliance as a KVM host, or all-in-a-box to build test CloudStack deployment.
* If ACS rpms aren't installing, such as case with cloudstack-common, try `rpm -ivh cloudstack-common*.rpm --nodeps`
* Note: before deploying the zone, please seed the ARM64/aarch64 systemvmtemplate on the NFS/secondary storage. Such as: https://download.cloudstack.org/systemvm/4.20/systemvmtemplate-4.20.0-aarch64-kvm.qcow2.bz2 for ACS 4.20.0.
