
# Windows VM Setup on Proxmox with Remote Access

## Overview
This guide covers the step-by-step process for setting up a Windows Virtual Machine (VM) on a Dell PowerEdge R620 server running Proxmox VE and configuring secure remote access via Microsoft Remote Desktop (RDP) on a MacBook.

---

## Hardware and Software Used
- **Server:** Dell PowerEdge R620 with Intel Xeon E5-2640 v2 CPU (8 cores, 16 threads)
- **Client:** 14" MacBook Pro (2021) with Apple M1 Pro (8 cores, 16 GB RAM)
- **Hypervisor:** Proxmox VE 8.3
- **VM OS:** Windows 10 Home Edition
- **Remote Access:** Microsoft Remote Desktop (Mac)
- **Network Security:** Tailscale VPN

---

## Setup Steps

### 1. **Proxmox Installation**
- Downloaded the Proxmox VE 8.3 ISO.
- Created a bootable USB with Proxmox using the `dd` command on the MacBook.
- Installed Proxmox on the Dell PowerEdge R620.
- Configured network settings in the BIOS/iDRAC.

### 2. **Windows VM Creation**
- Uploaded the **Windows 10 ISO** and **VirtIO Drivers ISO** to Proxmox.
- Created a new VM with the following specs:
  - **CPU:** 4 cores (host type)
  - **RAM:** 12 GB
  - **Disk:** 100 GB (VirtIO Block with Writeback cache)
- Mounted the Windows ISO and VirtIO ISO to the VM.

### 3. **Windows Installation**
- Booted the VM into the Windows installer.
- Loaded **VirtIO storage drivers** during installation to detect the hard disk.
- Completed Windows installation.

### 4. **VirtIO Drivers Installation**
- Installed all VirtIO drivers for **network**, **disk**, and **QEMU Guest Agent**.
- Enabled **QEMU Guest Agent** in Proxmox for better integration.

### 5. **Networking Setup**
- Installed **Tailscale VPN** on both the Windows VM and MacBook.
- Logged into Tailscale to establish a secure VPN connection.
- Enabled **Remote Desktop** on the Windows VM.

### 6. **Remote Access Configuration**
- Installed **Microsoft Remote Desktop** on the MacBook.
- Connected to the Windows VM using its **Tailscale IP address**.
- Verified stable remote access from any network.

### 7. **Performance Optimization**
- Adjusted VM CPU allocation to **4 cores** to balance Proxmox host performance.
- Set CPU type to **host** for optimized performance.
- Enabled **Writeback Cache** for the virtual disk.
- Disabled unnecessary Windows startup apps and visual effects.
- Synced system time between Proxmox and the Windows VM.

---

## Final Result
- Fully functional **Windows 10 VM** on Proxmox.
- **Secure remote access** via Microsoft Remote Desktop on the MacBook.
- Optimized performance with proper CPU/RAM allocation and driver support.

---

## Future Improvements
- Set up automatic backups for the VM.
- Deploy additional VMs for other services.
- Implement firewall rules for enhanced security.
