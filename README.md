# 🔐 Cybersecurity Lab Environment Setup

### Building a Virtual Cybersecurity Lab Using VMware Workstation and Kali Linux

![Cybersecurity](https://img.shields.io/badge/Skill-Cybersecurity-red)
![Virtualization](https://img.shields.io/badge/Virtualization-VMware-blue)
![Operating System](https://img.shields.io/badge/OS-Kali%20Linux-557C94)
![Networking](https://img.shields.io/badge/Network-10.0.0.0%2F24-green)
![Internship](https://img.shields.io/badge/Internship-Networkwalks-orange)

---

## 📌 Project Overview

This project documents the setup and configuration of a virtual cybersecurity laboratory as part of **Week 1, Project Module 1 (PM1)** of my cybersecurity internship at **Networkwalks**.

The lab environment was created using VMware Workstation and Kali Linux to provide a controlled environment for learning cybersecurity concepts, network configuration, Linux administration, and authorized security testing.

The primary objective was to establish a functional virtual machine with internet connectivity, static IP addressing, VMware Tools integration, and file-sharing capabilities.

---

## 🎯 Objectives

The main objectives of this project were:

1. Set up a Kali Linux virtual machine using VMware Workstation.
2. Configure a NAT network with the subnet `10.0.0.0/24`.
3. Assign a static IP address of `10.0.0.2/24` to Kali Linux.
4. Configure the default gateway and DNS servers.
5. Verify internet connectivity and DNS resolution.
6. Install and verify VMware Tools.
7. Enable bidirectional clipboard sharing between Windows and Kali Linux.
8. Configure a shared folder for transferring files.
9. Practise basic Linux terminal commands.
10. Create a virtual machine snapshot for recovery.

---

## 🛠️ Tools and Technologies Used

| Component | Technology |
|---|---|
| Host Operating System | Windows |
| Virtualization Software | VMware Workstation |
| Guest Operating System | Kali Linux |
| Network Type | NAT |
| Network Subnet | 10.0.0.0/24 |
| Static IP Address | 10.0.0.2/24 |
| Default Gateway | 10.0.0.1 |
| DNS Servers | 8.8.8.8, 1.1.1.1 |
| Guest Integration | open-vm-tools |
| Shared Folder | Windows Downloads |
| Network Configuration Tool | NetworkManager |

---

## ⚙️ Lab Setup and Configuration

### Step 1: Kali Linux Virtual Machine

An existing Kali Linux virtual machine was used in VMware Workstation.

The VM was configured to use VMware's NAT networking mode.

This allows the guest operating system to access external networks through the host while remaining on a separate virtual subnet.

![Kali Linux Desktop](01_Kali_Linux_Desktop.png)

---

### Step 2: NAT Network Configuration

VMware Virtual Network Editor was used to configure the VMnet8 NAT network.

**Network Configuration:**

- Virtual Network: VMnet8
- Network Type: NAT
- Subnet: `10.0.0.0/24`
- Subnet Mask: `255.255.255.0`
- NAT Gateway: `10.0.0.1`

The NAT gateway was configured to avoid conflicts with Kali Linux's required static IP address.

![VMware NAT Configuration](03_VMware_NAT_Configuration.png)

---

### Step 3: Static IP Address Configuration

A static IPv4 address was configured on Kali Linux using NetworkManager.

**Configuration:**

| Parameter | Value |
|---|---|
| Interface | eth0 |
| IPv4 Address | 10.0.0.2 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 10.0.0.1 |
| Primary DNS | 8.8.8.8 |
| Secondary DNS | 1.1.1.1 |

The following command was used to verify the IP address:

```bash
ip -4 addr show eth0
```

The routing configuration was verified using:

```bash
ip route
```

The expected default route was:

```text
default via 10.0.0.1 dev eth0
```

![Kali Static IP Configuration](02_Kali_Static_IP.png)

---

### Step 4: Internet Connectivity Verification

Internet connectivity was tested using ICMP ping commands.

**Test 1: External IP connectivity**

```bash
ping -c 4 8.8.8.8
```

**Test 2: DNS resolution**

```bash
ping -c 4 google.com
```

Both tests completed successfully with 0% packet loss during verification.

This confirmed that Kali Linux could access external networks and resolve domain names.

![Internet Connectivity](04_Internet_Connectivity.png)

---

### Step 5: VMware Tools Installation

VMware Tools integration was configured using the following packages:

- `open-vm-tools`
- `open-vm-tools-desktop`

The installed packages were verified using:

```bash
dpkg -l open-vm-tools open-vm-tools-desktop
```

Both packages were confirmed to be installed.

VMware guest integration was used to support clipboard sharing and shared-folder functionality.

![VMware Tools Installation](05_VMware_Tools_Installed.png)

---

### Step 6: Shared Folder Configuration

A shared folder was configured to allow file transfers between Windows and Kali Linux.

**Host Folder:** Windows Downloads

**Shared Folder Name:** `Downloads`

**Kali Mount Location:**

```text
/mnt/hgfs/Downloads
```

The shared folder was mounted using VMware HGFS.

The following command was used to verify access to the test file:

```bash
ls -l /mnt/hgfs/Downloads/internship-test.txt
```

The test file was successfully accessible from Kali Linux and Windows.

Automatic mounting was also configured to preserve shared-folder access after restarting the VM.

![Shared Folder Verification](06_Shared_Folder_Verification.png)

---

### Step 7: Bidirectional Clipboard Integration

VMware guest isolation settings were configured to enable copy-and-paste functionality.

Clipboard sharing was tested in both directions:

- Windows → Kali Linux
- Kali Linux → Windows

Both tests were successful.

This allows commands and text to be transferred conveniently between the host and guest operating systems.

---

### Step 8: Basic Linux Commands

Basic Linux file and directory operations were practised inside the Kali terminal.

The following commands were executed:

```bash
mkdir -p ~/Desktop/Internship_Week1
cd ~/Desktop/Internship_Week1
echo "Cybersecurity Internship - Week 1 Lab Setup" > week1.txt
ls -l
cat week1.txt
```

These commands demonstrate:

- Creating directories
- Navigating between directories
- Creating text files
- Listing files
- Displaying file contents

![Basic Linux Commands](07_Basic_Linux_Commands.png)

---

### Step 9: Virtual Machine Snapshot

A VMware snapshot was created after completing the main lab configuration.

**Snapshot Name:**

`Week 1 - Cybersecurity Lab Setup`

The snapshot provides a recovery checkpoint that can be used to restore the virtual machine to its saved state if future configuration changes cause problems.

![VMware Snapshot](08_VMware_Snapshot.png)

---

## 🧪 Verification Results

| Test | Result |
|---|---|
| Kali Linux VM boots successfully | PASS |
| Static IP configuration | PASS |
| NAT network configuration | PASS |
| Internet connectivity | PASS |
| DNS resolution | PASS |
| VMware Tools installation | PASS |
| Windows → Kali clipboard | PASS |
| Kali → Windows clipboard | PASS |
| Shared-folder file transfer | PASS |
| Basic Linux commands | PASS |
| VMware snapshot creation | PASS |
| Drag-and-drop file transfer | NOT WORKING |

---

## ⚠️ Challenges Encountered

During the setup process, several configuration issues were encountered.

**1. NAT Gateway Conflict**

The initial NAT gateway configuration conflicted with the required Kali Linux static IP address.

This was resolved by configuring the NAT gateway as `10.0.0.1`.

**2. Internet Connectivity Issues**

Initial connectivity tests failed due to network configuration conflicts.

After adjusting the VMware virtual network settings, internet connectivity and DNS resolution were successfully restored.

**3. Shared Folder Mounting**

The shared folder was initially not accessible through the expected mount directory.

VMware HGFS was configured, and automatic mounting was enabled to provide access after restarting Kali Linux.

**4. Drag-and-Drop Integration**

VMware drag-and-drop file transfer remained unavailable despite troubleshooting.

However, bidirectional clipboard sharing and the Windows–Kali shared folder were successfully configured, providing an alternative method for transferring files.

---

## 📚 Learning Outcomes

Through this project, I gained practical experience in:

- Virtual machine management using VMware Workstation.
- NAT networking and IPv4 addressing.
- Static IP, gateway, and DNS configuration.
- Linux network troubleshooting.
- VMware guest integration.
- Shared-folder configuration.
- Basic Linux command-line operations.
- Virtual machine snapshots and recovery.

This project provided a foundation for future cybersecurity internship activities and authorized security testing in a controlled lab environment.

---

## 👨‍💻 Internship Information

**Organization:** Networkwalks  
**Batch:** B084  
**Week:** 1  
**Project Module:** PM1  
**Project:** Cybersecurity Lab Environment Setup  
**Virtualization Platform:** VMware Workstation  
**Guest OS:** Kali Linux

---

## 📌 Conclusion

The Week 1 cybersecurity lab environment was configured using VMware Workstation and Kali Linux.

The completed setup includes NAT networking, static IP addressing, internet connectivity, VMware Tools, bidirectional clipboard integration, shared-folder access, and a virtual machine snapshot.

The environment is ready for further learning and practical cybersecurity exercises, with drag-and-drop integration remaining an outstanding limitation.

---

**Cybersecurity Internship | Networkwalks | Batch B084**
