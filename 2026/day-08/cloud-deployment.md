Part 1: Launch Cloud Instance & SSH Access 

Step 1: Create a Cloud Instance

Step 2: Connect via SSH
arishma@karishma-Vostro-3400:~/Downloads$ chmod 400 "kubectl-key.pem"
karishma@karishma-Vostro-3400:~/Downloads$ ssh -i "kubectl-key.pem" ubuntu@ec2-44-197-179-251.compute-1.amazonaws.com
The authenticity of host 'ec2-44-197-179-251.compute-1.amazonaws.com (44.197.179.251)' can't be established.
ED25519 key fingerprint is: SHA256:4rEa7pRzv6J/LTYU+Tj3BrZk/YqBpxcrdVcdQZhIjqE
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'ec2-44-197-179-251.compute-1.amazonaws.com' (ED25519) to the list of known hosts.
Welcome to Ubuntu 26.04 LTS (GNU/Linux 7.0.0-1006-aws x86_64)

 * Documentation:  https://docs.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun Aug  9 17:33:03 UTC 2026

  System load:  0.16              Temperature:           -273.1 C
  Usage of /:   30.5% of 6.61GB   Processes:             122
  Memory usage: 26%               Users logged in:       0
  Swap usage:   0%                IPv4 address for ens5: 172.31.15.88

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ubuntu@ip-172-31-15-88:~$ 

*****************************************************************************************************************************
Part 2: Install Docker & Nginx

Update system: sudo apt update

Install nginx: sudo apt install nginx

Verify status : 
ubuntu@ip-172-31-15-88:~$ systemctl status nginx.service 
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: active (running) since Sun 2026-08-09 17:35:24 UTC; 31s ago
 Invocation: 492161623ccd4741b34c21494d5bf796
       Docs: man:nginx(8)
    Process: 1721 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
    Process: 1723 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
   Main PID: 1752 (nginx)
      Tasks: 3 (limit: 627)
     Memory: 3M (peak: 7M)
        CPU: 45ms
     CGroup: /system.slice/nginx.service
             ├─1752 "nginx: master process /usr/sbin/nginx -g daemon on; master_process on;"
             ├─1755 "nginx: worker process"
             └─1756 "nginx: worker process"

Aug 09 17:35:24 ip-172-31-15-88 systemd[1]: Starting nginx.service - A high performance web server and a reverse proxy server...
Aug 09 17:35:24 ip-172-31-15-88 systemd[1]: Started nginx.service - A high performance web server and a reverse proxy server.
ubuntu@ip-172-31-15-88:~$ 

*********************************************************************************************************************
Part 3: Security Group Configuration

In security groups of EC2 add port 80 in inbound rules

image added in the day-08 as img

*************************************************************************************************************************
Part 4: Extract Nginx Logs
 
