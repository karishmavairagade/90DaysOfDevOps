You will pick a running process/service on your system and:

Capture a quick health snapshot (CPU, memory, disk, network)
Trace logs for that service
Write a mini runbook describing what you did and what you’d do next if things were worse




Here we will do troubleshooting for sshd service

root@new-server:~# uname -a
Linux new-server 5.4.0-216-generic #236-Ubuntu SMP Fri Apr 11 19:53:21 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
root@new-server:~# cat /etc/os-release
NAME="Ubuntu"
VERSION="20.04.6 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.6 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
root@new-server:~# cat /etc/hosts
127.0.0.1 localhost
127.0.1.1 new-server

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
root@new-server:~# df -h
Filesystem                         Size  Used Avail Use% Mounted on
udev                               938M     0  938M   0% /dev
tmpfs                              198M  1.2M  197M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv   12G  4.8G  5.9G  45% /
tmpfs                              986M     0  986M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
tmpfs                              986M     0  986M   0% /sys/fs/cgroup
/dev/loop0                          92M   92M     0 100% /snap/lxd/38688
/dev/loop2                          50M   50M     0 100% /snap/snapd/26865
/dev/loop1                          64M   64M     0 100% /snap/core20/2866
/dev/loop4                          50M   50M     0 100% /snap/snapd/18357
/dev/loop3                          64M   64M     0 100% /snap/core20/1828
/dev/loop5                          92M   92M     0 100% /snap/lxd/24061
/dev/sda2                          2.0G  114M  1.7G   7% /boot
tmpfs                              198M     0  198M   0% /run/user/1000
root@new-server:~# uname -a
Linux new-server 5.4.0-216-generic #236-Ubuntu SMP Fri Apr 11 19:53:21 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
root@new-server:~# cat /etc/os-release
NAME="Ubuntu"
VERSION="20.04.6 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.6 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
root@new-server:~# cat /etc/hosts
127.0.0.1 localhost
127.0.1.1 new-server

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
root@new-server:~# df -h
Filesystem                         Size  Used Avail Use% Mounted on
udev                               938M     0  938M   0% /dev
tmpfs                              198M  1.2M  197M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv   12G  4.8G  5.9G  45% /
tmpfs                              986M     0  986M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
tmpfs                              986M     0  986M   0% /sys/fs/cgroup
/dev/loop0                          92M   92M     0 100% /snap/lxd/38688
/dev/loop2                          50M   50M     0 100% /snap/snapd/26865
/dev/loop1                          64M   64M     0 100% /snap/core20/2866
/dev/loop4                          50M   50M     0 100% /snap/snapd/18357
/dev/loop3                          64M   64M     0 100% /snap/core20/1828
/dev/loop5                          92M   92M     0 100% /snap/lxd/24061
/dev/sda2                          2.0G  114M  1.7G   7% /boot
tmpfs                              198M     0  198M   0% /run/user/1000

root@new-server:~# netstat -tunlp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      3080/nginx: master
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      640/systemd-resolve
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      813/sshd: /usr/sbin
tcp6       0      0 :::80                   :::*                    LISTEN      3080/nginx: master
tcp6       0      0 :::22                   :::*                    LISTEN      813/sshd: /usr/sbin
udp        0      0 127.0.0.53:53           0.0.0.0:*                           640/systemd-resolve
udp        0      0 192.168.1.50:68         0.0.0.0:*                           638/systemd-network
udp6       0      0 fe80::a00:27ff:fe60:546 :::*                                638/systemd-network

root@new-server:~# journalctl -u ssh.service
-- Logs begin at Thu 2026-05-07 13:13:10 UTC, end at Wed 2026-06-03 13:43:19 UTC. --
May 07 13:18:39 new-server systemd[1]: Starting OpenBSD Secure Shell server...
May 07 13:18:39 new-server sshd[1493]: Server listening on 0.0.0.0 port 22.
May 07 13:18:39 new-server sshd[1493]: Server listening on :: port 22.
May 07 13:18:39 new-server systemd[1]: Started OpenBSD Secure Shell server.
-- Reboot --
May 16 12:58:55 new-server systemd[1]: Starting OpenBSD Secure Shell server...
May 16 12:58:55 new-server sshd[811]: Server listening on 0.0.0.0 port 22.
May 16 12:58:55 new-server sshd[811]: Server listening on :: port 22.
May 16 12:58:55 new-server systemd[1]: Started OpenBSD Secure Shell server.
May 17 04:45:06 new-server sshd[2283]: Accepted password for karu from 192.168.1.7 port 58076 ssh2
May 17 04:45:06 new-server sshd[2283]: pam_unix(sshd:session): session opened for user karu by (uid=0)
-- Reboot --
Jun 03 11:52:22 new-server systemd[1]: Starting OpenBSD Secure Shell server...
Jun 03 11:52:22 new-server sshd[813]: Server listening on 0.0.0.0 port 22.
Jun 03 11:52:22 new-server sshd[813]: Server listening on :: port 22.
Jun 03 11:52:22 new-server systemd[1]: Started OpenBSD Secure Shell server.
Jun 03 11:55:52 new-server sshd[1165]: Accepted password for karu from 192.168.1.14 port 64277 ssh2
Jun 03 11:55:52 new-server sshd[1165]: pam_unix(sshd:session): session opened for user karu by (uid=0)
Jun 03 12:58:54 new-server sshd[1599]: Accepted password for karu from 192.168.1.14 port 65059 ssh2
Jun 03 12:58:54 new-server sshd[1599]: pam_unix(sshd:session): session opened for user karu by (uid=0)
Jun 03 13:22:43 new-server sshd[2433]: Accepted password for karu from 192.168.1.14 port 65310 ssh2
Jun 03 13:22:43 new-server sshd[2433]: pam_unix(sshd:session): session opened for user karu by (uid=0)
root@new-server:~#


We will check CPU and memory utilization of server
top/htop/iostat -- CPU
free -gh/top --memory

To check logs and configuration use

journalctl -u ssh.service
systemctl status ssh.service
grep sshd /var/log/auth.log | tail -50

configuration at /etc/sshd/sshd.conf


If sshd is consumimg much memory and CPU we can restart the sshd, we can also increase disk space
