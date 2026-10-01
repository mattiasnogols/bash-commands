rm -rf /        # wipes entire filesystem if run with sudo
# Add alias rm='rm -i' to bashrc. Always use specific paths. Never use / as the target.

:(){ :|:& };:   # creates infinite processes. requires a hard reboot
# Limit processes: run ulimit -u 4000 now; add "* hard nproc 4000" to /etc/security/limits.conf

dd if=/dev/zero of=/dev/sda     # writes zeros to your disk. destroys partition table.
# Always verify of= before running dd. Never copy dd commands from the internet.

chmod -R 777 /  # gives every user full access to filesystem.
# Never use / with recursive chmod. Use specific paths only. 755 for directories, 644 for files.

wget -O- url | bash     # downloads script and executes it IMMEDIATELY
# Never pipe curl or wget directly into bash or sh if you have not read first

# Commands you don't understand, especially Hex-encoded, should be avoided.
