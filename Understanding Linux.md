Understanding Linux
#sre/linux

Contents:
1. Intro to Linux
2. Basic CLI Commands
3. Understanding files in Linux
4. Filters & Redirection
5. Users & Groups
6. Sudo
7. Software Management
8. Services & Processes
9. Good To Know Commands
10. Server Management
---
#### Linux Principles
- everything is a file (including hardware)
- small single purpose programs
- avoid captive user interface
- ability to chain programs together for complex operations
- Configuration data stored in text file

---
#### Linux Architecture

applications/programs -> shell -> kernel -> hardware

Linux distributions are categorized based on their **package management system**. The two most common types are:

1. **Debian-Based (DEB) Distributions**
```
Debian (the original)
Ubuntu (most popular)
Linux Mint
Kali Linux
MX Linux


🔸 Advantages: ✔ More Stable & Reliable – Debian is known for rock-solid stability. ✔ Large Community Support – Especially with Ubuntu-based systems. ✔ Better Dependency Management – APT resolves dependencies efficiently.

🔸 Disadvantages: ❌ Slower to Adopt New Packages – Prioritizes stability over the latest software. ❌ Less Control for Power Users – Ubuntu, for example, automates many processes.

```

2. **RPM-Based (Red Hat Package Manager) Distributions**
```
Red Hat Enterprise Linux (RHEL)
Fedora
CentOS (Now Replaced by CentOS Stream)
Rocky Linux & AlmaLinux (RHEL alternatives)
openSUSE

🔸 Advantages: ✔ More Cutting-Edge – Fedora, for example, includes newer software than Debian-based systems. ✔ Strong Security – Red Hat focuses on security patches and enterprise support. ✔ Enterprise-Grade Stability – RHEL-based systems are widely used in production environments.

🔸 Disadvantages: ❌ More Complex Dependency Handling – RPM can sometimes struggle with package dependencies. ❌ Less Community Support (Compared to Ubuntu/Debian) – Primarily used in enterprise environments.

```

Difference: is the packaging management system 
![](Understanding%20Linux/Screenshot%202025-02-01%20at%209.53.32%E2%80%AFPM.png)

If you **want stability & easy use** → **Debian-Based (Ubuntu, Mint, Debian).**
If you **need enterprise support & latest tech** → **RPM-Based (RHEL, Fedora, Rocky Linux).**
