$ sudo apt update
$ sudo apt install fastfetch -y
$ fastfetch     # see your OS, kernel, CPU, RAM in one output

# Patch everything first
$ sudo apt upgrade -y
$ sudo apt install unattended-upgrades -y && sudo dpkg-reconfigure -plow unattended-upgrades   # downloads and applies security patches automatically

# Lock the front door: SSH keys and sshd hardening are in 02-HARDEN.md

# Build the Walls
$ sudo ufw allow OpenSSH
$ sudo ufw enable
$ sudo ufw status verbose

# Add the guards
$ sudo apt install fail2ban -y && sudo systemctl enable --now fail2ban

# Make files immutable so no one can modify
$ sudo chattr +i /etc/passwd
$ sudo chattr +i /etc/shadow
$ sudo chattr +i /etc/group
$ sudo chattr +i /etc/sudoers

# See exposed ports
$ sudo ss -tulnp

# Kernel (sysctl) hardening
# /etc/sysctl.d/99-hardening.conf
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.all.send_redirects = 0
net.ipv4.conf.all.rp_filter = 1
net.ipv4.icmp_echo_ignore_broadcasts = 1
$ sudo sysctl --system    # apply the sysctl file

# lynis audit system
$ sudo apt install lynis -y
$ sudo lynis audit system
