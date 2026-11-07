# 🔐 Cybersecurity Lab Environment Setup

### Networkwalks Cybersecurity Internship | Batch B084 | Week 1 | PM1

![Cybersecurity](https://img.shields.io/badge/Cybersecurity-Lab%20Setup-red)
![Kali Linux](https://img.shields.io/badge/OS-Kali%20Linux-blue)
![VMware](https://img.shields.io/badge/Virtualization-VMware-green)
![Status](https://img.shields.io/badge/Status-Partially%20Complete-yellow)

---

## 📌 Project Overview

This project documents the setup and configuration of a virtual cybersecurity laboratory as part of **Week 1, Project Module 1 (PM1)** of my cybersecurity internship at **Networkwalks**.

The lab was configured using **VMware Workstation and Kali Linux** to provide a controlled environment for learning cybersecurity concepts, Linux administration, networking, and practical security testing.

The environment includes NAT networking, static IP addressing, internet connectivity, VMware Tools integration, shared-folder access, and a virtual machine snapshot.

---

## 🎯 Project Objectives

The objectives of this project were:

1. Configure a Kali Linux virtual machine.
2. Set up NAT networking using the subnet `10.0.0.0/24`.
3. Assign the static IP address `10.0.0.2/24`.
4. Configure the default gateway and DNS servers.
5. Verify internet connectivity.
6. Install and verify VMware Tools.
7. Enable bidirectional clipboard integration.
8. Configure Windows–Kali file sharing.
9. Practise basic Linux commands.
10. Create a virtual machine snapshot.

---

## 🛠️ Tools and Technologies

| Component | Configuration |
|---|---|
| Host Operating System | Windows |
| Virtualization Platform | VMware Workstation |
| Guest Operating System | Kali Linux |
| Network Mode | NAT |
| Virtual Network | VMnet8 |
| Subnet | 10.0.0.0/24 |
| Static IP | 10.0.0.2/24 |
| Default Gateway | 10.0.0.1 |
| DNS Servers | 8.8.8.8, 1.1.1.1 |
| VMware Integration | open-vm-tools |
| Shared Folder | Windows Downloads |

---

# ⚙️ Lab Setup Procedure

## Step 1: Kali Linux Virtual Machine

An existing Kali Linux virtual machine was configured using VMware Workstation.

The virtual machine was connected to VMware's NAT network to provide internet connectivity through the Windows host.

### Screenshot

![Kali Linux Desktop](./Kali%20Linux%20Desktop.png)

---

## Step 2: NAT Network Configuration

The VMware Virtual Network Editor was used to configure the VMnet8 network.

**Network settings:**

- Network Type: NAT
- Virtual Network: VMnet8
- Subnet IP: `10.0.0.0`
- Subnet Mask: `255.255.255.0`
- NAT Gateway: `10.0.0.1`

The NAT gateway was configured to avoid an IP address conflict with the Kali Linux virtual machine.

### Screenshot

![VMware NAT Configuration](VMware%20NAT%20Configuration.png)

---

## Step 3: Static IP Configuration

A static IP address was assigned to Kali Linux using NetworkManager.

**Network configuration:**

| Parameter | Value |
|---|---|
| Interface | eth0 |
| IP Address | 10.0.0.2 |
| Subnet Mask | 255.255.255.0 |
| Gateway | 10.0.0.1 |
| Primary DNS | 8.8.8.8 |
| Secondary DNS | 1.1.1.1 |

The IP address was verified using:

```bash
ip -4 addr show eth0
```

The routing table was checked using:

```bash
ip route
```

The default route was configured through `10.0.0.1`.

### Screenshot

![Kali Static IP](Kali%20Static%20IP.png)

---

## Step 4: Internet Connectivity Verification

Internet connectivity was tested using the following commands:

**External IP connectivity:**

```bash
ping -c 4 8.8.8.8
```

**DNS resolution:**

```bash
ping -c 4 google.com
```

Both tests were successful, confirming internet access and DNS resolution.

### Screenshot

![Internet Connectivity](Internet%20Connectivity.png)

---

## Step 5: VMware Tools Installation

VMware Tools integration was configured using:

- `open-vm-tools`
- `open-vm-tools-desktop`

The installed packages were verified using:

```bash
dpkg -l open-vm-tools open-vm-tools-desktop
```

Both packages were successfully installed.

VMware Tools provides guest integration features such as clipboard sharing and shared-folder support.

### Screenshot

![VMware Tools Installed](VMware%20Tools%20Installed.png)

---

## Step 6: Shared Folder Configuration

A shared folder was configured between Windows and Kali Linux.

**Shared folder details:**

- Host Folder: Windows Downloads
- VMware Share Name: `Downloads`
- Kali Mount Point: `/mnt/hgfs/Downloads`

The shared folder was mounted using VMware HGFS.

The following command verified access to the shared test file:

```bash
ls -l /mnt/hgfs/Downloads/internship-test.txt
```

The test file was accessible from both Windows and Kali Linux.

Automatic mounting was configured to preserve shared-folder access after restarting Kali.

### Screenshot

![Shared Folder Verification](Shared%20Folder%20Verification.png)

---

## Step 7: Bidirectional Clipboard Integration

VMware guest isolation settings were configured to enable clipboard sharing.

Clipboard functionality was tested in both directions:

- Windows → Kali Linux
- Kali Linux → Windows

Both tests were successful.

This allows text and commands to be copied between the host and guest operating systems.

---

## Step 8: Basic Linux Commands

Basic Linux file and directory management commands were practised.

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
- Navigating directories
- Creating files
- Listing directory contents
- Reading text files

### Screenshot

![Basic Linux Commands](Basic%20Linux%20Commands.png)

---

## Step 9: Virtual Machine Snapshot

A VMware snapshot was created after completing the main lab configuration.

**Snapshot name:**

`Week 1 - Cybersecurity Lab Setup`

The snapshot provides a recovery checkpoint that can be used to restore the virtual machine to its saved state.

### Screenshot

![VMware Snapshot](VMware%20Snapshot.png)

---

# 🧪 Verification Results

| Test | Status |
|---|---|
| Kali Linux VM | PASS |
| NAT Configuration | PASS |
| Static IP Configuration | PASS |
| Internet Connectivity | PASS |
| DNS Resolution | PASS |
| VMware Tools Installation | PASS |
| Bidirectional Clipboard | PASS |
| Shared Folder File Transfer | PASS |
| Basic Linux Commands | PASS |
| VM Snapshot | PASS |
| Drag-and-Drop File Transfer | NOT WORKING |

---

# ⚠️ Challenges Encountered

### 1. NAT Gateway Conflict

The initial NAT gateway configuration conflicted with Kali Linux's required static IP address.

**Resolution:** The gateway was configured as `10.0.0.1`.

### 2. Internet Connectivity

Initial internet connectivity tests failed due to network configuration conflicts.

**Resolution:** The VMware virtual network settings were adjusted, restoring internet connectivity.

### 3. Shared Folder Mounting

The Windows Downloads folder was initially inaccessible from Kali Linux.

**Resolution:** VMware HGFS was configured, and automatic mounting was enabled.

### 4. Drag-and-Drop Integration

VMware drag-and-drop file transfer remained unavailable after troubleshooting.

However, the shared folder and bidirectional clipboard were successfully configured, providing alternative file-transfer functionality.

---

# 📚 Learning Outcomes

Through this project, I gained practical experience with:

- VMware Workstation virtualization
- Kali Linux administration
- NAT networking
- IPv4 addressing
- Static IP configuration
- Gateway and DNS configuration
- Network troubleshooting
- VMware Tools integration
- Windows–Linux file sharing
- Basic Linux commands
- Virtual machine snapshots

---

# 👨‍💻 Internship Details

**Organization:** Networkwalks  
**Batch:** B084  
**Week:** 1  
**Project Module:** PM1  
**Project Title:** Cybersecurity Lab Environment Setup  
**Virtualization Platform:** VMware Workstation  
**Guest Operating System:** Kali Linux

---

# 🏁 Conclusion

The Week 1 cybersecurity lab environment was configured using VMware Workstation and Kali Linux.

The setup includes NAT networking, static IP addressing, internet connectivity, VMware Tools, bidirectional clipboard sharing, shared-folder access, and a virtual machine snapshot.

The environment provides a foundation for future cybersecurity learning and practical exercises. Drag-and-drop integration remains an outstanding limitation.

---

**Networkwalks Cybersecurity Internship | Batch B084 | Week 1**
