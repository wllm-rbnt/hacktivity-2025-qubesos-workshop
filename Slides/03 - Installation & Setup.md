
## Hardware

- Hardware recommendation
	+ https://doc.qubes-os.org/en/latest/user/hardware/system-requirements.html
		+ Recent Intel 64 Bit CPU with VT-d & VT-x extensions
			+ VT-x: virtualization extensions (**vmx** CPU flag on Linux, see ```lscpu```command)
			+ VT-d: I/O MMU virtualization (PCI passthrough)
		+ *Notes*: AMD not recommended because of their microcode update distribution policy
		+ Minimum 16GB RAM
		+ Minimum 128GB HDD with SSD
		+ Intel Graphic adapter
		+ A non-USB keyboard (as in most laptops) or multiple USB controllers
		+ TPM with good BIOS support
+ Hardware Compatibility List
	- https://www.qubes-os.org/hcl/
+ Certified Hardware
	- https://doc.qubes-os.org/en/latest/user/hardware/certified-hardware/certified-hardware.html
- Qubes OS can run as a VM (nested virtualization)
- Personal experience on laptops only
	- Lenovo X260 (16GB RAM)
	- Lenovo T14 Gen 4 (32GB RAM)

## Source validation

- **Do not install Qubes on a computer you don’t trust**
- **Chain of trust** problem during installation media validation
- Ultimately, you make the **choice** to trust your setup
- https://doc.qubes-os.org/en/latest/user/downloading-installing-upgrading/install-security.html
- https://www.qubes-os.org/downloads/
- ![[Pasted image 20250929214501.png]]

- Retrieve **QMSK** (Qubes Master Signing Key)
```console
$ sudo apt install gnupg
$ gpg --keyserver-options no-self-sigs-only,no-import-clean --keyserver hkp://keyserver.ubuntu.com --recv-keys 0x427F11FD0FAA4B080123F01CDDFA1A3E36879494
```
- Check QMSK authenticity:
```
427F 11FD 0FAA 4B08 0123  F01C DDFA 1A3E 3687 9494
```
- Adjust trust level on QMSK
```console
$ gpg --edit-key 0x427F11FD0FAA4B080123F01CDDFA1A3E36879494
[...]
gpg> fpr
pub   4096R/36879494 2010-04-01 Qubes Master Signing Key
Primary key fingerprint: 427F 11FD 0FAA 4B08 0123  F01C DDFA 1A3E 3687 9494

gpg> trust
[...]
Please decide how far you trust this user to correctly verify other users' keys

   1 = I don't know or won't say
   2 = I do NOT trust
   3 = I trust marginally
   4 = I trust fully
   5 = I trust ultimately
   m = back to the main menu

Your decision? 5
Do you really want to set this key to ultimate trust? (y/N) y
[...]
gpg> q
```  
- Retrieve **RSK** (Release Signing Key)
```console
gpg2 --keyserver-options no-self-sigs-only,no-import-clean --fetch-keys https://keys.qubes-os.org/keys/qubes-release-4.2-signing-key.asc
```
- Check detached signature
```console
$ gpg -v --verify Qubes-R4.2.4-x86_64.iso.asc Qubes-R4.2.4-x86_64.iso
gpg: Signature made ma 17 feb 2025 05:58:47 CET  
gpg:                using RSA key 9C884DF3F81064A569A4A9FAE022E58F8E34D89F  
gpg: using pgp trust model  
gpg: checking the trustdb  
gpg: 1 key processed (0 validity counts cleared)  
gpg: marginals needed: 3  completes needed: 1  trust model: pgp  
gpg: depth: 0  valid:   1  signed:   1  trust: 0-, 0q, 0n, 0m, 0f, 1u  
gpg: depth: 1  valid:   1  signed:   0  trust: 1-, 0q, 0n, 0m, 0f, 0u  
gpg: Good signature from "Qubes OS Release 4.2 Signing Key" [full]  
gpg: binary signature, digest algorithm SHA256, key algorithm rsa4096
```
## Installation
Use ```shift + PrintScreen``` to take screenshots during setup (Anaconda Installer).
They'll be available **after installation**, on the newly installed machine, in ``/root/anaconda-screenshots```.
![[screenshot-0001.png]]
![[screenshot-0002.png]]
![[screenshot-0004.png]]
![[screenshot-0005.png]]
![[screenshot-0006.png]]
![[screenshot-0008.png]]
![[screenshot-0009.png]]
![[screenshot-0010.png]]
![[screenshot-0011.png]]
## After install
- TOR bootstrap, up to 300 seconds (if you installed Whonix)
- ... after you configured the network access
## Qubes OS system Upgrade

- **Backup** current setup
	- Use backup facility for Qubes (encrypted .tar.gz)
	- Manually export configuration changes made on dom0
		- Custom shortcuts, custom startup launcher, ...
- **Install new** Qubes OS version
	- Restore Qubes from backup
	- Re-do dom0 manual configuration
