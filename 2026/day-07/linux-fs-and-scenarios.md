PART-1
########################################################

Core Directories (Must Know):

    / (root) - The starting point of everything. The top-level directory of the Linux filesystem. All other directories and files exist under it.
    
    /home - User home directories. Contains personal directories and files for regular users. Example: /home/alex.
    
    /root - Root user's home directory. The home directory of the root (administrator) user. It is separate from /home.
    
    /etc - Configuration files. Stores system-wide configuration files. Examples include network, user, service, and application configurations.
    
    /var/log - Log files (very important for DevOps!) Contains system and application log files. Very useful for troubleshooting and DevOps monitoring.
    
    /tmp - Temporary files. Used for temporary files created by users and applications. Files here may be automatically deleted after a reboot.
    
    /bin - Essential command binaries. Contains essential command-line binaries needed for basic system operation. Examples: ls, cp, mv, cat.
    
/usr/bin - User command binaries. Contains most user-level command binaries and utilities installed on the system. Examples: git, python, curl.

/opt - Optional/third-party applications. Used for installing optional or third-party software packages. Often used for applications that are self-contained.

##############  HANDS ON TASK #########################

# Find the largest log file in /var/log
du -sh /var/log/* 2>/dev/null | sort -h | tail -5
4.4M	/var/log/syslog.2.gz
7.0M	/var/log/syslog.4.gz
27M	/var/log/syslog
71M	/var/log/syslog.1
794M	/var/log/journal


# Look at a config file in /etc
cat /etc/hostname
karishma-Vostro-3400

# Check your home directory
ls -la ~
total 168
drwxr-x--- 25 karishma karishma  4096 Aug  9 22:27 .
drwxr-xr-x  3 root     root      4096 Jul  2 18:43 ..
drwxrwxr-x  2 karishma karishma  4096 Jul 22 12:25 .aws
-rw-------  1 karishma karishma 17422 Aug  9 21:57 .bash_history
-rw-r--r--  1 karishma karishma   220 Feb 13 17:46 .bash_logout
-rw-r--r--  1 karishma karishma  3771 Feb 13 17:46 .bashrc
drwx------ 20 karishma karishma  4096 Aug  2 13:14 .cache
drwx------ 22 karishma karishma  4096 Aug  9 15:07 .config
drwx------  4 karishma karishma  4096 Jul 31 01:14 .copilot
drwxr-xr-x 10 karishma karishma  4096 Aug  9 21:57 .docker
drwxrwxr-x  3 karishma karishma  4096 Jul 13 16:14 .dotnet
-rw-rw-r--  1 karishma karishma   101 Jul 23 22:59 .gitconfig
drwx------  2 karishma karishma  4096 Aug  9 22:24 .gnupg
drwxr-xr-x  3 karishma karishma  4096 Jul  4 23:52 .kube
drwx------  4 karishma karishma  4096 Jul  2 18:56 .local
-rw-r--r--  1 karishma karishma   807 Feb 13 17:46 .profile
drwx------  2 karishma karishma  4096 Aug  9 18:39 .ssh
drwxr-xr-x  2 karishma karishma  4096 Jul 22 12:05 .terraform.d
-rw-------  1 karishma karishma 21919 Aug  9 22:27 .viminfo
drwxrwxr-x  4 karishma karishma  4096 Jul  3 15:38 .vscode
drwxrwxr-x  3 karishma karishma  4096 Jul  3 15:38 .vscode-shared
-rw-rw-r--  1 karishma karishma   181 Jul 12 09:53 .wget-hsts
drwxr-xr-x  2 karishma karishma  4096 Jul  2 18:56 Desktop
drwxrwxr-x  7 karishma karishma  4096 Aug  9 22:03 Devops
drwxr-xr-x  3 karishma karishma  4096 Aug  9 15:01 Documents
drwxr-xr-x  3 karishma karishma  4096 Aug  9 22:00 Downloads
drwxr-xr-x  2 karishma karishma  4096 Jul  2 18:56 Music
drwxr-xr-x  3 karishma karishma  4096 Aug  2 12:56 Pictures
drwxr-xr-x  2 karishma karishma  4096 Jul  2 18:56 Public
drwxr-xr-x  2 karishma karishma  4096 Jul  2 18:56 Templates
drwxr-xr-x  2 karishma karishma  4096 Jul  2 18:56 Videos
drwx------  8 karishma karishma  4096 Jul 10 17:42 snap
##################################################################################################

PART-2



Scenario 1: Service Not Starting

A web application service called 'myapp' failed to start after a server reboot.
What commands would you run to diagnose the issue?
Write at least 4 commands in order.

Step 1: check service status
systemctl status myapp

Step 2: Check service logs
journalctl -u myapp

Step 3: Check if service is enabled on boot
systemctl is-enabled my-app
if not - systemctl enable my-app

Step 4: Restart my-app service
systemctl restart my-app
check status : systemctl status my-app

**********************************************
Scenario 2: High CPU Usage

Your manager reports that the application server is slow.
You SSH into the server. What commands would you run to identify
which process is using high CPU?

Step 1: check the mountpoints 
df -h

Step 2: Check which process using high cpu
top OR ps aux --sort=-%cpu | head

********************************

Scenario 3: Finding Service Logs

A developer asks: "Where are the logs for the 'docker' service?"
The service is managed by systemd.
What commands would you use?

Step 1: Check docker status first
systemctl status docker

Step 2: Check logs by
journalctl -u docker

Step 3: View last 50 lines of logs
journalctl -u docker -n 50

Step 4: Continously follow logs
journalctl -u docker -f 

/var/lib/docker/containers/ = container logs.

****************************************************

Scenario 4: File Permissions Issue

A script at /home/user/backup.sh is not executing.
When you run it: ./backup.sh
You get: "Permission denied"
What commands would you use to fix this?

Step 1: First check if script is present in mentioned location or not
cat /home/user/backup.sh

Step 2: Check permissions 
ls -ltr backup.sh

Step 3: Add execute permission
chmod +x backup.sh

Step 4: Run script again
./backup.sh
*******************************************




