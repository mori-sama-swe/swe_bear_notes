Package Management
#sre/linux

Linux package management systems handle the installation, updating, configuration, and removal of software on a Linux system. There are several package managers, each associated with different Linux distributions.

### Package Managers By Distribution Family
#### Debian-based Systems
* **APT (Advanced Package Tool)** – Used in Debian, Ubuntu, and related distributions.
  * Uses .deb packages.
Common commands:
```bash
sudo apt update   # Update package lists
sudo apt upgrade  # Upgrade installed packages
sudo apt install <package-name>  # Install a package
sudo apt remove <package-name>  # Remove a package
```

#### Red Hat-based Systems
* **DNF (Dandified Yum)** – Used in Fedora, RHEL (Red Hat Enterprise Linux), and CentOS 8+.
  * Uses .rpm packages.
  * Common commands:
```bash
sudo dnf install <package-name>
sudo dnf remove <package-name>
sudo dnf update
```

- **RPM (Red Hat Package Manager)** – A lower-level tool similar to dpkg but for .rpm files.
```bash
sudo rpm -i <package.rpm>  # Install
sudo rpm -e <package-name>  # Remove
```
