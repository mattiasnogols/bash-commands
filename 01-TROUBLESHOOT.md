# Server is slow.
# Check load average first, then narrow down (CPU, memory, disk IO, network)
$ uptime
$ top
$ iostat -x 1     # apt install sysstat if not working
$ free -h

# Service not running after reboot.
$ systemctl start nginx           # runs now only
$ systemctl enable --now nginx    # starts and survives reboot

# Disk is full. First find out if filesystem is full. Find the culprit.
$ df -h     # find which filesystem is full
$ sudo du -sh /* 2>/dev/null | sort -rh | head  # find the biggest directories

# Can a process catch or ignore a SIGKILL? No. The kernel handles it directly, so the kill -9 is last resort.
$ kill -15 PID # SIGTERM
$ kill -9 PID  # SIGKILL

# Server failed to boot. See complete boot record.
$ journalctl -b     # current boot full log
$ journalctl -b -1  # previous boot log (use --list-boots to pick another)
