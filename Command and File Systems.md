Command and File Systems
#sre/linux

# 📂 File and Directory Management
| **Command** | **Example** | **Description** |
|:-:|:-:|:-:|
| ls | ls -lh | List files in human-readable format |
| cd | cd /home/user/Documents | Change to the "Documents" directory |
| pwd | pwd | Show current working directory |
| mkdir | mkdir new_folder | Create a new directory |
| rmdir | rmdir empty_folder | Remove an empty directory |
| rm -r | rm -r my_folder | Remove a directory and its contents |
| touch | touch newfile.txt | Create a new empty file |
| cp | cp file1.txt file2.txt | Copy a file |
| mv | mv oldname.txt newname.txt | Rename or move a file |
| rm | rm file.txt | Remove a file |
| find | find /home -name "myfile.txt" | Search for a file by name |
| locate | locate myfile.txt | Quickly find a file by name |
| tree | tree /home/user | Show directory structure |

# 📄 File Viewing & Editing
| **Command** | **Example** | **Description** |
|:-:|:-:|:-:|
| cat | cat file.txt | Display file contents |
| tac | tac file.txt | Display file contents in reverse order |
| less | less file.txt | View file content page by page |
| more | more file.txt | View file content (like less) |
| head | head -5 file.txt | Show first 5 lines of a file |
| tail | tail -5 file.txt | Show last 5 lines of a file |
| tail -f | tail -f log.txt | Monitor file changes in real-time |
| nano | nano file.txt | Open a file in Nano editor |
| vim | vim file.txt | Open a file in Vim editor |
| vi | vi file.txt | Open a file in Vi editor |

# 🛠 File Permissions & Ownership
| **Command** | **Example** | **Description** |
|:-:|:-:|:-:|
| ls -l | ls -l file.txt | Show file permissions |
| chmod | chmod 755 file.txt | Change file permissions |
| chown | chown user:group file.txt | Change file owner |
| chgrp | chgrp groupname file.txt | Change group ownership |
| umask | umask 022 | Set default permissions |
| stat | stat file.txt | Show detailed file information |

# 📜 File Compression & Archiving
| **Command** | **Example** | **Description** |
|:-:|:-:|:-:|
| tar | tar -cvf archive.tar file.txt | Create a tar archive |
| tar | tar -xvf archive.tar | Extract a tar archive |
| tar -czvf | tar -czvf archive.tar.gz my_folder/ | Create gzip-compressed archive |
| tar -xzvf | tar -xzvf archive.tar.gz | Extract gzip-compressed archive |
| zip | zip archive.zip file.txt | Compress file to ZIP |
| unzip | unzip archive.zip | Extract ZIP archive |
| gzip | gzip file.txt | Compress file using gzip |
| gunzip | gunzip file.txt.gz | Decompress gzip file |

# 🔎 File Searching & Finding
| **Command** | **Example** | **Description** |
|:-:|:-:|:-:|
| find | find /home -name "file.txt" | Find a file by name |
| find | find /home -type d -name "folder" | Find a directory by name |
| locate | locate myfile.txt | Find a file quickly |
| which | which ls | Find the path of a command |
| whereis | whereis ls | Find a command and documentation |
| grep | grep "error" logfile.txt | Search for "error" inside a file |
| grep -r | grep -r "error" /var/logs/ | Search recursively in a directory |
| awk | awk '{print $1}' file.txt | Extract first column from a file |
| sed | sed 's/old/new/g' file.txt | Replace text in a file |

# 🔄 File System & Disk Usage
| **Command** | **Example** | **Description** |
|:-:|:-:|:-:|
| df -h | df -h | Show disk space usage |
| du -sh | du -sh /home/user | Show size of a directory |
| du -h | du -h file.txt | Show file size |
| mount | mount /dev/sdb1 /mnt/usb | Mount a device |
| umount | umount /mnt/usb | Unmount a device |
| fsck | fsck /dev/sda1 | Check and repair file system |
| mkfs.ext4 | mkfs.ext4 /dev/sdb1 | Format partition with ext4 |

# ⚡ File Manipulation & Metadata
| **Command** | **Example** | **Description** |
|:-:|:-:|:-:|
| stat | stat file.txt | Get detailed file info |
| touch | touch file.txt | Create or update timestamp of file |
| diff | diff file1.txt file2.txt | Compare two files line by line |
| cmp | cmp file1.txt file2.txt | Compare two files byte by byte |
| sort | sort file.txt | Sort file contents alphabetically |
| uniq | uniq file.txt | Remove duplicate lines from file |
| wc -l | wc -l file.txt | Count number of lines in a file |
| wc -w | wc -w file.txt | Count number of words in a file |
| tee | `echo "Hello" | tee output.txt` |
| cut | cut -d':' -f1 file.txt | Extract first column from a file |
---
# 📂 Important Directories in Linux
| **Directory** | **Description** |
|:-:|:-:|
| / **(Root)** | The top-level directory that contains all other directories. Everything in Linux starts from here. |
| /bin | Contains essential user binaries (executables), like ls, cp, mv, cat, etc. |
| /sbin | Contains system binaries used by the root user, like fsck, reboot, ifconfig. |
| /boot | Contains boot loader files (e.g., grub), kernel images (vmlinuz), and initramfs. |
| /dev | Contains device files, such as sda (hard disk), tty (terminals), null, random. |
| /etc | System-wide configuration files (passwd, shadow, hosts, resolv.conf, etc.). |
| /home | Contains user home directories (/home/user for each user). |
| /lib | Shared libraries required for system programs and the kernel. |
| /lib64 | Stores 64-bit shared libraries (used on 64-bit systems). |
| /media | Mount point for removable media like USB drives, CDs (/media/cdrom). |
| /mnt | Temporary mount point for manually mounted filesystems. |
| /opt | Used for third-party software installations (e.g., Google Chrome, Zoom). |
| /proc | Virtual filesystem that provides system and process information (/proc/cpuinfo, /proc/meminfo). |
| /root | Home directory of the root (admin) user (/home/root is NOT used). |
| /run | Stores system and process runtime data (temporary files since the last boot). |
| /srv | Contains service-related data (e.g., website files for a web server). |
| /sys | Provides kernel-related information similar to /proc (device details). |
| /tmp | Temporary directory for storing files that are deleted on reboot. |
| /usr | Contains user binaries (/usr/bin), libraries (/usr/lib), and documentation (/usr/share). |
| /usr/local | Stores software installed manually instead of using package managers. |
| /var | Stores variable data like logs (/var/log), mail (/var/mail), and cache (/var/cache). |
