Task 1: Create Users (20 minutes)

Create three users with home directories and passwords:

    tokyo
    berlin
    professor


To create users:
    useradd <user-name>
      eg: useradd tokyo

search id :
id tokyo berlin proffessor
uid=1001(tokyo) gid=1001(tokyo) groups=1001(tokyo)
uid=1002(berlin) gid=1002(berlin) groups=1002(berlin)
uid=1003(proffessor) gid=1003(proffessor) groups=1003(proffessor)
karishma@karishma-Vostro-3400:~/Devops/90daysofDevops/90DaysOfDevOps/2026/day-09$ ls -ld /home/tokyo /home/berlin /home/proffessor
drwxr-x--- 2 berlin     berlin     4096 Aug  9 23:32 /home/berlin
drwxr-x--- 2 proffessor proffessor 4096 Aug  9 23:33 /home/proffessor
drwxr-x--- 2 tokyo      tokyo      4096 Aug  9 23:32 /home/tokyo
karishma@karishma-Vostro-3400:~/Devops/90daysofDevops/90DaysOfDevOps/2026/day-09$ 

/etc/passwd file

grep -E 'tokyo|berlin|proffessor' /etc/passwd
tokyo:x:1001:1001::/home/tokyo:/bin/sh
berlin:x:1002:1002::/home/berlin:/bin/sh
proffessor:x:1003:1003::/home/proffessor:/bin/sh

karishma@karishma-Vostro-3400:/home$ ls -ltrh
total 16K
drwxr-x--- 25 karishma   karishma   4.0K Aug  9 23:32 karishma
drwxr-x---  2 tokyo      tokyo      4.0K Aug  9 23:32 tokyo
drwxr-x---  2 berlin     berlin     4.0K Aug  9 23:32 berlin
drwxr-x---  2 proffessor proffessor 4.0K Aug  9 23:33 proffessor

*******************************************************************************************************************
Task 2: Create Groups 

To create groupd:
sudo groupadd developers
sudo groupadd admins

To check :
karishma@karishma-Vostro-3400:~$ getent group developers
developers:x:1004:
karishma@karishma-Vostro-3400:~$ getent group admins
admins:x:1005:

to check cat /etc/group

karishma@karishma-Vostro-3400:~$ grep -E 'developers|admin' /etc/group
lpadmin:x:111:karishma
developers:x:1004:
admins:x:1005:
karishma@karishma-Vostro-3400:~$ 

***********************************************************************************************************
Task 3: Assign to Groups

Assign users:

    tokyo → developers
    berlin → developers + admins (both groups)
    professor → admins

Verify: Use appropriate command to check group membership

To add users:

karishma@karishma-Vostro-3400:~$ sudo usermod -aG developers tokyo
karishma@karishma-Vostro-3400:~$ sudo usermod -aG developers,admins berlin
karishma@karishma-Vostro-3400:~$ sudo usermod -aG admins proffessor

karishma@karishma-Vostro-3400:~$ id tokyo berlin proffessor 
uid=1001(tokyo) gid=1001(tokyo) groups=1001(tokyo),1004(developers)
uid=1002(berlin) gid=1002(berlin) groups=1002(berlin),1004(developers),1005(admins)
uid=1003(proffessor) gid=1003(proffessor) groups=1003(proffessor),1005(admins)

*******************************************************************************************************************

Task 4: Shared Directory

    Create directory: /opt/dev-project
    Set group owner to developers
    Set permissions to 775 (rwxrwxr-x)
    Test by creating files as tokyo and berlin

Verify: Check permissions and test file creation

arishma@karishma-Vostro-3400:~/practice$ sudo mkdir -p /opt/dev-project
karishma@karishma-Vostro-3400:~/practice$ sudo chown :developers /opt/dev-project
karishma@karishma-Vostro-3400:~/practice$ sudo chmod 775 /opt/dev-project
karishma@karishma-Vostro-3400:~/practice$ ls -ld /opt/dev-project
drwxrwxr-x 2 root developers 4096 Aug  9 23:52 /opt/dev-project
karishma@karishma-Vostro-3400:~/practice$ sudo -u tokyo touch /opt/dev-project/tokyo.txt
karishma@karishma-Vostro-3400:~/practice$ sudo -u berlin touch /opt/dev-project/berlin.txt
karishma@karishma-Vostro-3400:~/practice$ ls -l /opt/dev-project
total 0
-rw-r--r-- 1 berlin berlin 0 Aug  9 23:53 berlin.txt
-rw-r--r-- 1 tokyo  tokyo  0 Aug  9 23:53 tokyo.txt
karishma@karishma-Vostro-3400:~/practice$ 

********************************************************************************************************************

Task 5: Team Workspace 

    Create user nairobi with home directory
    Create group project-team
    Add nairobi and tokyo to project-team
    Create /opt/team-workspace directory
    Set group to project-team, permissions to 775
    Test by creating file as nairobi

karishma@karishma-Vostro-3400:~/practice$ sudo useradd -m nairobi
karishma@karishma-Vostro-3400:~/practice$ sudo groupadd project-team
karishma@karishma-Vostro-3400:~/practice$ sudo usermod -aG project-team nairobi
karishma@karishma-Vostro-3400:~/practice$ sudo usermod -aG project-team tokyo
karishma@karishma-Vostro-3400:~/practice$ sudo mkdir -p /opt/team-workspace
karishma@karishma-Vostro-3400:~/practice$ sudo chown :project-team /opt/team-workspace
karishma@karishma-Vostro-3400:~/practice$ sudo chmod 775 /opt/team-workspace
karishma@karishma-Vostro-3400:~/practice$ sudo -u nairobi touch /opt/team-workspace/nairobi.txt
karishma@karishma-Vostro-3400:~/practice$ ls -ld /opt/team-workspace
drwxrwxr-x 2 root project-team 4096 Aug  9 23:57 /opt/team-workspace
karishma@karishma-Vostro-3400:~/practice$ ls -l /opt/team-workspace
total 0
-rw-r--r-- 1 nairobi nairobi 0 Aug  9 23:57 nairobi.txt
karishma@karishma-Vostro-3400:~/practice$ groups nairobi tokyo 
nairobi : nairobi project-team
tokyo : tokyo developers project-team
karishma@karishma-Vostro-3400:~/practice$ 

