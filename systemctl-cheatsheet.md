---
id: 2
date: 2025-05-02T00:00:00Z
title: Systemctl Cheatsheet
author: Jeremy Novak
summary: Cheatsheet for the systemctl command
slug: systemctl-cheatsheet
tags:
  - systemctl
published: true
---

# Systemctl Cheatsheet

---

## Basic Service Management

- Start a service
```bash
sudo systemctl start <service-name>
```

- Stop a service
```bash
sudo systemctl stop <service-name>
```

- Restart a service
```bash
sudo systemctl restart <service-name>
```

- Reload service configuration
```bash
sudo systemctl reload <service-name>
```

- Restart or reload if running
```bash
sudo systemctl reload-or-restart <service-name>
```

- Show service status
```bash
systemctl status <service-name>
```

- Check if service is active
```bash
systemctl is-active <service-name>
```

- Check if service is enabled
```bash
systemctl is-enabled <service-name>
```

---

## Service Configuration

- Enable service at boot
```bash
sudo systemctl enable <service-name>
```

- Disable service at boot
```bash
sudo systemctl disable <service-name>
```

- Enable and start service
```bash
sudo systemctl enable --now <service-name>
```

- Disable and stop service
```bash
sudo systemctl disable --now <service-name>
```

- Mask service (prevent starting)
```bash
sudo systemctl mask <service-name>
```

- Unmask service
```bash
sudo systemctl unmask <service-name>
```

---

## Service Information

- List all services
```bash
systemctl list-units --type=service
```

- List all enabled services
```bash
systemctl list-unit-files --type=service --state=enabled
```

- List all disabled services
```bash
systemctl list-unit-files --type=service --state=disabled
```

- List failed services
```bash
systemctl list-units --type=service --state=failed
```

- List all running services
```bash
systemctl list-units --type=service --state=running
```

- Show service dependencies
```bash
systemctl list-dependencies <service-name>
```

- Show reverse dependencies
```bash
systemctl list-dependencies --reverse <service-name>
```

---

## System State Management

- Reboot system
```bash
sudo systemctl reboot
```

- Shutdown system
```bash
sudo systemctl poweroff
```

- Suspend system
```bash
sudo systemctl suspend
```

- Hibernate system
```bash
sudo systemctl hibernate
```

- Switch to rescue mode
```bash
sudo systemctl rescue
```

- Switch to emergency mode
```bash
sudo systemctl emergency
```

- Get default target
```bash
systemctl get-default
```

- Set default target
```bash
sudo systemctl set-default <target>
```

---

## Target Management

- List available targets
```bash
systemctl list-unit-files --type=target
```

- Switch to target
```bash
sudo systemctl isolate <target>
```

- Common targets
```bash
# Multi-user (CLI)
sudo systemctl isolate multi-user.target

# Graphical (GUI)
sudo systemctl isolate graphical.target

# Rescue mode
sudo systemctl isolate rescue.target
```

---

## Logs and Journaling

- View service logs
```bash
journalctl -u <service-name>
```

- Follow service logs
```bash
journalctl -u <service-name> -f
```

- View logs since boot
```bash
journalctl -u <service-name> -b
```

- View logs for last hour
```bash
journalctl -u <service-name> --since "1 hour ago"
```

- View logs with priority
```bash
journalctl -u <service-name> -p err
```

- View system boot logs
```bash
journalctl -b
```

- View kernel messages
```bash
journalctl -k
```

- Clear journal logs
```bash
sudo journalctl --vacuum-time=2weeks
sudo journalctl --vacuum-size=100M
```

---

## Unit File Management

- Show unit file content
```bash
systemctl cat <service-name>
```

- Edit unit file
```bash
sudo systemctl edit <service-name>
```

- Edit full unit file
```bash
sudo systemctl edit --full <service-name>
```

- Reload systemd configuration
```bash
sudo systemctl daemon-reload
```

- Reset failed services
```bash
sudo systemctl reset-failed
```

- Reset specific failed service
```bash
sudo systemctl reset-failed <service-name>
```

---

## Custom Service Creation

- Example service unit file (/etc/systemd/system/myapp.service)
```ini
[Unit]
Description=My Application
After=network.target

[Service]
Type=simple
User=myuser
WorkingDirectory=/opt/myapp
ExecStart=/opt/myapp/bin/myapp
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

- Create and enable custom service
```bash
sudo cp myapp.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable myapp.service
sudo systemctl start myapp.service
```

---

## Timers (Systemd Cron)

- List active timers
```bash
systemctl list-timers
```

- Example timer unit file (mytask.timer)
```ini
[Unit]
Description=Run mytask every 5 minutes

[Timer]
OnCalendar=*:0/5
Persistent=true

[Install]
WantedBy=timers.target
```

- Example service for timer (mytask.service)
```ini
[Unit]
Description=My scheduled task

[Service]
Type=oneshot
ExecStart=/usr/local/bin/mytask.sh
```

- Enable and start timer
```bash
sudo systemctl enable mytask.timer
sudo systemctl start mytask.timer
```

---

## Environment and Variables

- Show service environment
```bash
systemctl show-environment
```

- Set environment variable
```bash
sudo systemctl set-environment VAR=value
```

- Unset environment variable
```bash
sudo systemctl unset-environment VAR
```

- Import environment file
```bash
sudo systemctl import-environment
```

---

## Advanced Operations

- Kill service processes
```bash
sudo systemctl kill <service-name>
```

- Kill with specific signal
```bash
sudo systemctl kill -s SIGUSR1 <service-name>
```

- Show service properties
```bash
systemctl show <service-name>
```

- Show specific property
```bash
systemctl show <service-name> -p MainPID
```

- Monitor service changes
```bash
systemctl monitor
```

- Verify service configuration
```bash
systemd-analyze verify <service-name>
```

---

## Troubleshooting

- Check system state
```bash
systemctl status
```

- List failed units
```bash
systemctl --failed
```

- Analyze boot time
```bash
systemd-analyze
```

- Show critical chain
```bash
systemd-analyze critical-chain
```

- Show service startup time
```bash
systemd-analyze blame
```

- Check configuration issues
```bash
systemd-analyze verify
```

- Check if system is running
```bash
systemctl is-system-running
```

---

## Common Service Operations

- Web servers
```bash
sudo systemctl restart nginx
sudo systemctl restart apache2
sudo systemctl reload nginx
```

- Databases
```bash
sudo systemctl start mysql
sudo systemctl start postgresql
sudo systemctl status redis
```

- System services
```bash
sudo systemctl restart ssh
sudo systemctl status network
sudo systemctl restart systemd-resolved
```

- Check network service
```bash
systemctl status NetworkManager
systemctl status systemd-networkd
```

---

## Useful Patterns

- Restart service if config changed
```bash
sudo systemctl reload-or-restart nginx
```

- Check service before restart
```bash
nginx -t && sudo systemctl reload nginx
```

- Enable multiple services
```bash
sudo systemctl enable nginx mysql redis
```

- Check multiple service status
```bash
systemctl status nginx mysql redis
```

- Filter services by pattern
```bash
systemctl list-units --type=service | grep -i apache
```

- Show services using port
```bash
ss -tulpn | grep :80
systemctl status $(systemctl list-units --type=service --state=running | grep -i apache | awk '{print $1}')
```

---

## Service Dependencies

- Show what services depend on target
```bash
systemctl list-dependencies --reverse multi-user.target
```

- Show what target depends on
```bash
systemctl list-dependencies multi-user.target
```

- Check service conflicts
```bash
systemctl show <service-name> -p Conflicts
```

- Check service requirements
```bash
systemctl show <service-name> -p Requires
``` 