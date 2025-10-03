# History
- Blue Pill presented at Blackhat in 2006 by Joanna Rutkowska
![[Pasted image 20250929223554.png]]
- Project started in 2010 by Joanna Rutkowska & Rafal Wojtczuk
- The initial release of Qubes 1.0 was completed by September 3, 2012
---
# Principles
- "security by compartmentalization/isolation"
	- allows users to compartmentalize their digital life into isolated environments, which is the core security principle of Qubes OS
- Qualified as "Reasonably secure OS"
- Template, "stateless desktop"
- Built around the Xen hypervisor, we'll come back to this later
---
# Security features
- https://doc.qubes-os.org/en/latest/introduction/intro.html
- Security by isolation (security-by-compartmentalization)
	- Different security domains as different VMs
	- With seamless GUI integration
- Stateless environments with the help of template system
- Secure updates
	- Updates to the dom0 operating system and the included Template OS images are performed via a special mechanism which does not require dom0 operating system to connect directly to a network.
- Secure clipboard
- Secure copy between domains
- Pre-defined functionnal domains (sys-net, sys-usb, sys-gpg, ...)
- Documentation: https://doc.qubes-os.org
![[qubes-trust-level-architecture.png]]
- `qubes-gui`(running in AppVM) and `qubes-guid` (running on GuiVM, dom0 by default) processes
- no network access for dom0
	- same goes for TemplateVMs, Vault VM, sys-usb VM
---
-  General organization depends on you
    - [https://doc.qubes-os.org/en/latest/user/how-to-guides/how-to-organize-your-qubes.html](https://doc.qubes-os.org/en/latest/user/how-to-guides/how-to-organize-your-qubes.html)
- There is a of room for human error
## Some fresh news
- QubesOS summit 2025 - Berlin - last week
    - Day #1 [https://www.youtube.com/watch?v=HwisqKFEQ0g](https://www.youtube.com/watch?v=HwisqKFEQ0g)
    - Day #2 [https://www.youtube.com/watch?v=F9eRaa1w4KM](https://www.youtube.com/watch?v=F9eRaa1w4KM)