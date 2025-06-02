# SSH Cheatsheet

---

## Basic Connection

- Connect to remote server
```bash
ssh user@hostname
```

- Connect with specific port
```bash
ssh -p <port> user@hostname
```

- Connect with specific identity file
```bash
ssh -i <private-key> user@hostname
```

- Connect with verbose output
```bash
ssh -v user@hostname
```

- Connect and execute command
```bash
ssh user@hostname 'command'
```

---

## SSH Key Management

- Generate SSH key pair
```bash
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```

- Generate Ed25519 key (recommended)
```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

- Copy public key to remote server
```bash
ssh-copy-id user@hostname
```

- Copy public key with specific key file
```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub user@hostname
```

- Add SSH key to ssh-agent
```bash
ssh-add ~/.ssh/id_rsa
```

- List keys in ssh-agent
```bash
ssh-add -l
```

- Remove all keys from ssh-agent
```bash
ssh-add -D
```

---

## File Transfer

- Copy file to remote server
```bash
scp local-file user@hostname:/remote/path/
```

- Copy file from remote server
```bash
scp user@hostname:/remote/file /local/path/
```

- Copy directory recursively
```bash
scp -r local-directory user@hostname:/remote/path/
```

- Copy with specific port
```bash
scp -P <port> local-file user@hostname:/remote/path/
```

- Sync directories with rsync
```bash
rsync -avz local-directory/ user@hostname:/remote/path/
```

- Sync with delete (mirror)
```bash
rsync -avz --delete local-directory/ user@hostname:/remote/path/
```

---

## Port Forwarding and Tunneling

- Local port forwarding
```bash
ssh -L <local-port>:<remote-host>:<remote-port> user@hostname
```

- Remote port forwarding
```bash
ssh -R <remote-port>:<local-host>:<local-port> user@hostname
```

- Dynamic port forwarding (SOCKS proxy)
```bash
ssh -D <local-port> user@hostname
```

- Background tunnel
```bash
ssh -f -N -L <local-port>:<remote-host>:<remote-port> user@hostname
```

- Keep tunnel alive
```bash
ssh -o ServerAliveInterval=60 -o ServerAliveCountMax=3 user@hostname
```

---

## SSH Configuration

- Edit SSH config file
```bash
vim ~/.ssh/config
```

- Example SSH config entry
```
Host myserver
    HostName example.com
    User username
    Port 2222
    IdentityFile ~/.ssh/id_rsa
    ServerAliveInterval 60
```

- Connect using config alias
```bash
ssh myserver
```

- Test SSH config
```bash
ssh -T git@github.com
```

---

## Security and Authentication

- Disable password authentication (server-side)
```bash
# In /etc/ssh/sshd_config
PasswordAuthentication no
PubkeyAuthentication yes
```

- Change SSH key passphrase
```bash
ssh-keygen -p -f ~/.ssh/id_rsa
```

- View SSH key fingerprint
```bash
ssh-keygen -lf ~/.ssh/id_rsa.pub
```

- Connect with specific cipher
```bash
ssh -c aes256-ctr user@hostname
```

- Disable host key checking (not recommended for production)
```bash
ssh -o StrictHostKeyChecking=no user@hostname
```

---

## Session Management

- Run command in background
```bash
ssh user@hostname 'nohup command &'
```

- Keep session alive after disconnect
```bash
ssh user@hostname
screen -S session-name
# or
tmux new-session -s session-name
```

- Reconnect to screen session
```bash
ssh user@hostname
screen -r session-name
```

- Reconnect to tmux session
```bash
ssh user@hostname
tmux attach-session -t session-name
```

---

## Troubleshooting

- Debug connection issues
```bash
ssh -vvv user@hostname
```

- Check SSH service status
```bash
systemctl status ssh
# or
service ssh status
```

- View SSH logs
```bash
tail -f /var/log/auth.log
# or
journalctl -u ssh -f
```

- Test specific SSH version
```bash
ssh -o Protocol=2 user@hostname
```

- Escape sequences (when connected)
```bash
~.  # Disconnect
~^Z # Background SSH
~#  # List forwarded connections
~?  # Help
```

---

## Common Use Cases

- Jump host / bastion server
```bash
ssh -J jump-host target-host
```

- Multiple jump hosts
```bash
ssh -J host1,host2 target-host
```

- X11 forwarding for GUI applications
```bash
ssh -X user@hostname
```

- Compress data transfer
```bash
ssh -C user@hostname
```

- Run local script on remote server
```bash
ssh user@hostname 'bash -s' < local-script.sh
```

- Mount remote filesystem with SSHFS
```bash
sshfs user@hostname:/remote/path /local/mount/point
```

---

## Quick File Operations

- Edit remote file directly
```bash
ssh user@hostname 'vim /path/to/file'
```

- Create remote directory
```bash
ssh user@hostname 'mkdir -p /path/to/directory'
```

- Check disk space on remote server
```bash
ssh user@hostname 'df -h'
```

- View remote file content
```bash
ssh user@hostname 'cat /path/to/file'
```

- Tail remote log file
```bash
ssh user@hostname 'tail -f /var/log/application.log'
``` 