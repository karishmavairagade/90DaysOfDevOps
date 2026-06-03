Check running processes
Inspect one systemd service
Capture a small troubleshooting flow

running processes are checked by - ps command (current shell process) and ps aux (shows processes by other users as well with other details like PID,CPU, memory etc) 

root@new-server:~# ps
    PID TTY          TIME CMD
   2534 pts/0    00:00:00 sudo
   2535 pts/0    00:00:00 bash
   3375 pts/0    00:00:00 ps

root@new-server:~# ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.6 105956 13084 ?        Ss   11:52   0:03 /sbin/init
root           2  0.0  0.0      0     0 ?        S    11:52   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        I<   11:52   0:00 [rcu_gp]
root           4  0.0  0.0      0     0 ?        I<   11:52   0:00 [rcu_par_gp]
root           6  0.0  0.0      0     0 ?        I<   11:52   0:00 [kworker/0:0H-kblockd]
root           8  0.0  0.0      0     0 ?        I<   11:52   0:00 [mm_percpu_wq]
root           9  0.0  0.0      0     0 ?        S    11:52   0:02 [ksoftirqd/0]

Inspecting process eg: nginx

root@new-server:~# ps aux | grep nginx
root        3080  0.0  0.0  51216  1468 ?        Ss   13:24   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
www-data    3081  0.0  0.2  51780  5164 ?        S    13:24   0:00 nginx: worker process
root        3419  0.0  0.0   6300   724 pts/0    S+   13:30   0:00 grep --color=auto nginx

checking with PID
root@new-server:~# ps 3080
    PID TTY      STAT   TIME COMMAND
   3080 ?        Ss     0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;

root@new-server:~# systemctl status nginx.service
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2026-06-03 13:24:10 UTC; 7min ago
       Docs: man:nginx(8)
   Main PID: 3080 (nginx)
      Tasks: 2 (limit: 2250)
     Memory: 4.9M
     CGroup: /system.slice/nginx.service
             ├─3080 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
             └─3081 nginx: worker process

Jun 03 13:24:10 new-server systemd[1]: Starting A high performance web server and a reverse proxy server...
Jun 03 13:24:10 new-server systemd[1]: Started A high performance web server and a reverse proxy server.




To check configuration
root@new-server:~# cat /etc/nginx/nginx.conf

