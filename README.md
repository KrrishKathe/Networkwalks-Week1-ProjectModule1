
# 🔐 Cybersecurity Lab Environment Setup

### Building a Virtual Lab for Ethical Hacking & Security Testing

![VirtualBox](https://img.shields.io/badge/VirtualBox-7.2-blue?style=for-the-badge&logo=virtualbox)
![Kali Linux](https://img.shields.io/badge/Kali%20Linux-2023.4-557C94?style=for-the-badge&logo=kalilinux)
![Network](https://img.shields.io/badge/Network-NAT%20Network-green?style=for-the-badge)
![Purpose](https://img.shields.io/badge/Purpose-Educational-orange?style=for-the-badge)

---

## 📌 Project Overview

This project involves setting up a virtual cybersecurity lab using Oracle VirtualBox and Kali Linux. The environment is intended for learning networking, exploring security tools, and performing authorized penetration-testing exercises in a controlled virtual environment.

The lab uses a custom NAT Network, allowing additional virtual machines to be connected in the future for cybersecurity practice.

## 🎯 Objectives

- Install and configure Oracle VirtualBox.
- Import Kali Linux as a virtual machine.
- Create a custom NAT Network using the `10.0.0.0/24` subnet.
- Configure Kali Linux networking.
- Enable clipboard sharing and drag-and-drop.
- Configure a shared folder between Windows and Kali Linux.
- Verify internet connectivity and DNS resolution.
- Create a clean virtual machine snapshot.

## ⚙️ Lab Configuration

| Component | Configuration |
|---|---|
| Host OS | Windows |
| Hypervisor | Oracle VirtualBox |
| Security OS | Kali Linux 2023.4 |
| VM RAM | 2048 MB (planned) |
| Network Type | NAT Network |
| Network Name | NatNetwork |
| Subnet | `10.0.0.0/24` |
| Kali IP | `10.0.0.2/24` |
| Default Gateway | `10.0.0.1` (verify) |
| DNS Server | `8.8.8.8` (if configured) |

## 🏗️ Lab Architecture

```text
          Windows Host Machine
                   |
            Oracle VirtualBox
                   |
             NAT Network
             10.0.0.0/24
                   |
             Kali Linux VM
             10.0.0.2/24
                   |
        Future Target Machines
             (Optional)
```

## 🪜 Lab Setup Procedure

### Step 1: Install 7-Zip

7-Zip is used to extract the compressed Kali Linux virtual machine archive.

Download: https://www.7-zip.org/download.html

### Step 2: Install VirtualBox

Oracle VirtualBox is used to create and manage virtual machines.

Download: https://www.virtualbox.org/wiki/Downloads

### Step 3: Download Kali Linux

Download the prebuilt VirtualBox image and extract it using 7-Zip.

Download: https://www.kali.org/get-kali/

### Step 4: Configure the NAT Network

Create a custom NAT Network with the following settings:

- Network Name: `NatNetwork`
- IPv4 Prefix: `10.0.0.0/24`
- DHCP: Enabled if required
- IPv6: Disabled for this lab

A NAT Network allows connected virtual machines to communicate with each other and access external networks through NAT.

### Step 5: Configure the Kali VM

Configure Adapter 1 in the Kali virtual machine settings:

- Attached to: NAT Network
- Network Name: `NatNetwork`

Target network configuration:

```text
IP Address:    10.0.0.2
Subnet Mask:   255.255.255.0
Gateway:       10.0.0.1
DNS Server:    8.8.8.8
```

Verify the network gateway and settings before applying the static IP configuration.

### Step 6: Enable Clipboard and Shared Folder

In VirtualBox VM Settings, configure:

- Shared Clipboard: Bidirectional
- Drag and Drop: Bidirectional
- Shared Folder: Windows Downloads folder

Install VirtualBox Guest Additions if required for clipboard and shared-folder functionality.

### Step 7: Verify Network Connectivity

Check the Kali IP address:

```bash
ip a
```

Check the default gateway:

```bash
ip route
```

Test gateway connectivity:

```bash
ping -c 4 10.0.0.1
```

Test internet connectivity:

```bash
ping -c 4 8.8.8.8
```

Test DNS resolution:

```bash
nslookup networkwalks.com
```

Check Nmap:

```bash
nmap --version
```

### Step 8: Create a VM Snapshot

After verifying the configuration, create a snapshot in VirtualBox.

Suggested snapshot name:

`Kali - Clean Network Baseline`

This snapshot can be used to restore the virtual machine before future experiments.

## 🧪 Verification Checklist

- [ ] Kali Linux starts successfully.
- [ ] NAT Network is configured.
- [ ] Kali IP address is `10.0.0.2/24`.
- [ ] Gateway connectivity is verified.
- [ ] Internet connectivity is verified.
- [ ] DNS resolution works.
- [ ] Clipboard and drag-and-drop work.
- [ ] Shared folder is accessible.
- [ ] Baseline snapshot is created.

## 🐞 Troubleshooting

### Internet Connectivity Issues

If Kali cannot access the internet:

1. Verify that the NAT Network is enabled.
2. Confirm that the Kali VM is connected to `NatNetwork`.
3. Check the IP address, gateway, and DNS settings.
4. Ensure no other VM uses the same static IP address.
5. Restart the network connection and test again.

To inspect the available network connections:

```bash
nmcli connection show
```

For certain Kali and VirtualBox networking issues, the following workaround may help. Replace the connection name if yours differs:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

### VirtualBox Startup Issues

If the VM fails to start, check whether hardware virtualization (Intel VT-x or AMD-V) is enabled in BIOS/UEFI.

## 💡 Key Learnings

- Understanding virtualization and virtual machines.
- Configuring NAT Network connectivity.
- Working with IPv4 addresses, gateways, and DNS.
- Testing connectivity using Linux networking commands.
- Managing shared folders and VM integration features.
- Creating snapshots for recovery.
- Preparing a reusable environment for cybersecurity practice.

## 🔐 Ethical Use

This lab is intended for educational purposes and authorized security testing only. Test only systems that you own or have explicit permission to assess.

## 🔗 Tools and Resources

- [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Kali Linux](https://www.kali.org/get-kali/)
- [7-Zip](https://www.7-zip.org/download.html)
- [Network Walks](https://www.networkwalks.com/)

## 👨‍💻 Project Information

**Program:** Cybersecurity at Network Walks  
**Task:** WK1-PM1  
**Project:** Cybersecurity Lab Environment Setup  
**Virtualization:** Oracle VirtualBox  
**Security VM:** Kali Linux 2023.4
