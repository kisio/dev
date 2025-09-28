
### **1. Introduction to Linux & Core Concepts**

Linux is a Unix-like, open-source operating system based on the Linux kernel. It's known for its stability, security, and flexibility.

*   **Kernel:** The core of the OS, managing system resources.
*   **Shell:** A command-line interpreter that allows users to interact with the kernel (e.g., Bash, Zsh).
*   **Distribution (Distro):** A complete OS package built around the Linux kernel, including a shell, utilities, and applications (e.g., Ubuntu, CentOS, Fedora).
*   **Everything is a File:** A fundamental Unix philosophy. Devices, processes, and network sockets are often represented as files in the filesystem.

---

### **2. The Linux Filesystem Hierarchy (FHS)**

Understanding the Linux filesystem structure is paramount. It's standardized to make it predictable across distributions.

**Table: Key Directories in the Linux Filesystem**

| Directory | Purpose                                                           | Examples of Contents                          |
| :-------- | :---------------------------------------------------------------- | :-------------------------------------------- |
| `/`       | **Root Directory:** The base of the entire filesystem.            | All other directories                         |
| `/bin`    | **Binaries:** Essential user command-line binaries.               | `ls`, `cp`, `mv`, `cat`, `bash`               |
| `/sbin`   | **System Binaries:** Essential system administration binaries (for root). | `fdisk`, `ifconfig`, `mount`, `reboot`        |
| `/etc`    | **Configuration Files:** System-wide configuration files.         | `/etc/passwd`, `/etc/fstab`, `/etc/ssh/sshd_config` |
| `/home`   | **User Home Directories:** Contains personal files for each user. | `/home/user1`, `/home/user2/documents`        |
| `/root`   | **Root User's Home Directory:** Home for the superuser.           | `root`'s specific configuration and files     |
| `/var`    | **Variable Data:** Data that changes frequently (logs, spool files, temporary web files). | `/var/log`, `/var/www`, `/var/cache`          |
| `/tmp`    | **Temporary Files:** Files that are deleted between reboots or after a certain time. | Session files, temporary program data         |
| `/usr`    | **Unix System Resources:** Read-only user programs, libraries, documentation. | `/usr/bin`, `/usr/lib`, `/usr/share/doc`      |
| `/opt`    | **Optional Add-on Applications:** Third-party software packages.  | `/opt/google/chrome`, `/opt/splunk`           |
| `/dev`    | **Devices:** Device files (hardware interfaces).                 | `/dev/sda`, `/dev/null`, `/dev/random`        |
| `/proc`   | **Process Information:** Virtual filesystem providing process and kernel info. | `/proc/cpuinfo`, `/proc/meminfo`, `/proc/PID` |
| `/sys`    | **System Information:** Virtual filesystem providing kernel and device info. | `/sys/class/net`, `/sys/block`                |
| `/mnt`    | **Mount Point:** Temporary mount points for filesystems.        | Used for mounting USB drives, network shares  |
| `/media`  | **Mount Point:** Mount points for removable media (CD-ROMs, USBs). | `/media/usbdisk`                              |
| `/run`    | **Runtime Variable Data:** Data relevant since the last boot.     | PID files, UDS sockets                        |

---

### **3. Essential Command-Line Interface (CLI) Commands**

The CLI is your primary interface on a Linux server. Proficiency here is non-negotiable.

#### **3.1. Navigation & Information**

| Command  | Description                                                     | Examples                                 |
| :------- | :-------------------------------------------------------------- | :--------------------------------------- |
| `pwd`    | **Print Working Directory:** Shows your current location.       | `pwd`                                    |
| `ls`     | **List Directory Contents:** Shows files and directories.       | `ls -l` (long format), `ls -a` (all files including hidden) |
| `cd`     | **Change Directory:** Navigate the filesystem.                  | `cd /etc`, `cd ..` (parent dir), `cd ~` (home dir) |
| `file`   | **Determine File Type:** Identifies the type of a file.         | `file /bin/bash`, `file image.jpg`       |
| `man`    | **Manual Pages:** Access documentation for commands.          | `man ls`, `man man`                      |
| `whatis` | **Short Description:** Provides a one-line summary of a command. | `whatis ls`                              |
| `which`  | **Locate Command:** Shows the full path to an executable.       | `which bash`, `which sudo`               |
| `history`| **Command History:** Displays previously executed commands.     | `history`, `!25` (rerun command #25)     |

#### **3.2. File & Directory Management**

| Command  | Description                                                     | Examples                                     |
| :------- | :-------------------------------------------------------------- | :------------------------------------------- |
| `mkdir`  | **Make Directory:** Creates new directories.                    | `mkdir newdir`, `mkdir -p /path/to/nested/dir` |
| `rmdir`  | **Remove Directory:** Deletes empty directories.                 | `rmdir olddir`                               |
| `rm`     | **Remove:** Deletes files or directories (be careful!).         | `rm file.txt`, `rm -r directory/` (recursive), `rm -rf sensitive/` (force recursive) |
| `cp`     | **Copy:** Copies files or directories.                          | `cp file.txt newfile.txt`, `cp -r dir/ newdir/` |
| `mv`     | **Move / Rename:** Moves or renames files/directories.          | `mv oldname.txt newname.txt`, `mv file.txt /new/location/` |
| `touch`  | **Create Empty File / Update Timestamp:** Creates a new empty file or updates access/modification times. | `touch newfile.txt`, `touch -a file.txt`     |
| `find`   | **Find Files:** Searches for files based on various criteria.   | `find . -name "*.log"`, `find / -type d -name "config"` |
| `locate` | **Find Files (Database):** Searches a pre-built database (faster but less real-time). | `locate sshd_config`                         |

#### **3.3. File Content Manipulation & Viewing**

| Command  | Description                                                     | Examples                                         |
| :------- | :-------------------------------------------------------------- | :----------------------------------------------- |
| `cat`    | **Concatenate & Display:** Shows entire file content.           | `cat file.txt`, `cat file1.txt file2.txt > combined.txt` |
| `less`   | **View File (Pager):** Views files page by page (can scroll back). | `less large_log.log`                             |
| `more`   | **View File (Pager):** Views files page by page (can't scroll back as easily). | `more another_log.log`                           |
| `head`   | **Display Top Lines:** Shows the beginning of a file.           | `head -n 10 file.txt` (first 10 lines)           |
| `tail`   | **Display Bottom Lines:** Shows the end of a file.              | `tail -n 5 file.txt` (last 5 lines), `tail -f /var/log/syslog` (follow log in real-time) |
| `grep`   | **Search Pattern:** Searches for text patterns in files.        | `grep "error" /var/log/messages`, `ls -l | grep "Aug"` |
| `sed`    | **Stream Editor:** Powerful text manipulation (find, replace, delete). | `sed 's/old/new/g' file.txt` (replace all 'old' with 'new') |
| `awk`    | **Pattern Scanning & Processing:** More powerful text processing, often column-based. | `awk '{print $1}' file.txt` (print first column) |
| `sort`   | **Sort Lines:** Sorts lines of text files.                      | `sort names.txt`, `sort -r names.txt` (reverse)  |
| `uniq`   | **Report/Filter Duplicate Lines:** Filters out or reports duplicate lines. | `sort file.txt | uniq -c` (count unique lines)   |
| `wc`     | **Word Count:** Counts lines, words, and characters.            | `wc -l file.txt` (line count)                    |
| `diff`   | **Compare Files:** Shows differences between two files.         | `diff file1.txt file2.txt`                       |

#### **3.4. Input/Output Redirection & Pipes**

These are essential for chaining commands and managing data flow.

*   **`>` (Redirect Output):** Sends command output to a file, overwriting it.
    *   `ls -l > file_list.txt`
*   **`>>` (Append Output):** Appends command output to a file.
    *   `echo "New line" >> file_list.txt`
*   **`<` (Redirect Input):** Uses a file as input for a command.
    *   `sort < unsorted.txt`
*   **`|` (Pipe):** Sends the output of one command as the input to another. This is incredibly powerful.
    *   `ls -l /var/log | grep ".log"` (list logs, then filter for .log files)
    *   `cat access.log | grep "404" | wc -l` (count 404 errors in an access log)

#### **3.5. Text Editors**

You'll spend a lot of time in text editors.

*   **Nano:** User-friendly, simpler, easier for beginners.
    *   `nano filename.txt`
    *   `Ctrl+X` to exit, `Y` to save.
*   **Vi/Vim:** Powerful, modal editor, steeper learning curve but highly efficient once mastered.
    *   `vim filename.txt`
    *   **Modes:**
        *   **Normal Mode (Command Mode):** For navigation, deleting, copying. (Press `Esc` to enter)
        *   **Insert Mode:** For typing text. (Press `i`, `a`, `o` to enter)
        *   **Visual Mode:** For selecting text. (Press `v` to enter)
        *   **Command-Line Mode (Ex Mode):** For saving, quitting, search/replace. (Press `:` to enter)
    *   **Common Vim Commands:**
        *   `i` - insert before cursor
        *   `a` - append after cursor
        *   `o` - open new line below
        *   `dd` - delete line
        *   `yy` - yank (copy) line
        *   `p` - paste
        *   `/pattern` - search for pattern
        *   `:w` - write (save)
        *   `:q` - quit
        *   `:wq` - write and quit
        *   `:q!` - quit without saving
        *   `:s/old/new/g` - substitute 'old' with 'new' globally on current line
        *   `:%s/old/new/g` - substitute 'old' with 'new' globally in the file

---

### **4. User & Group Management**

Security and access control are fundamental in Linux.

#### **4.1. Users**

| Command   | Description                                                     | Examples                                     |
| :-------- | :-------------------------------------------------------------- | :------------------------------------------- |
| `adduser` | **Add User:** Creates a new user with home directory and default settings. | `sudo adduser newuser`                       |
| `useradd` | **Add User (Low-level):** More granular control, no interactive prompts. | `sudo useradd -m -s /bin/bash newuser`       |
| `passwd`  | **Change Password:** Sets or changes a user's password.         | `passwd newuser`                             |
| `usermod` | **Modify User:** Changes user properties (home dir, shell, groups). | `sudo usermod -aG sudo newuser` (add to sudo group) |
| `deluser` | **Delete User:** Removes a user.                                | `sudo deluser --remove-home olduser`         |
| `id`      | **Display User/Group IDs:** Shows current user's UID, GID, and groups. | `id`, `id username`                          |
| `whoami`  | **Current User:** Displays the current effective username.      | `whoami`                                     |
| `su`      | **Switch User:** Change to another user (or root).             | `su - otheruser`                             |
| `sudo`    | **Execute as Superuser:** Runs a single command with root privileges. | `sudo apt update`, `sudo vi /etc/hosts`      |

#### **4.2. Groups**

| Command   | Description                                                     | Examples                                     |
| :-------- | :-------------------------------------------------------------- | :------------------------------------------- |
| `addgroup`| **Add Group:** Creates a new group.                             | `sudo addgroup developers`                   |
| `groupadd`| **Add Group (Low-level):** Creates a new group.                 | `sudo groupadd testers`                      |
| `groupmod`| **Modify Group:** Changes group properties.                     | `sudo groupmod -n newname oldname`           |
| `delgroup`| **Delete Group:** Removes a group.                              | `sudo delgroup oldgroup`                     |
| `groups`  | **Display Groups:** Shows groups a user belongs to.             | `groups`, `groups username`                  |
| `gpasswd` | **Administer Group Files:** Manage group members.               | `sudo gpasswd -a user groupname` (add user to group) |

#### **4.3. Files: Key Configuration Files**

*   `/etc/passwd`: Stores user account information (username, UID, GID, home directory, shell). Passwords are not here.
*   `/etc/shadow`: Stores encrypted user passwords and password expiration information (readable only by root).
*   `/etc/group`: Stores group account information (group name, GID, members).
*   `/etc/sudoers`: Defines which users or groups can run `sudo` commands and with what permissions (`sudo visudo` to edit safely).

---

### **5. File Permissions**

This is a critical security concept. Every file and directory has permissions that determine who can read, write, or execute it.

#### **5.1. Permission Types**

*   **Read (`r`):**
    *   **Files:** Can view file content.
    *   **Directories:** Can list contents (but not access details without `x`).
*   **Write (`w`):**
    *   **Files:** Can modify or delete file content.
    *   **Directories:** Can create, delete, or rename files within the directory (regardless of file permissions).
*   **Execute (`x`):**
    *   **Files:** Can run the file as a program/script.
    *   **Directories:** Can enter the directory and access its files.

#### **5.2. Permission Categories**

Permissions are defined for three categories:

1.  **Owner (`u`):** The user who owns the file/directory.
2.  **Group (`g`):** The group associated with the file/directory.
3.  **Others (`o`):** Everyone else on the system.
4.  **All (`a`):** Refers to all three (user, group, others).

#### **5.3. Viewing Permissions**

Use `ls -l` to see permissions:

```
-rw-r--r-- 1 user group 1024 Jan 1 10:00 filename.txt
drwxr-xr-x 2 user group 4096 Jan 1 10:00 dirname/
```

*   **First Character:**
    *   `-`: Regular file
    *   `d`: Directory
    *   `l`: Symbolic link
*   **Next 9 characters (3 sets of `rwx`):**
    *   Set 1: Owner permissions
    *   Set 2: Group permissions
    *   Set 3: Others permissions

#### **5.4. Changing Permissions (`chmod`)**

`chmod` changes file permissions using either symbolic (rwx) or octal (numeric) modes.

**Symbolic Mode:**

*   **`u`**, **`g`**, **`o`**, **`a`** (user, group, others, all)
*   **`+`** (add permission), **`-`** (remove permission), **`=`** (set exactly)
*   **`r`**, **`w`**, **`x`** (read, write, execute)

| Command                           | Description                            |
| :-------------------------------- | :------------------------------------- |
| `chmod u+x script.sh`             | Add execute permission for the owner.    |
| `chmod g-w file.txt`              | Remove write permission for the group.   |
| `chmod o=r file.txt`              | Set 'others' to read-only.             |
| `chmod a+rwx myfile`              | Give all users full permissions (rarely good practice). |
| `chmod +x script.sh`              | Add execute for all (user, group, others). |

**Octal (Numeric) Mode:**

Each permission (`r`, `w`, `x`) has a numeric value:

*   `r` = 4
*   `w` = 2
*   `x` = 1
*   `-` = 0

Sum the values for each category (owner, group, others).

| Permission Set | Numeric Value |
| :------------- | :------------ |
| `rwx`          | 4+2+1 = 7     |
| `rw-`          | 4+2+0 = 6     |
| `r-x`          | 4+0+1 = 5     |
| `r--`          | 4+0+0 = 4     |
| `--x`          | 0+0+1 = 1     |
| `---`          | 0+0+0 = 0     |

**Common Octal Permissions:**

| Octal | Symbolic | Description                                              |
| :---- | :------- | :------------------------------------------------------- |
| `777` | `rwxrwxrwx` | All permissions for everyone (DANGEROUS).                  |
| `755` | `rwxr-xr-x` | Owner has full, group/others can read/execute (common for scripts/directories). |
| `644` | `rw-r--r--` | Owner can read/write, group/others can only read (common for files). |
| `700` | `rwx------` | Owner has full, no one else has any.                   |
| `600` | `rw-------` | Owner can read/write, no one else has any.             |

*   `chmod 755 script.sh`
*   `chmod 644 document.txt`

#### **5.5. Changing Ownership (`chown`, `chgrp`)**

*   `chown`: Change owner and/or group.
    *   `sudo chown newuser file.txt`
    *   `sudo chown newuser:newgroup file.txt`
    *   `sudo chown -R newuser:newgroup directory/` (recursive)
*   `chgrp`: Change group only.
    *   `sudo chgrp newgroup file.txt`

#### **5.6. Special Permissions (Advanced)**

*   **SetUID (SUID):** On an executable file, allows the user to execute it with the permissions of the file owner. Appears as `s` in owner's execute bit (`rws`). Used for `passwd`, `sudo`.
    *   `chmod u+s executable` or `chmod 4755 executable`
*   **SetGID (SGID):**
    *   On an executable file: Runs with the permissions of the file's group (`rws` in group's execute bit).
    *   On a directory: New files/directories created within it inherit the parent directory's group, not the creator's primary group. (`rws` in group's execute bit).
    *   `chmod g+s directory` or `chmod 2775 directory`
*   **Sticky Bit:** Only applies to directories. Prevents users from deleting or renaming files in a directory unless they own the file or the directory. Appears as `t` in others' execute bit (`rwt`). Used in `/tmp`.
    *   `chmod +t /shared/tmp` or `chmod 1777 /shared/tmp`

---

### **6. Process Management**

Processes are running programs. Managing them is crucial for server health and troubleshooting.

#### **6.1. Viewing Processes**

| Command   | Description                                                     | Examples                                     |
| :-------- | :-------------------------------------------------------------- | :------------------------------------------- |
| `ps`      | **Process Status:** Displays a snapshot of current processes.   | `ps aux` (all processes, user, CPU, memory), `ps -ef` (full format) |
| `top`     | **Task Manager:** Real-time, interactive display of processes, CPU, memory usage. | `top`, press `q` to quit                     |
| `htop`    | **Interactive Process Viewer:** Enhanced version of `top` (often needs installation). | `htop`, use F-keys for options               |
| `pgrep`   | **Process by Name:** Finds process IDs (PIDs) by name.         | `pgrep sshd`                                 |
| `pstree`  | **Process Tree:** Displays processes in a tree structure showing parent-child relationships. | `pstree -p` (show PIDs)                      |

#### **6.2. Controlling Processes**

| Command   | Description                                                     | Examples                                     |
| :-------- | :-------------------------------------------------------------- | :------------------------------------------- |
| `kill`    | **Send Signal to Process:** Sends a signal to a process by PID. | `kill 12345` (sends SIGTERM - graceful stop), `kill -9 12345` (sends SIGKILL - forceful stop) |
| `killall` | **Kill by Name:** Kills all processes with a given name.        | `killall firefox`                            |
| `pkill`   | **Kill by Pattern:** Kills processes matching a pattern (similar to `pgrep` + `kill`). | `pkill -u username` (kill all processes for a user) |
| `jobs`    | **List Jobs:** Shows jobs running in the current shell (background/foreground). | `jobs`                                       |
| `fg`      | **Foreground:** Brings a background job to the foreground.      | `fg %1` (bring job 1 to foreground)          |
| `bg`      | **Background:** Sends a suspended job to the background.        | `bg %1`                                      |
| `Ctrl+C`  | **Interrupt:** Sends `SIGINT` to the foreground process.       | (Stops most foreground commands)             |
| `Ctrl+Z`  | **Suspend:** Sends `SIGTSTP` to the foreground process.        | (Suspends a foreground command)              |
| `&`       | **Run in Background:** Appends to a command to run it in the background immediately. | `long_running_script.sh &`                   |
| `nohup`   | **Run in Background (Immune to Hangup):** Runs a command that continues even if you close the terminal. | `nohup command &`                            |

---

### **7. Package Management**

Installing, updating, and removing software is done via package managers, which vary by distribution.

#### **7.1. Debian/Ubuntu (APT - Advanced Package Tool)**

*   **Repositories:** Software sources listed in `/etc/apt/sources.list` and `/etc/apt/sources.list.d/`.
*   **Packages:** `.deb` files.

| Command         | Description                                                     |
| :-------------- | :-------------------------------------------------------------- |
| `sudo apt update` | **Refresh Repositories:** Downloads latest package lists (does not upgrade). |
| `sudo apt upgrade`| **Upgrade Installed Packages:** Upgrades all installed packages to their latest versions. |
| `sudo apt install <pkg>`| **Install Package:** Installs a new package.                          |
| `sudo apt remove <pkg>` | **Remove Package:** Removes a package, leaving configuration files. |
| `sudo apt purge <pkg>`  | **Purge Package:** Removes a package and its configuration files.  |
| `sudo apt autoremove`| **Remove Unused Dependencies:** Removes packages installed as dependencies that are no longer needed. |
| `apt search <keyword>`| **Search Packages:** Searches for packages containing a keyword.   |
| `apt show <pkg>`  | **Show Package Details:** Displays detailed info about a package.  |
| `dpkg -i <file.deb>`| **Install Local .deb:** Installs a `.deb` file directly (APT handles dependencies better). |
| `dpkg -l`         | **List Installed Packages:** Shows all installed `.deb` packages. |

#### **7.2. Red Hat/CentOS/Fedora (YUM/DNF - Yellowdog Updater, Modified / DNF is the next-gen YUM)**

*   **Repositories:** Software sources listed in `/etc/yum.repos.d/` (YUM) or `/etc/dnf/` (DNF).
*   **Packages:** `.rpm` files.

| Command           | Description                                                     |
| :---------------- | :-------------------------------------------------------------- |
| `sudo dnf check-update` | **Refresh Repositories:** Checks for available updates.       |
| `sudo dnf update`   | **Update System:** Updates all installed packages.            |
| `sudo dnf install <pkg>`| **Install Package:** Installs a new package.                  |
| `sudo dnf remove <pkg>` | **Remove Package:** Removes a package.                        |
| `sudo dnf autoremove`| **Remove Unused Dependencies:** Removes packages installed as dependencies that are no longer needed. |
| `dnf search <keyword>`| **Search Packages:** Searches for packages.                   |
| `dnf info <pkg>`  | **Show Package Details:** Displays detailed info.             |
| `rpm -ivh <file.rpm>`| **Install Local .rpm:** Installs a `.rpm` file directly (DNF handles dependencies better). |
| `rpm -qa`         | **List Installed Packages:** Shows all installed `.rpm` packages. |

---

### **8. Service Management (systemd)**

Most modern Linux distributions use `systemd` to manage system services (daemons).

| Command          | Description                                                     |
| :--------------- | :-------------------------------------------------------------- |
| `systemctl status <service>` | **Check Status:** Shows if a service is running, enabled, etc. |
| `systemctl start <service>` | **Start Service:** Starts a service.                            |
| `systemctl stop <service>`  | **Stop Service:** Stops a running service.                      |
| `systemctl restart <service>`| **Restart Service:** Restarts a service.                        |
| `systemctl reload <service>` | **Reload Service:** Reloads service configuration without full restart (if supported). |
| `systemctl enable <service>` | **Enable Service:** Configures service to start on boot.        |
| `systemctl disable <service>`| **Disable Service:** Configures service *not* to start on boot. |
| `systemctl is-active <service>`| **Check if Active:** Returns 0 if active, 1 otherwise.          |
| `systemctl is-enabled <service>`| **Check if Enabled:** Returns 0 if enabled, 1 otherwise.        |
| `systemctl list-units --type=service`| **List Services:** Shows all loaded service units.             |
| `journalctl -u <service>` | **View Service Logs:** Displays logs for a specific service.    |

---

### **9. Archiving & Compression**

Dealing with archives and compressed files is a daily task.

| Command    | Description                                                     | Examples                                     |
| :--------- | :-------------------------------------------------------------- | :------------------------------------------- |
| `tar`      | **Tape Archiver:** Combines multiple files into a single archive (`.tar` file). | `tar -cvf archive.tar dir/` (create), `tar -xvf archive.tar` (extract) |
| `gzip`     | **GNU Zip:** Compresses single files.                           | `gzip file.txt` (creates `file.txt.gz`), `gzip -d file.txt.gz` (decompress) |
| `gunzip`   | **Decompress Gzip:** Decompresses `gzip` files.                  | `gunzip file.txt.gz`                         |
| `bzip2`    | **Bzip2:** Compresses files with better compression than gzip (slower). | `bzip2 file.txt` (creates `file.txt.bz2`), `bzip2 -d file.txt.bz2` (decompress) |
| `bunzip2`  | **Decompress Bzip2:** Decompresses `bzip2` files.                | `bunzip2 file.txt.bz2`                       |
| `xz`       | **Xz:** Even better compression than bzip2 (slower).            | `xz file.txt` (creates `file.txt.xz`), `xz -d file.txt.xz` (decompress) |
| `unxz`     | **Decompress Xz:** Decompresses `xz` files.                      | `unxz file.txt.xz`                           |
| `zip`      | **Zip Archive:** Creates `.zip` archives (common across OSes). | `zip archive.zip file1 file2 dir/`           |
| `unzip`    | **Unzip Archive:** Extracts `.zip` archives.                    | `unzip archive.zip`                          |

**Common Combined `tar` Commands:**

*   **Create compressed archive:**
    *   `tar -czvf archive.tar.gz directory/` (gzip)
    *   `tar -cjvf archive.tar.bz2 directory/` (bzip2)
    *   `tar -cJvf archive.tar.xz directory/` (xz)
*   **Extract compressed archive:**
    *   `tar -xzvf archive.tar.gz`
    *   `tar -xjvf archive.tar.bz2`
    *   `tar -xJvf archive.tar.xz`

---

### **10. Networking Basics (Linux Context)**

While full networking is extensive, these are Linux commands for network interaction.

| Command       | Description                                                     | Examples                                     |
| :------------ | :-------------------------------------------------------------- | :------------------------------------------- |
| `ip addr`     | **IP Address:** Displays network interface addresses (modern replacement for `ifconfig`). | `ip addr show`, `ip -c addr show` (colorized) |
| `ip route`    | **IP Routing Table:** Displays and manages the kernel's IP routing tables. | `ip route show`                              |
| `ping`        | **Packet Internet Groper:** Tests network connectivity to a host. | `ping google.com`, `ping -c 4 192.168.1.1`   |
| `netstat`     | **Network Statistics:** Shows active network connections, routing tables, interface statistics (legacy). | `netstat -tulnp` (TCP, UDP, Listen, Numeric, Programs) |
| `ss`          | **Socket Statistics:** Faster, more powerful replacement for `netstat`. | `ss -tulnp`                                  |
| `dig`         | **Domain Information Groper:** Query DNS servers for name resolution. | `dig google.com`, `dig @8.8.8.8 example.com` |
| `nslookup`    | **Name Server Lookup:** Another tool for DNS queries (often used interactively). | `nslookup google.com`                        |
| `traceroute`  | **Trace Route:** Displays the route packets take to a network host. | `traceroute google.com`                      |
| `tracepath`   | **Trace Path (MTU):** Traces path and discovers MTU.           | `tracepath google.com`                       |
| `nmap`        | **Network Mapper:** Network discovery and security auditing tool (often needs installation). | `nmap localhost`, `nmap -sT 192.168.1.1` (TCP connect scan) |
| `ssh`         | **Secure Shell:** Connects to remote Linux servers securely.   | `ssh user@hostname_or_ip`, `ssh -p 2222 user@host` |
| `scp`         | **Secure Copy:** Securely copies files between local and remote hosts. | `scp localfile.txt user@host:/remote/path/`, `scp user@host:/remote/file.txt .` |
| `sftp`        | **Secure File Transfer Protocol:** Interactive secure file transfer. | `sftp user@host`                             |
| `/etc/network/interfaces` | **Network Configuration (Debian/Ubuntu):** Defines network interfaces. |                                              |
| `/etc/sysconfig/network-scripts/ifcfg-<interface>` | **Network Configuration (Red Hat/CentOS):** Defines network interfaces. |                                              |
| `/etc/resolv.conf` | **DNS Resolver Configuration:** Specifies DNS servers.        | `nameserver 8.8.8.8`                         |
| `/etc/hosts`   | **Local Hostname Resolution:** Maps hostnames to IP addresses locally. | `127.0.0.1 localhost`                        |

---

### **11. System Monitoring & Performance**

Keeping an eye on your system's health.

| Command   | Description                                                     | Examples                                     |
| :-------- | :-------------------------------------------------------------- | :------------------------------------------- |
| `df`      | **Disk Free:** Reports filesystem disk space usage.             | `df -h` (human-readable)                     |
| `du`      | **Disk Usage:** Estimates file space usage.                     | `du -sh /var/log` (summary, human-readable for a directory) |
| `free`    | **Memory Usage:** Displays amount of free and used memory.      | `free -h`                                    |
| `uptime`  | **System Uptime & Load:** Shows how long the system has been running, and load averages. | `uptime`                                     |
| `iostat`  | **I/O Statistics:** Reports CPU utilization and I/O statistics for devices/partitions (from `sysstat` package). | `iostat -x 1` (extended stats every 1 second) |
| `vmstat`  | **Virtual Memory Statistics:** Reports virtual memory statistics. | `vmstat 1