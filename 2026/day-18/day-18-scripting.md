Task 1: Basic Functions

    Create functions.sh with:
        A function greet that takes a name as argument and prints Hello, <name>!
        A function add that takes two numbers and prints their sum
        Call both functions from the script
        
vi functions.sh
karishma@MyPc:~/practice$ chmod +x functions.sh 
karishma@MyPc:~/practice$ ./functions.sh 
Hello, Alice!
8

*********************************************************

Task 2: Functions with Return Values

    Create disk_check.sh with:
        A function check_disk that checks disk usage of / using df -h
        A function check_memory that checks free memory using free -h
        A main section that calls both and prints the results

vi disk_check.sh
karishma@MyPc:~/practice$ chmod +x disk_check.sh 
karishma@MyPc:~/practice$ ./disk_check.sh 
Disk Usage:
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n1p5  234G   39G  183G  18% /

Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:            10Gi       4.0Gi       2.8Gi       1.0Gi       4.9Gi       6.9Gi
Swap:          4.0Gi          0B       4.0Gi

**********************************************************************

Task 3: Strict Mode — set -euo pipefail

    Create strict_demo.sh with set -euo pipefail at the top
    Try using an undefined variable — what happens with set -u?
    Try a command that fails — what happens with set -e?
    Try a piped command where one part fails — what happens with set -o pipefail?

Document: What does each flag do?

    set -e →
    set -u →
    set -o pipefail →
    
./strict_demo.sh 
1. Testing set -u...
2. Testing set -e...
3. Testing set -o pipefail...

All tests completed.

Test 1: Undefined variable

./strict_demo.sh 
1. Testing set -u...
./strict_demo.sh: line 6: UNDEFINED_VAR: unbound variable

Test 2: failing command

 ./strict_demo.sh 
1. Testing set -u...
2. Testing set -e...

Test 3: Failing command

./strict_demo.sh 
1. Testing set -u...
2. Testing set -e...
3. Testing set -o pipefail...
Pipeline

**************************************************************************

Task 4: Local Variables

    Create local_demo.sh with:
        A function that uses local keyword for variables
        Show that local variables don't leak outside the function
        Compare with a function that uses regular variables

./local_demo.sh 
=== Local variable demo ===
Inside local_demo:
Name: Alice
Age: 25

Outside local_demo:
Name: not set
Age: not set

=== Regular variable demo ===
Inside regular_demo:
Name: Bob
Age: 30

Outside regular_demo:
Name: Bob
Age: 30


**********************************************************

Task 5: Build a Script — System Info Reporter

Create system_info.sh that uses functions for everything:

    A function to print hostname and OS info
    A function to print uptime
    A function to print disk usage (top 5 by size)
    A function to print memory usage
    A function to print top 5 CPU-consuming processes
    A main function that calls all of the above with section headers
    Use set -euo pipefail at the top

Output should look clean and readable.

./system_info.sh 
========================================
           SYSTEM INFORMATION
========================================

-------- Hostname & OS --------
Hostname: MyPc
OS: Ubuntu 26.04 LTS

-------- Uptime --------
Uptime: up 47 minutes

-------- Disk Usage --------
Top 5 Filesystems by Usage:
efivarfs        374K  272K   98K  74% /sys/firmware/efi/efivars
/dev/nvme0n1p1  196M   38M  159M  20% /boot/efi
/dev/nvme0n1p5  234G   39G  183G  18% /
tmpfs           5.5G  5.4M  5.5G   1% /dev/shm
tmpfs           5.5G   16K  5.5G   1% /tmp

-------- Memory Usage --------
               total        used        free      shared  buff/cache   available
Mem:            10Gi       4.1Gi       2.7Gi       1.0Gi       4.9Gi       6.9Gi
Swap:          4.0Gi          0B       4.0Gi

-------- Top 5 CPU Processes --------
Top 5 CPU-Consuming Processes:
    PID USER     %CPU %MEM COMMAND
   4229 karishma 13.1  6.5 firefox
   1863 karishma 11.3  2.6 gnome-shell
   7578 karishma  6.3  4.3 Isolated Web Co
   6266 karishma  1.4  1.3 gnome-text-edit
   5704 karishma  1.4  1.2 ptyxis

========================================
              END
========================================







