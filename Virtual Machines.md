Virtual Machines
#sre/virtualmachine

Virtualization: [DevOps](https://www.visualpath.in/devopstutorials/devops)

life before virtual machines -> basically for any instance of an app - we had to dedicate individual servers or physical machines to make all 3 run in parallel -> vm comes in and now requires only one host-machine, that can run multiple virtual machines within in

**~virtual machine:~** is a software-based emulation of a physical computer, it runs an operating machine (OS) and applications just like a physical machine. but is hosted on a physical machine (called the **host machine**)  using a virtualization software

- allows host-machine to run multiple operating systems 

key components of a virtual machine:
1. **host-machine**: the physical computer that provides resources (cpu,memory, and storage)
2. **guest-machine/vm**: the virtualized system running inside the host
3. **snapshot:** a snapshot of the virtual machine which can be backed-up
4. **hypervisor**: enables virtualization, there are two types:<!-- {"fold":true} -->
   - bare-metal: runs as a base (OS), VMWare esxi, XenHypervisor
   - runs as a software (learn and test), Oraclebox, VMware Server
---
benefits of virtual machines:
- **Isolation** – Each VM runs independently.
- **Resource Efficiency** – Multiple VMs can share physical hardware.
- **Portability** – VMs can be moved across systems easily.
- **Scalability** – Easy to create or remove VMs based on needs.
- **Testing & Development** – Great for running different OS environments on
---

**~what is virtualization:~** is the process of creating a virtual version of computing resources, such as hardward, storage, network, or an entire OS, instead of physical components

how virtualization works: at the core of virtualization is the **hypervisor** a software layer that allows multiple (vms) to run on a single machine
- type 1: (Bare Metal) -> runs directly on the hardware (VMWare ESXI)
- type 2: (Hosted) -> runs on top of an existing OS (VirtualBox, VMWare Station)

![](Virtual%20Machines/Screenshot%202025-02-01%20at%207.16.21%E2%80%AFPM.png)

![](Virtual%20Machines/Screenshot%202025-02-01%20at%207.17.21%E2%80%AFPM.png)
![](Virtual%20Machines/Screenshot%202025-02-01%20at%207.17.44%E2%80%AFPM.png)
---
#### Types of Virtualization:

**Server Virtualization** – Running multiple virtual servers on a single physical machine (e.g., using VMware, Hyper-V, or KVM).

**Desktop Virtualization** – Running multiple virtual desktops on a server, enabling remote access (e.g., VDI - Virtual Desktop Infrastructure).

**Application Virtualization** – Running applications in isolated environments without installation on the OS (e.g., Citrix Virtual Apps).

**Network Virtualization** – Creating virtual network devices (routers, switches) for flexible networking (e.g., VLANs, SDN).

**Storage Virtualization** – Pooling multiple storage devices into a single, virtual storage unit (e.g., SAN, NAS).

**Data Virtualization** – Combining data from multiple sources into a unified, virtual database for easy access.

---
#### 3 Types of Methods
rule of thumb: if you want to automate something. make sure you know how to do it manually.
1) Manual:
2) Automated: