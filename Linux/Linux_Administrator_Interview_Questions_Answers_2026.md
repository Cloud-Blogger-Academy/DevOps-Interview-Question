# Linux Administrator Interview Questions & Answers 

Cracking your next Linux Administrator/DevOps interview? These are
practical Linux interview questions with clear, interview-ready answers
you can explain confidently in a real interview.

💡 Want to go beyond theory and actually build, troubleshoot, secure,
and manage real Linux servers?

**Linux Red Hat Administrator Course --- ₹999 → [Enroll
Here](https://www.cloudbloggeracademy.com/courses/Redhat-Linux-Administrator-6a6a05599545794ded966ea9)**

------------------------------------------------------------------------

## 1. A Cron Job hasn't run for 5 days --- how will you troubleshoot it?

### Answer

I would troubleshoot the Cron Job step by step:

1.  **Check whether the cron service is running**

    ``` bash
    systemctl status crond
    ```

    On Ubuntu/Debian:

    ``` bash
    systemctl status cron
    ```

2.  **Check the user's crontab**

    ``` bash
    crontab -l
    ```

3.  **Verify the cron syntax**

    ``` text
    * * * * * command
    ```

    The five fields represent:

    -   Minute
    -   Hour
    -   Day of month
    -   Month
    -   Day of week

4.  **Check cron logs**

    ``` bash
    grep CRON /var/log/cron
    ```

    Or:

    ``` bash
    journalctl -u crond
    ```

5.  **Check the script permissions**

    ``` bash
    ls -l /path/script.sh
    ```

6.  **Check the script's absolute paths**

    Cron has a limited environment, so commands that work interactively
    may fail from cron. I prefer absolute paths such as
    `/usr/bin/python3` instead of only `python3`.

7.  **Check environment variables**

    Variables such as `PATH`, `HOME`, and application-specific variables
    may not be available.

8.  **Check the script manually**

    ``` bash
    /path/script.sh
    echo $?
    ```

9.  **Redirect output to a log**

    ``` bash
    * * * * * /path/script.sh >> /var/log/mycron.log 2>&1
    ```

10. **Check SELinux or permissions if applicable**
    `bash     ausearch -m AVC -ts recent`

### Interview Answer

> "First I check whether the cron service is running, then verify the
> crontab entry and syntax. After that I check cron logs, script
> permissions, absolute paths, environment variables, and the script's
> exit code. Finally, I redirect stdout and stderr to a log file and
> check SELinux or other security restrictions if required."

🎯 **Master Linux with hands-on labs → [Linux Red Hat Administrator
Course ---
₹999](https://www.cloudbloggeracademy.com/courses/Redhat-Linux-Administrator-6a6a05599545794ded966ea9)**

------------------------------------------------------------------------

## 2. What is a Cron Job?

### Answer

A **Cron Job** is a Linux task scheduler used to automatically execute
commands or scripts at a predefined time or interval.

For example:

``` bash
0 2 * * * /opt/scripts/backup.sh
```

This runs the backup script every day at **2:00 AM**.

The Cron format is:

``` text
* * * * * command
| | | | |
| | | | +--- Day of week
| | | +----- Month
| | +------- Day of month
| +--------- Hour
+----------- Minute
```

Common commands:

``` bash
crontab -l
crontab -e
```

`crontab -l` lists cron jobs, while `crontab -e` allows you to edit
them.

### Interview Answer

> "Cron is a Linux job scheduler. We use it to execute scripts or
> commands automatically at a specific time or recurring interval, such
> as backups, log cleanup, monitoring, and report generation."

🎯 **Master Linux with hands-on labs → [Linux Red Hat Administrator
Course ---
₹999](https://www.cloudbloggeracademy.com/courses/Redhat-Linux-Administrator-6a6a05599545794ded966ea9)**

------------------------------------------------------------------------

## 3. How strong is your Linux experience?

### Answer

A good interview answer should focus on practical administration rather
than simply saying a number of years.

### Interview Answer

> "I have strong hands-on experience with Linux administration. I have
> worked with user and group management, file permissions, SSH, process
> and service management, package installation, disk and filesystem
> management, LVM, networking, cron jobs, log analysis, system
> troubleshooting, firewalld, and SELinux. I am also comfortable
> troubleshooting CPU, memory, disk, networking, and application-related
> issues on production Linux servers."

You can also mention technologies relevant to the role:

-   RHEL / Rocky Linux / Ubuntu
-   Bash scripting
-   SSH
-   systemd
-   LVM
-   XFS / ext4
-   NFS
-   firewalld
-   SELinux
-   Apache / Nginx
-   Docker
-   Kubernetes
-   Cloud Linux VMs

🎯 **Master Linux with hands-on labs → [Linux Red Hat Administrator
Course ---
₹999](https://www.cloudbloggeracademy.com/courses/Redhat-Linux-Administrator-6a6a05599545794ded966ea9)**

------------------------------------------------------------------------

## 4. How can you access a Linux server without using a password?

### Answer

The standard method is **SSH key-based authentication**.

First, generate an SSH key pair on the client:

``` bash
ssh-keygen
```

This creates:

-   **Private key** --- kept securely on the client
-   **Public key** --- copied to the Linux server

Copy the public key:

``` bash
ssh-copy-id user@server-ip
```

Then connect:

``` bash
ssh user@server-ip
```

The server verifies the private key against the public key stored in:

``` bash
~/.ssh/authorized_keys
```

You can also configure SSH to disable password authentication after
validating key-based access:

``` text
PasswordAuthentication no
```

in:

``` bash
/etc/ssh/sshd_config
```

Then restart or reload SSH:

``` bash
systemctl reload sshd
```

### Important Security Point

Never share the private key. The private key should remain protected on
the client.

### Interview Answer

> "I use SSH key-based authentication. I generate a public-private key
> pair, copy the public key to the server's authorized_keys file, and
> then authenticate using the private key. This is more secure and is
> commonly used for automation."

🎯 **Master Linux with hands-on labs → [Linux Red Hat Administrator
Course ---
₹999](https://www.cloudbloggeracademy.com/courses/Redhat-Linux-Administrator-6a6a05599545794ded966ea9)**

------------------------------------------------------------------------

## 5. How do you give permissions to a specific service?

### Answer

First, I would clarify what permission the service needs. I would avoid
giving unnecessary root access.

Suppose an application service runs as:

``` text
appuser
```

and needs access to:

``` text
/opt/application/data
```

I can assign ownership:

``` bash
chown -R appuser:appgroup /opt/application/data
```

Or use a group:

``` bash
chgrp appgroup /opt/application/data
chmod 770 /opt/application/data
```

If I need to grant access to a specific user without changing the
existing ownership, I can use ACLs:

``` bash
setfacl -m u:appuser:rwx /opt/application/data
```

To verify:

``` bash
getfacl /opt/application/data
```

For a systemd service, I can also use systemd security controls and run
the service under a dedicated account:

``` ini
[Service]
User=appuser
Group=appgroup
```

### Best Practice

I follow the **principle of least privilege**. The service should
receive only the permissions required to perform its function.

### Interview Answer

> "I first identify the service account and the exact resource it needs.
> Then I use ownership, groups, ACLs, or systemd service configuration
> to provide only the required permissions. I avoid giving the service
> unnecessary root privileges."

🎯 **Master Linux with hands-on labs → [Linux Red Hat Administrator
Course ---
₹999](https://www.cloudbloggeracademy.com/courses/Redhat-Linux-Administrator-6a6a05599545794ded966ea9)**

------------------------------------------------------------------------

## 6. Name a few Linux commands you use.

### Answer

Some commonly used Linux administration commands are:

### File and Directory

``` bash
ls
cd
pwd
cp
mv
rm
mkdir
touch
find
```

### File Content and Search

``` bash
cat
less
head
tail
grep
awk
sed
sort
uniq
```

### Permissions

``` bash
chmod
chown
chgrp
getfacl
setfacl
```

### Process Management

``` bash
ps
top
htop
kill
pkill
pgrep
```

### Service Management

``` bash
systemctl
journalctl
```

### Storage

``` bash
df
du
lsblk
mount
umount
blkid
fdisk
parted
```

### LVM

``` bash
pvs
vgs
lvs
pvcreate
vgcreate
lvcreate
lvextend
```

### Networking

``` bash
ip
ss
ping
curl
nc
traceroute
dig
nslookup
```

### Package Management

RHEL-based:

``` bash
rpm
dnf
yum
```

Ubuntu/Debian:

``` bash
apt
dpkg
```

### Interview Answer

> "I regularly use commands such as ls, find, grep, awk, sed, chmod,
> chown, ps, top, systemctl, journalctl, df, du, lsblk, ip, ss, ping,
> curl, dnf, rpm, and other troubleshooting commands depending on the
> issue."

🎯 **Master Linux with hands-on labs → [Linux Red Hat Administrator
Course ---
₹999](https://www.cloudbloggeracademy.com/courses/Redhat-Linux-Administrator-6a6a05599545794ded966ea9)**

------------------------------------------------------------------------

## 7. What is the difference between scp and rsync?

### Answer

Both `scp` and `rsync` can transfer files between Linux systems over
SSH, but they are designed differently.

  -----------------------------------------------------------------------
  Feature                 SCP                     rsync
  ----------------------- ----------------------- -----------------------
  Purpose                 Simple file copy        Efficient
                                                  synchronization

  Incremental transfer    No                      Yes

  Delta transfer          No                      Yes

  Resume capability       Limited                 Better support

  Performance for         Lower                   Usually better
  repeated sync                                   

  Directory               Supported               Excellent
  synchronization                                 

  Delete extra            Not a native sync       `--delete`
  destination files       feature                 

  Common use              Quick one-time copy     Backup and
                                                  synchronization
  -----------------------------------------------------------------------

### SCP Example

``` bash
scp file.txt user@server:/tmp/
```

Copy a directory:

``` bash
scp -r /opt/app user@server:/opt/
```

### rsync Example

``` bash
rsync -avz /opt/app/ user@server:/opt/app/
```

For deletion of destination files that no longer exist at the source:

``` bash
rsync -avz --delete /opt/app/ user@server:/opt/app/
```

### Important Difference

`rsync` can compare source and destination and transfer only changed
data, which makes it very useful for repeated backups and
synchronization.

### Interview Answer

> "SCP is mainly used for simple file or directory copying, while rsync
> is designed for synchronization. Rsync is more efficient for repeated
> transfers because it can transfer only changed data and provides
> useful options for backups and mirroring."

🎯 **Master Linux with hands-on labs → [Linux Red Hat Administrator
Course ---
₹999](https://www.cloudbloggeracademy.com/courses/Redhat-Linux-Administrator-6a6a05599545794ded966ea9)**

------------------------------------------------------------------------

## 8. What is the difference between a hard link and a soft link in Linux?

### Answer

Linux supports two common types of links:

-   **Hard link**
-   **Soft link / Symbolic link**

### Hard Link

A hard link points to the same inode as the original file.

Example:

``` bash
ln file1.txt file2.txt
```

Both filenames point to the same underlying file data.

Check inode numbers:

``` bash
ls -li
```

### Soft Link

A soft link is a separate file that stores a path/reference to another
file.

Example:

``` bash
ln -s file1.txt file2.txt
```

Check it:

``` bash
ls -l
```

You will see something similar to:

``` text
file2.txt -> file1.txt
```

### Main Differences

  -----------------------------------------------------------------------
  Feature                 Hard Link               Soft Link
  ----------------------- ----------------------- -----------------------
  Points to               Same inode              Path/name

  Cross filesystem        No                      Yes

  Directory linking       Generally no            Yes

  If original file is     Data remains accessible Link becomes broken
  deleted                 through hard link       

  Different inode         No                      Yes
  -----------------------------------------------------------------------

### Interview Answer

> "A hard link points to the same inode and underlying data as the
> original file, while a soft link points to the original file path.
> Hard links generally cannot cross filesystems, whereas symbolic links
> can. If the original file is deleted, a hard link can still access the
> data, while a soft link normally becomes broken."

🎯 **Master Linux with hands-on labs → [Linux Red Hat Administrator
Course ---
₹999](https://www.cloudbloggeracademy.com/courses/Redhat-Linux-Administrator-6a6a05599545794ded966ea9)**

------------------------------------------------------------------------

## 9. What is your Linux scripting experience with Bash and PowerShell?

### Answer

### Interview Answer

> "I have experience using Bash scripting for Linux administration and
> automation. I use Bash to automate repetitive tasks such as user
> management, log cleanup, service checks, disk monitoring, backup
> operations, health checks, and deployment activities. I am comfortable
> using variables, conditions, loops, functions, exit codes, command
> substitution, pipes, redirection, and error handling."

Example Bash script:

``` bash
#!/bin/bash

DISK=$(df -h / | awk 'NR==2 {print $5}' | tr -d '%')

if [ "$DISK" -gt 80 ]; then
    echo "Warning: Disk usage is ${DISK}%"
else
    echo "Disk usage is ${DISK}%"
fi
```

For PowerShell:

> "I also understand PowerShell and use it for Windows and Microsoft
> ecosystem automation. I can work with variables, loops, conditions,
> functions, objects, pipelines, and administrative cmdlets. In a mixed
> Windows-Linux environment, I use Bash where Linux automation is
> required and PowerShell for Windows or Microsoft platform tasks."

Example PowerShell:

``` powershell
$disk = Get-PSDrive C

if ($disk.Used / ($disk.Used + $disk.Free) -gt 0.80) {
    Write-Host "Disk usage is above 80%"
}
```

### Key Bash Concepts to Know

``` bash
#!/bin/bash
variable="Linux"

if [ "$variable" = "Linux" ]; then
    echo "Linux detected"
fi

for i in 1 2 3
do
    echo "$i"
done
```

### Interview Tip

Do not claim advanced scripting if you cannot explain your scripts. Be
ready to explain:

-   Variables
-   Conditions
-   Loops
-   Functions
-   Exit status
-   `$?`
-   `$PATH`
-   Pipes `|`
-   Redirection `>`, `>>`, `2>`
-   `grep`
-   `awk`
-   `sed`
-   `cut`
-   `xargs`
-   Error handling
-   Cron automation

🎯 **Master Linux with hands-on labs → [Linux Red Hat Administrator
Course ---
₹999](https://www.cloudbloggeracademy.com/courses/Redhat-Linux-Administrator-6a6a05599545794ded966ea9)**

------------------------------------------------------------------------

# Quick Interview Revision

Before a Linux Administrator interview, make sure you can practically
demonstrate:

``` bash
systemctl status sshd
journalctl -u sshd
df -h
du -sh /var/*
free -m
top
ps aux
ss -lntp
ip addr
ip route
dig google.com
chmod 755 script.sh
chown user:group file
find / -name "*.log"
grep -i "error" /var/log/messages
crontab -l
lsblk
pvs
vgs
lvs
mount
```

### 🎯 Hands-on Linux Training

**Learn Linux Administration with practical labs → [Red Hat Linux
Administrator Course ---
₹999](https://www.cloudbloggeracademy.com/courses/Redhat-Linux-Administrator-6a6a05599545794ded966ea9)**
