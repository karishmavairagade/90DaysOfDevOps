1. Which 3 commands save you the most time right now, and why?
The command I used max are ls -ltrh, chown -R (as we need to change permission of every file manually), echo (we can add/append lines to files)


2. How do you check if a service is healthy? List the exact 2–3 commands you’d run first.
To check if service is healthy we run:
    systemctl status <service-name>
    systemctl is-active <service-name>
    journalctl -xe <service-name>

3. How do you safely change ownership and permissions without breaking access? Give one example command.
Ownership and permissions can be changed with chown and chmod. Try to give minimum permissions to others.

4. What will you focus on improving in the next 3 days?
Linux basics and Troubleshooting
More hands-on for linux

