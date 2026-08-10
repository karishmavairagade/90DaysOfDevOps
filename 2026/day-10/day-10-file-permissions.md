Task 1: Create Files


    Create empty file devops.txt using touch
    Create notes.txt with some content using cat or echo
    Create script.sh using vim with content: echo "Hello DevOps"

Verify: ls -l to see permissions

root@MyPc:~# touch devops.txt

root@MyPc:~# echo "This is new file" > notes.txt

root@MyPc:~# cat >> notes.txt 
This is new line being appended to original file
Line no3
Line no 4
root@MyPc:~# cat  notes.txt 
This is new file
This is new line being appended to original file
Line no3
Line no 4

root@MyPc:~# echo "Hello Devops" > script.sh
root@MyPc:~# ls
devops.txt  notes.txt  script.sh  snap
root@MyPc:~# 

*************************************************************************************
Task 2: Read Files 

    Read notes.txt using cat
    View script.sh in vim read-only mode
    Display first 5 lines of /etc/passwd using head
    Display last 5 lines of /etc/passwd using tail

root@MyPc:~# cat notes.txt 
This is new file
This is new line being appended to original file
Line no3
Line no 4

root@MyPc:~# vim -R script.sh 

root@MyPc:~# head -n 5 /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync

root@MyPc:~# tail -n 5 /etc/passwd
karishma:x:1000:1000:Karishma:/home/karishma:/bin/bash
tokyo:x:1001:1001::/home/tokyo:/bin/sh
berlin:x:1002:1002::/home/berlin:/bin/sh
proffessor:x:1003:1003::/home/proffessor:/bin/sh
nairobi:x:1004:1006::/home/nairobi:/bin/sh

*******************************************************************************************************
Task 3: Understand Permissions 
Format: rwxrwxrwx (owner-group-others)

    r = read (4), w = write (2), x = execute (1)

Check your files: ls -l devops.txt notes.txt script.sh

Answer: What are current permissions? Who can read/write/execute?

root@MyPc:~# ls -ltrh
total 12K
drwx------ 10 root root 4.0K Jul  2 18:56 snap
-rw-r--r--  1 root root    0 Aug 10 23:01 devops.txt
-rw-r--r--  1 root root   85 Aug 10 23:04 notes.txt
-rw-r--r--  1 root root   13 Aug 10 23:06 script.sh
root@MyPc:~# 

for all devops, notes and script USER has read, write permission and Group and others has read only

**********************************************************************************************************

Task 4: Modify Permissions 

Make script.sh executable → run it with ./script.sh

root@MyPc:~# chmod +x script.sh 
root@MyPc:~# ls -ltr script.sh 
-rwxr-xr-x 1 root root 20 Aug 10 23:13 script.sh
root@MyPc:~# ./script.sh 
Hello Devops
root@MyPc:~# 

    
Set devops.txt to read-only (remove write for all)
root@MyPc:~# ls -ltr
total 12
drwx------ 10 root root 4096 Jul  2 18:56 snap
-rw-r--r--  1 root root    0 Aug 10 23:01 devops.txt
-rw-r--r--  1 root root   85 Aug 10 23:04 notes.txt
-rwxr-xr-x  1 root root   20 Aug 10 23:13 script.sh
root@MyPc:~# chmod u-x devops.txt 
root@MyPc:~# ls -ltr devops.txt 
-rw-r--r-- 1 root root 0 Aug 10 23:01 devops.txt
root@MyPc:~# 

Set notes.txt to 640 (owner: rw, group: r, others: none)

root@MyPc:~# ls -ltr notes.txt 
-rw-r--r-- 1 root root 85 Aug 10 23:04 notes.txt
root@MyPc:~# chmod 640 notes.txt 
root@MyPc:~# ls -ltr notes.txt 
-rw-r----- 1 root root 85 Aug 10 23:04 notes.txt
root@MyPc:~# 

Create directory project/ with permissions 755
Verify: ls -l after each change

root@MyPc:~# mkdir -m 755 project
root@MyPc:~# ls -ltr
total 16
drwx------ 10 root root 4096 Jul  2 18:56 snap
-rw-r--r--  1 root root    0 Aug 10 23:01 devops.txt
-rw-r-----  1 root root   85 Aug 10 23:04 notes.txt
-rwxr-xr-x  1 root root   20 Aug 10 23:13 script.sh
drwxr-xr-x  2 root root 4096 Aug 10 23:19 project
root@MyPc:~# 

*******************************************************************************************
