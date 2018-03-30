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

## Commands and explanations

### grep "href=" index.html | cut -d "/" -f 3 | grep "\." | cut -d '"' -f 1 | sort -u
* grep "href=" index.html   (from index.html, extract all lines that contain "href=")
* cut -d "/" -f 3           (split using the front slash delimiter at the 3rd field)
* grep "\."                 (from previous outputs, extract all lines that contain a period)
* cut -d '"' -f 1           (from previous outputs, split using the double quotation mark delimiter at the 1st field)
* sort -u                   (sort unique)

### for url in $(cat list.txt); do host $url; done | grep "has address" | cut -d " " -f 4 | sort -u
*  for url in $(cat list.txt); do host $url; done    (for loop, iterates through each line in list.txt with each line as $url and runs host)
* grep "has address"                                (extract all lines that contain "has address")
* cut -d " " -f 4                                   (split using the space delimiter at the 4th field)
* sort -u                                           (sort unique)
 
