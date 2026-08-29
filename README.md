*This project has been created as part of the 42 curriculum by lbalderr.*

# Born2beRoot

## Description
Born2beRoot is a system administration project that introduces the fundamentals of virtualization, system configuration and strict security policies. The primary goal is to create a secure virtual machine operating under specific constraints. This project serves as an introduction to the role of a system administrator, requiring the setup of an encrypted file system, strict password and sudo policies, firewall and ssh rules, and automated system monitoring via a bash script.

## Architecture and Design Choices
During the setup of this secure environment, several critical design and architectural choices were made to adhere to the project constraints and best practices:

*   **Operating System:** Debian 13 (Trixie) was chosen over Rocky Linux. Debian is renowned for its stability, extensive package repository and the user-friendly `apt` package manager. While Rocky Linux provides an excellent enterprise-grade environment (being bug-for-bug compatible with Red Hat Enterprise Linux), Debian's widespread community support and lighter default footprint make it ideal for a strictly controlled, minimalist server environment.
*   **Partitioning:** Logical Volume Management (LVM) was implemented over an encrypted partition. This allows for flexible volume resizing in the future while ensuring that all data remains secure. 
*   **Security & User Management:** The system enforces a strong password policy (expiration, complexity and history checks) using `libpam-pwquality`. Root login is disabled via SSH, forcing users to connect through standard accounts and elevate privileges using `sudo`. The `sudo` environment itself is locked down with limited retry attempts, required TTY (terminal interface) and persistent logging of all executed commands.
*   **Services:** The SSH daemon is configured to listen on a non-standard port (4242) rather than the default port 22, adding a basic layer of security against automated bot scans.

## Technical Comparisons
*   **Debian vs Rocky Linux:** Debian uses the `apt`/`dpkg` package management system and follows a community-driven release cycle prioritizing stability. Rocky Linux utilizes `dnf`/`rpm` and is built as an enterprise-focused operating system directly mapping to Red Hat Enterprise Linux (RHEL).
*   **AppArmor vs SELinux:** AppArmor (the default on Debian) is a Mandatory Access Control (MAC) system that secures applications by binding access control attributes to programs via file paths. SELinux (default on Rocky Linux) is significantly more granular and complex, labeling inodes (files) and processes directly. AppArmor is generally easier to configure and maintain for a basic server setup.
*   **UFW vs firewalld:** Uncomplicated Firewall (UFW) is a user-friendly frontend for `iptables`, making it extremely simple to allow or deny specific ports, which is perfect for this Debian setup. `firewalld` is the standard on RHEL-based systems and uses a zone-based approach to manage trust levels for different network connections.
*   **VirtualBox vs UTM:** VirtualBox is a cross-platform type-2 hypervisor that natively supports x86/x64 architectures. UTM is heavily optimized for Apple platforms and utilizes QEMU to emulate different architectures (such as running x86 operating systems on Apple Silicon ARM chips). This project was implemented using VirtualBox to ensure standard compatibility with the provided Debian ISO.

## Instructions
To evaluate or run this project:
1. Verify current signature matches the content of signature.txt

```bash
cd /home/lbalderr/sgoinfre/lbalderr_vm/Born2beRoot
diff -s /path_to_this_repo/signature.txt <(sha1sum Born2beRoot.vdi)
```

2. Open Oracle VM VirtualBox.
3. Right-click the existing VM in VirtualBox, select Clone and choose Full Clone to create a completely detached copy of the disk.
4. Start the cloned virtual machine. It will boot into a `multi-user.target` text interface (no GUI).
5. Follow the evaluation rule and ask me anything if you need help.

To connect via ssh:

```bash
ssh -p 9999 username@localhost
```

## Resources
*   [Debian Administrator's Handbook](https://debian-handbook.info/)
*   [UFW - Ubuntu Community Help Wiki](https://help.ubuntu.com/community/UFW)
*   [Sudo Manual](https://www.sudo.ws/docs/man/sudoers.man/)
*   [Bash Scripting Tutorial](https://linuxconfig.org/bash-scripting-tutorial-for-beginners)

## AI Usage
Large Language Models (Google Gemini) were used as an interactive tutor and debugging assistant throughout this project. 
No commands or scripts were blindly copied, AI was used strictly to explain concepts and troubleshoot environmental specificities.
