![[Pasted image 20250929224637.png]]
Homepage: https://xenproject.org/

- Hypervisor **types 1 & 2** https://en.wikipedia.org/wiki/Hypervisor
	- **KVM**, **bhyve** (kernel modules) transform OS in **type 1 HV**
	- **Xen**, **Hyper-V** or **VMWare ESX** are **type 1 HV**
	- **Virtualbox** or **VMWare Workstation** are **type 2 HV**
	- Depends on the integration level with the underlying OS

- **Domains** aka **VMs** of different types
	- **Dom0** (Privileged domain) has the capability to access the hardware directly, handles all access to the system’s I/O functions and interacts with the other Virtual Machines
	- **DomU** (Unprivileged Domains) - Guest VMs are totally isolated from the hardware: in other words, they have no privilege to access hardware or I/O functionality

- Virtualization methods
	Reference: https://wiki.xenproject.org/wiki/Understanding_the_Virtualization_Spectrum
	- **PV** (ParaVirtualization):
		- does not require virtualization extensions from the host CPU
		- guests require a PV-enabled kernel and PV drivers
		- guests are aware of the hypervisor
		- PV-enabled kernels exist for Linux, NetBSD and FreeBSD
	- **HVM** (Hardware-assisted VM)
		- uses virtualization extensions (Intel VT or AMD-V) from the host CPU to virtualize guests
		- uses QEMU to emulate PC hardware, including BIOS, IDE disk controller, VGA graphic adapter, USB controller, network adapter etc.
		- guests do not require any kernel support
		- Windows operating systems can be used as a Xen Project HVM guest
	- **PVH**
		- hybrid mode where the VM uses hardware virtualization extensions for CPU and memory management (like HVM) but uses PV drivers for I/O, so it avoids emulation of devices. It combines the best of both worlds, fast CPU virtualization from HVM with efficient I/O from PV

Management tools
- **Xen** default **toolstack**, the```xl```command in dom0 (previously ```xm```)
	(also available in **Qubes OS**)
- Alternatives are libvirt/virtsh, xcp-ng, ...

I/O virtualization
- The **PV split driver model**: in this model, a virtual front-end device driver talks to a virtual back-end device driver which in turn talks to the physical device via the (native) device driver
- **Device Emulation Based I/O**: HVM guests emulate hardware devices in software. In Xen, QEMU is used as Device Emulator
- **Passthrough**: allows you to give control of physical devices to guests

Networking
- **PV split driver** frontend/backend
- Seen as virtual interface **vif** + **bridge** in dom0, **native** interface in domU
