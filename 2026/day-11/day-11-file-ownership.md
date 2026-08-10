Task 1: Understanding Ownership 

    Run ls -l in your home directory
    Identify the owner and group columns
    Check who owns your files

Format: -rw-r--r-- 1 owner group size date filename

Document: What's the difference between owner and group?

root@MyPc:/home/karishma# ls -l
total 344
drwxrwxr-x 9 karishma karishma   4096 Aug 10 00:11  90DaysOfDevOps
drwxr-xr-x 2 karishma karishma   4096 Jul  2 18:56  Desktop
drwxr-xr-x 3 karishma karishma   4096 Aug  9 15:01  Documents
drwxr-xr-x 5 karishma karishma   4096 Aug 10 22:57  Downloads
-rw-rw-r-- 1 karishma karishma    108 Aug 10 00:11 'GITHUB Token ghp KjrPW76G1i2Zm2JMbt6vZW5tMWB4Px23kNTc.md'
-rw-rw-r-- 1 karishma karishma    142 Aug 10 22:01  Github-token
drwxr-xr-x 2 karishma karishma   4096 Jul  2 18:56  Music
drwxr-xr-x 3 karishma karishma   4096 Aug  2 12:56  Pictures
drwxr-xr-x 2 karishma karishma   4096 Jul  2 18:56  Public
drwxr-xr-x 2 karishma karishma   4096 Jul  2 18:56  Templates
drwxr-xr-x 2 karishma karishma   4096 Jul  2 18:56  Videos
-rw-rw-r-- 1 karishma karishma 296761 Aug  9 23:16  nginx.img.odt
drwxrwxr-x 2 karishma karishma   4096 Aug  9 23:52  practice
drwx------ 8 karishma karishma   4096 Jul 10 17:42  snap
root@MyPc:/home/karishma# 

karishma karishma 1st karishma is the owner and 2nd is group.

All the files and folders here are owned by karishma

**********************************************************************************

Task 2: Basic chown Operations 

    Create file devops-file.txt
    Check current owner: ls -l devops-file.txt
    Change owner to tokyo (create user if needed)
    Change owner to berlin
    Verify the changes

root@MyPc:/home/karishma/practice# touch devops-file.txt

root@MyPc:/home/karishma/practice# ls -ltr devops-file.txt 
-rw-r--r-- 1 root root 0 Aug 10 23:24 devops-file.txt

root@MyPc:/home/karishma/practice# adduser tokyo
fatal: The user `tokyo' already exists.

root@MyPc:/home/karishma/practice# chown tokyo devops-file.txt 

root@MyPc:/home/karishma/practice# ls -ltrh devops-file.txt 
-rw-r--r-- 1 tokyo root 0 Aug 10 23:24 devops-file.txt

root@MyPc:/home/karishma/practice# chown berlin devops-file.txt 

root@MyPc:/home/karishma/practice# ls -ltrh devops-file.txt 
-rw-r--r-- 1 berlin root 0 Aug 10 23:24 devops-file.txt
root@MyPc:/home/karishma/practice# 

**************************************************************************

Task 3: Basic chgrp Operations 

    Create file team-notes.txt
    Check current group: ls -l team-notes.txt
    Create group: sudo groupadd heist-team
    Change file group to heist-team
    Verify the change

root@MyPc:/home/karishma/practice# touch team-notes.txt

root@MyPc:/home/karishma/practice# ls -l team-notes.txt 
-rw-r--r-- 1 root root 0 Aug 10 23:26 team-notes.txt

root@MyPc:/home/karishma/practice# groupadd heist-team

root@MyPc:/home/karishma/practice# chgrp heist-team team-notes.txt 

root@MyPc:/home/karishma/practice# ls -ltr team-notes.txt 
-rw-r--r-- 1 root heist-team 0 Aug 10 23:26 team-notes.txt

***********************************************************************

Task 4: Combined Owner & Group Change 

Using chown you can change both owner and group together:

    Create file project-config.yaml
    Change owner to professor AND group to heist-team (one command)
    Create directory app-logs/
    Change its owner to berlin and group to heist-team

root@MyPc:/home/karishma/practice# touch project-config.yaml
root@MyPc:/home/karishma/practice# ls -ltr project-config.yaml 
-rw-r--r-- 1 root root 0 Aug 10 23:29 project-config.yaml
root@MyPc:/home/karishma/practice# 

root@MyPc:/home/karishma/practice# chown proffessor:heist-team project-config.yaml 
root@MyPc:/home/karishma/practice# ls -ltr project-config.yaml 
-rw-r--r-- 1 proffessor heist-team 0 Aug 10 23:29 project-config.yaml
root@MyPc:/home/karishma/practice# 

root@MyPc:/home/karishma/practice# chown proffessor:heist-team project-config.yaml 
root@MyPc:/home/karishma/practice# ls -ltr project-config.yaml 
-rw-r--r-- 1 proffessor heist-team 0 Aug 10 23:29 project-config.yaml
root@MyPc:/home/karishma/practice# 

root@MyPc:/home/karishma/practice# mkdir app-logs
root@MyPc:/home/karishma/practice# chown berlin:heist-team app-logs/
root@MyPc:/home/karishma/practice# ls -ltr 
total 4
-rw-r--r-- 1 berlin     root          0 Aug 10 23:24 devops-file.txt
-rw-r--r-- 1 root       heist-team    0 Aug 10 23:26 team-notes.txt
-rw-r--r-- 1 proffessor heist-team    0 Aug 10 23:29 project-config.yaml
drwxr-xr-x 2 berlin     heist-team 4096 Aug 10 23:33 app-logs
root@MyPc:/home/karishma/practice# 

***********************************************************************************

ask 5: Recursive Ownership (20 minutes)

    Create directory structure:

    mkdir -p heist-project/vault
    mkdir -p heist-project/plans
    touch heist-project/vault/gold.txt
    touch heist-project/plans/strategy.conf

    Create group planners: sudo groupadd planners

    Change ownership of entire heist-project/ directory:
        Owner: professor
        Group: planners
        Use recursive flag (-R)

    Verify all files and subdirectories changed: ls -lR heist-project/

root@MyPc:/home/karishma/practice# mkdir -p heist-project/vault
root@MyPc:/home/karishma/practice#   mkdir -p heist-project/plans
root@MyPc:/home/karishma/practice# touch heist-project/vault/gold.txt
root@MyPc:/home/karishma/practice# touch heist-project/plans/strategy.conf
root@MyPc:/home/karishma/practice# sudo groupadd planners
root@MyPc:/home/karishma/practice# ls -ltr heist-project/
total 8
drwxr-xr-x 2 root root 4096 Aug 10 23:35 vault
drwxr-xr-x 2 root root 4096 Aug 10 23:35 plans
root@MyPc:/home/karishma/practice# chown -R proffessor:planners heist-project/
root@MyPc:/home/karishma/practice# ls -ltr heist-project/
total 8
drwxr-xr-x 2 proffessor planners 4096 Aug 10 23:35 vault
drwxr-xr-x 2 proffessor planners 4096 Aug 10 23:35 plans
root@MyPc:/home/karishma/practice# 

**************************************************************************

Task 6: Practice Challenge 

Create users: tokyo, berlin, nairobi (if not already created)
Create groups: vault-team, tech-team
Create directory: bank-heist/
Create 3 files inside:
	touch bank-heist/access-codes.txt
	touch bank-heist/blueprints.pdf
    	touch bank-heist/escape-plan.txt

Set different ownership:
        access-codes.txt → owner: tokyo, group: vault-team
        blueprints.pdf → owner: berlin, group: tech-team
        escape-plan.txt → owner: nairobi, group: vault-team

Verify: ls -l bank-heist/


root@MyPc:/home/karishma/practice# id tokyo berlin nairobi 
uid=1001(tokyo) gid=1001(tokyo) groups=1001(tokyo),1004(developers),1007(project-team)
uid=1002(berlin) gid=1002(berlin) groups=1002(berlin),1004(developers),1005(admins)
uid=1004(nairobi) gid=1006(nairobi) groups=1006(nairobi),1007(project-team)

root@MyPc:/home/karishma/practice# groupadd vault-team
root@MyPc:/home/karishma/practice# groupadd tech-team

root@MyPc:/home/karishma/practice# mkdir bank-heist/
root@MyPc:/home/karishma/practice# touch bank-heist/access-codes.txt
root@MyPc:/home/karishma/practice# touch bank-heist/blueprints.pdf
root@MyPc:/home/karishma/practice# touch bank-heist/escape-plan.txt
root@MyPc:/home/karishma/practice# ls -ltr bank-heist/
total 0
-rw-r--r-- 1 root root 0 Aug 10 23:41 access-codes.txt
-rw-r--r-- 1 root root 0 Aug 10 23:41 blueprints.pdf
-rw-r--r-- 1 root root 0 Aug 10 23:41 escape-plan.txt

root@MyPc:/home/karishma/practice# chown tokyo:vault-team bank-heist/access-codes.txt
root@MyPc:/home/karishma/practice# chown berlin:tech-team bank-heist/blueprints.pdf
root@MyPc:/home/karishma/practice# chown nairobi:vault-team bank-heist/escape-plan.txt

root@MyPc:/home/karishma/practice# ls -ltr bank-heist/
total 0
-rw-r--r-- 1 tokyo   vault-team 0 Aug 10 23:41 access-codes.txt
-rw-r--r-- 1 berlin  tech-team  0 Aug 10 23:41 blueprints.pdf
-rw-r--r-- 1 nairobi vault-team 0 Aug 10 23:41 escape-plan.txt
root@MyPc:/home/karishma/practice# 





