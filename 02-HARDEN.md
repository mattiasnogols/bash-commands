# Ed25519 for all new keys.
$ ssh-keygen -t ed25519     # generate the key pair
$ ssh-copy-id user@server   # deploy to the server

# Put your hardening in a drop-in file instead of editing the main config.
# Files load in order and the first value wins, so keep the 99- prefix.
/etc/ssh/sshd_config.d/99-hardening.conf    # create this file
PermitRootLogin no
PasswordAuthentication no
MaxAuthTries 3
AllowUsers yourusername    # must be an existing user, or you lose SSH access
AllowGroups sshusers       # run first: sudo groupadd sshusers && sudo usermod -aG sshusers yourusername
LoginGraceTime 30

# An idle privileged session should be disconnected
ClientAliveInterval 300 # disconnects idle sessions after 10 minutes
ClientAliveCountMax 2

# Always validate config before reloading sshd.
$ sudo sshd -t        # test config, open a second terminal, test before closing
$ sudo systemctl reload ssh

# Check your current effective SSH settings with one command.
$ sudo sshd -T | grep passwordauth   # should return no
$ sudo sshd -T | grep permitroot     # should return no

# Verbose logging for SSH
LogLevel VERBOSE            # add to the 99- drop-in file
$ journalctl -u ssh -f      # watch SSH logs live
