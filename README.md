# HomeLab
My home lab environment - SonicWall NSv firewall + Alma Linux server + AD server 2022

# SonicWall NSv — Installation & Setup Guide

> *Note: IP addresses in this guide use lab addressing for transparency. The topology and configurations shown are real.*

## The VM layer

I chose **Windows 11 + Hyper-V** as my host because it's what I already had — no extra software, no Proxmox, no ESXi license needed. The NSv runs as a VM on the internal virtual switch, with Windows Server 2022 (AD) and AlmaLinux on separate LAN segments behind it.

## The struggle to deploy NSv

I'll be honest: getting NSv running was harder than the actual configuration. Here's the journey:

### Attempt 1 — VMware Workstation Pro

First I tried the obvious path: download the latest NSv OVA, import into Workstation Pro. **Failed immediately** with:

> `Couldn't load the image`

Turns out the latest NSv images ship with certificates that Workstation Pro rejects during OVA import. I searched multiple forums and repos — several people had the same issue. The consensus: the OVA *format* is broken on older VMware versions, not the VM itself.

### Attempt 2 — Hyper-V (raw)

Switched to Hyper-V, imported the same OVA. **Failed again.** This time, the issue wasn't the image or certificates — I just hadn't configured the Hyper-V environment correctly. The VM would fail to boot.

### Attempt 3 — Hyper-V (with preparation)

After more digging, I found the real fix. The NSv image works fine on Hyper-V **if you prepare the environment correctly first**. The key steps I was missing:

1. **Disable Secure Boot** on the NSv VM — SonicWall's EFI bootloader isn't signed for Hyper-V's secure boot chain
2. **Use Generation 1** (not Generation 2) VM — NSv expects BIOS, not UEFI
3. **Import the OVA as a .vhd** — convert from OVA first, then attach to Hyper-V (or use the .ovf/ovf export path)
4. **Enable MAC address spoofing** on the virtual switch — NSv needs to respond to ARP for its management interface

Once I had these steps right, the latest NSv version booted cleanly and I could access the SonicOS web interface.

## What I learned

- **NSv is finicky about its deployment path**, more than about configuration
- The certificates aren't "broken" — they just don't match the extensions what consumer hypervisors expect, on some OVA versions for VMware Workstation PRO.
- Hyper-V works, but it's **not plug-and-play** like VMware usually is
- The actual firewall setup (interfaces, zones, policies) was straightforward once I had the VM running

---

*Next: [AlmaLinux AD Server Setup](link-to-next-post)*
