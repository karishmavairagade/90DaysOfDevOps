Task 1: For Loop

    Create for_loop.sh that:
        Loops through a list of 5 fruits and prints each one
    Create count.sh that:
        Prints numbers 1 to 10 using a for loop

vi for_loop.sh
karishma@MyPc:~/practice$ chmod +x for_loop.sh 
karishma@MyPc:~/practice$ ./for_loop.sh 
Apple
Banana
Mango
Orange
Grapes

vi count.sh
karishma@MyPc:~/practice$ chmod +x c
check_number.sh  check.sh         count.sh         
karishma@MyPc:~/practice$ chmod +x count.sh 
karishma@MyPc:~/practice$ ./count.sh 
1
2
3
4
5
6
7
8
9
10


***********************************************************

Task 2: While Loop

    Create countdown.sh that:
        Takes a number from the user
        Counts down to 0 using a while loop
        Prints "Done!" at the end

arishma@MyPc:~/practice$ vi countdown.sh
karishma@MyPc:~/practice$ chmod +x countdown.sh 
karishma@MyPc:~/practice$ ./countdown.sh 
Enter a number: 3
3
2
1
0
Done!
karishma@MyPc:~/practice$ ./countdown.sh 
Enter a number: 8
8
7
6
5
4
3
2
1
0
Done!

**************************************************************************

Task 3: Command-Line Arguments

 A}   Create greet.sh that:
        Accepts a name as $1
        Prints Hello, <name>!
        If no argument is passed, prints "Usage: ./greet.sh "
        
        
        
        vi greet.sh
karishma@MyPc:~/practice$ chmod +x greet.sh
karishma@MyPc:~/practice$ ./greet.sh 
Usage: ./greet.sh <name>
karishma@MyPc:~/practice$ cat greet.sh 
#!/bin/bash

if [ -z "$1" ]; then
    echo 'Usage: ./greet.sh <name>'
else
    echo "Hello, $1!"
fi
karishma@MyPc:~/practice$ 


  B}  Create args_demo.sh that:
        Prints total number of arguments ($#)
        Prints all arguments ($@)
        Prints the script name ($0)

cat args_demo 
#!/bin/bash

echo "Total number of arguments: $#"
echo "All arguments: $@"
echo "Script name: $0"
karishma@MyPc:~/practice$ chmod +x args_demo 
karishma@MyPc:~/practice$ ./args_demo 
Total number of arguments: 0
All arguments: 
Script name: ./args_demo
karishma@MyPc:~/practice$ 


**************************************************************

Task 4: Install Packages via Script

    Create install_packages.sh that:
        Defines a list of packages: nginx, curl, wget
        Loops through the list
        Checks if each package is installed (use dpkg -s or rpm -q)
        Installs it if missing, skips if already present
        Prints status for each package

    Run as root: sudo -i or sudo su

vi install_package.sh
karishma@MyPc:~/practice$ chmod +x install_package.sh 
karishma@MyPc:~/practice$ ./install_package.sh 
Checking nginx...
nginx is not installed. Installing...
Reading package lists... Done
E: Could not open lock file /var/lib/apt/lists/lock - open (13: Permission denied)
E: Unable to lock directory /var/lib/apt/lists/
W: Problem unlinking the file /var/cache/apt/pkgcache.bin - RemoveCaches (13: Permission denied)
W: Problem unlinking the file /var/cache/apt/srcpkgcache.bin - RemoveCaches (13: Permission denied)
E: Could not open lock file /var/lib/dpkg/lock-frontend - open (13: Permission denied)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), are you root?
Failed to install nginx.
-------------------------
Checking curl...
curl is already installed. Skipping.
-------------------------
Checking wget...
wget is already installed. Skipping.

***********************************************************

Task 5: Error Handling

  A}  Create safe_script.sh that:
        Uses set -e at the top (exit on error)
        Tries to create a directory /tmp/devops-test
        Tries to navigate into it
        Creates a file inside
        Uses || operator to print an error if any step fails

Example:

mkdir /tmp/devops-test || echo "Directory already exists"

vi safe_script.sh
karishma@MyPc:~/practice$ chmod +x safe_script.sh 
karishma@MyPc:~/practice$ ./safe_script.sh 
Script completed successfully.
karishma@MyPc:~/practice$ cd /tmp/devops-test/
karishma@MyPc:/tmp/devops-test$ pwd
/tmp/devops-test

./safe_script.sh 
mkdir: /tmp/devops-test: File exists
Directory already exists
Script completed successfully.
karishma@MyPc:~/practice$ 


  B}  Modify your install_packages.sh to check if the script is being run as root — exit with a message if not.

vi safe_script.sh 
karishma@MyPc:~/practice$ ./safe_script.sh 
Error: Please run this script as root.
Example: sudo ./install_packages.sh
karishma@MyPc:~/practice$ sudo ./safe_script.sh 
[sudo: authenticate] Password:     
Checking nginx...
nginx is not installed. Installing...
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Solving dependencies... Done
The following additional packages will be installed:
  nginx-common
Suggested packages:
  fcgiwrap nginx-doc
The following NEW packages will be installed:
  nginx nginx-common
0 upgraded, 2 newly installed, 0 to remove and 105 not upgraded.
Need to get 655 kB of archives.
After this operation, 1,860 kB of additional disk space will be used.
Get:1 http://in.archive.ubuntu.com/ubuntu resolute-updates/main amd64 nginx-common all 1.28.3-2ubuntu1.8 [37.7 kB]
Get:2 http://in.archive.ubuntu.com/ubuntu resolute-updates/main amd64 nginx amd64 1.28.3-2ubuntu1.8 [617 kB]
Fetched 655 kB in 2s (390 kB/s)
Preconfiguring packages ...
Selecting previously unselected package nginx-common.
(Reading database… 259901 files and directories currently installed.)
Preparing to unpack …/nginx-common_1.28.3-2ubuntu1.8_all.deb…
Unpacking nginx-common (1.28.3-2ubuntu1.8)…
Selecting previously unselected package nginx.
Preparing to unpack …/nginx_1.28.3-2ubuntu1.8_amd64.deb…
Unpacking nginx (1.28.3-2ubuntu1.8)…
Setting up nginx-common (1.28.3-2ubuntu1.8)…
Created symlink '/etc/systemd/system/multi-user.target.wants/nginx.service' → '/usr/lib/systemd/system/nginx.service'.
Setting up nginx (1.28.3-2ubuntu1.8)…
 * Upgrading binary nginx                                                                                                                                                      [ OK ] 
Processing triggers for man-db (2.13.1-1build1)…
Processing triggers for ufw (0.36.2-9build1)…
nginx installed successfully.
-------------------------
Checking curl...
curl is already installed. Skipping.
-------------------------
Checking wget...
wget is already installed. Skipping.


