Services and Processes
#sre/linux
### Services and Processes in Linux
Linux manages applications and system operations through **services** and **processes**. While both are essential for the system's functioning, they have distinct characteristics and use cases

Understanding **services** and **processes** is crucial for Linux system administration. Services are background daemons managed by systemctl, while processes are individual program executions managed with ps, top, and kill.


Difference Between Services and Processes
| **Feature** | **Service** | **Process** |
|:-:|:-:|:-:|
| Runs in Background | Yes | Yes |
| Typically Starts at Boot | Yes | No |
| Managed by Systemd | Yes | No (Managed by kernel/user) |
| Can Be Interactive | No | Yes |
---

### Services in Linux
A **service** in Linux is a background process that runs continuously and usually starts at boot time. Services are often used for system functions like networking, logging, and user authentication.

##### Managing Services with Systemd
Most modern Linux distributions use **systemd** to manage services. The main command used is systemctl.
**Basic Service Management Commands**
| **Action** | **Command** |
|:-:|:-:|
| Check if a service is running | systemctl status <service> |
| Start a service | sudo systemctl start <service> |
| Stop a service | sudo systemctl stop <service> |
| Restart a service | sudo systemctl restart <service> |
| Enable service at boot | sudo systemctl enable <service> |
| Disable service from boot | sudo systemctl disable <service> |
| List all services | systemctl list-units --type=service |

**Example: Managing the SSH Service**
```bash
systemctl status ssh
sudo systemctl start ssh
sudo systemctl enable ssh
```

---
### Processes in Linux
A **process** is an instance of a running program. Linux allows users to monitor and manage processes using various tools.

#### Process Management Commands
| **Action** | **Command** |
|:-:|:-:|
| Show running processes | ps aux |
| Show a process tree | pstree |
| Monitor real-time processes | top or htop |
| Kill a process by PID | kill <PID> |
| Kill a process by name | pkill <process-name> |
| Kill all processes of a user | killall -u <username> |

Find the process ID (PID):
```bash
ps aux | grep apache
```

Kill the process:
```bash
sudo kill <PID>
```

Force kill if needed:
```bash
sudo kill -9 <PID>
```

---
