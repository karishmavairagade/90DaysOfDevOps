PROCESS MANAGEMENT COMMANDS

pidof - gives process id of commands
                eg: pidof systemd

top - shows the linux processes and their details
         eg: top

ps - reports snapshots of given process

kill - kills the running process and -f use for forcing
     eg: kill/ kill -9 1106

htop - same as top just gives output in gui

vmstats - gives virtual memory stastics

uptime - gives system uptime

time - run programs and summarize system resource usage

pgrep - gives the process id of the mentioned process
       eg : pgrep systemd

nohup - used to run process in background even after shell is terminated

jobs - jobs running in current shell session

screen - creates a virtual terminal session that can be attached and reattached at any time.

watch - runs any command repeatedly and displays the output in a full-screen view.




FILESYSTEM COMMANDS

pwd - present working directory

cd - change directory

mkdir - make directory

ls -list files can be combined with -l for long list and lrth

cp - copy the file from 1 location to other

mv - move contents of file to other its also used for renaming

tree - shows the filesystem as tree structure

cat - display contents of file

less - shows contents one screen at a time

echo - add/print contents to file
     eg: echo "Hello" > abc.txt (add content) >> (append)

head - shows top 10 files with -n we can mention number of files we want to see

tail- shows bottom 10 files with -n we can mention number of files we want to see

history- shows history



NETWORK TROUBLESHOOTING COMMANDS

ping - checks connectivity

ip a/ ifconfig - shows ip and ethernet details

traceroute - traces hop by hop from source to destination

netstat - display a list of all active TCP connections

show ip route- shows the details the ip hops to
    eg: show ip route 192.168.0.123

nslookup - queries the dns to obtain mapping info between domain name and IP address
       eg: nslookup google.com

dig - querying DNS (Domain Name System) servers troubleshooting network-relatd issues.

curl- used to transfer data to or from a server using various protocols

wget- downloading files from the web using HTTP, HTTPS, and FTP protocols.


