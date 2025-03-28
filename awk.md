# AWK

_Status: Published_
_Created: 2023-09-03 03:33:19_
_Tags: cli, awk_

Awk operates on a per-line basis, where it reads input line by line, applies patterns and actions, and then produces output based on those patterns. 
## Extracts disk usage percentage for the root file system
```bash
df -h | awk '$NF == "/" {print "Usage:", $5}'
```
## Lists processes using more than 10% CPU
```bash
ps aux | awk '{if ($3 >= 10) print $0}'
```
## Monitors CPU and memory usage of a process by PID
```bash
top -p PID -n 1 | awk '/PID/{getline; print "CPU:", $9, "MEM:", $10}'
```
## Monitors CPU and memory usage of a specific user
```bash
awk -F':' '{ print "User:", $1, "Home:", $6 }' /etc/passwd
```
## Extracts lines containing "error" from syslog
```bash
awk '/error/ {print $0}' /var/log/syslog
```
## Displays network interfaces and their IP addresses
```bash
ifconfig | awk '/inet addr/{print "Interface:", $1, "IP:", $2}'
```
## Checks if a service is active or not
```bash
systemctl is-active service-name | awk '{print "Service Status:", $0}'
```
## Shows system uptime
```bash
uptime | awk '{print "Uptime:", $3, $4}'
```
## Displays total and used memory
```bash
free -m | awk '/Mem/{print "Total Memory:", $2 "MB", "Used Memory:", $3 "MB"}'
```
## Lists open ports in listening state
```bash
netstat -tuln | awk '/LISTEN/{print "Port:", $4}'
```
## Lists top 5 largest directories
```bash
du -h /path | sort -rh | awk 'NR<=5{print $2, $1}'
```
## Displays CPU model information
```bash
awk -F: '/model name/ {print "CPU Model:", $2}' /proc/cpuinfo
```
## Monitors disk I/O for a specific disk (e.g., sda)
```bash
iostat -x 1 | awk '$1=="sda" {print "Read:", $6 "KB/s, Write:", $7 "KB/s"}'
```
## Lists active network connections and their states
```bash
ss -tuln | awk 'NR>1 {print "Protocol:", $1, "State:", $2, "Local Address:", $4}'
```
## Displays system load averages
```bash
uptime | awk -F'[a-z]:' '{print "Load Average (1/5/15 min):", $2, $3, $4}'
```
## Captures CPU and memory usage snapshot
```bash
top -b -n 1 | awk '/Cpu/{print "CPU Usage:", $2 "%"}; /KiB Mem/{print "Memory Usage:", $8}'
```








