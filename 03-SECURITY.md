# Who is on your server right now?
$ w             # who is logged in and what they run
$ last -n 20    # recent logins and source IPs
$ sudo lastb    # failed login attempts

# What is running that should not be?
$ ps auxf       # full process tree
$ top           # CPU spikes reveal miners

# Is data leaving your server?
$ sudo ss -tulpn                   # open ports and owning process
$ sudo ss -antp | grep ESTABLISHED # active outbound connections

# Where did they hide to survive a reboot?

$ for u in $(cut -f1 -d: /etc/passwd);
do sudo crontab -u $u -l 2>/dev/null; done    # check every user crontab
$ systemctl list-units --type=service         # look for rogue services

# What were they trying to steal? SSH keys, cloud credentials and API tokens are the most common targets (can go further beyond this host)
$ sudo find / -name "id_rsa" -o \
-name "*.pem" -o \
-name "credentials" 2>/dev/null

# What do the logs actually show? Attackers clear bash history. Auth logs can still show you the timeline.
$ sudo grep "Accepted" /var/log/auth.log # successful logins
$ sudo grep "Failed" /var/log/auth.log # failed attempts before success
$ sudo ausearch -m USER_CMD --start today # every command run today; apt install auditd if missing

# What changed recently? Files touched anywhere or under system paths are red flags.
$ sudo find / -mtime -1 -type f 2>/dev/null # files touched in last 24 hours
$ sudo find /etc /usr/bin /usr/sbin -mtime -7 -type f 2>/dev/null # system files changed this week
