---
id: 19
date: 2025-07-14T00:00:00Z
title: "Pacman Package Manager Cheatsheet"
author: "Jeremy Novak"
summary: "Cheatsheet for the Pacman Package Manager on Arch Linux"
slug: pacman-cheatsheet
tags:
  - pacman
  - arch
  - linux
published: true
---

# Pacman Package Manager Cheatsheet

---

## Updating and Synchronizing Packages

- Sync package database
```bash
sudo pacman -Sy
```

- Update system (sync database and upgrade packages)
```bash
sudo pacman -Syu
```

- Force refresh package database
```bash
sudo pacman -Syy
```

- Update system with database refresh
```bash
sudo pacman -Syyu
```
---

## Installing and Removing Packages

- Install a package (e.g., `firefox`)
```bash
sudo pacman -S <package>
```

- Install package without confirmation
```bash
sudo pacman -S --noconfirm <package>
```

- Install from file or URL
```bash
sudo pacman -U <path/to/package.pkg.tar.zst>
```

- Remove package only
```bash
sudo pacman -R <package>
```

- Remove package and dependencies
```bash
sudo pacman -Rs <package>
```

- Remove package, dependencies, and config files
```bash
sudo pacman -Rns <package>
```

- Remove orphaned packages
```bash
sudo pacman -Rns $(pacman -Qdtq)
```
---

## Searching and Querying Packages

- Search for packages in repositories
```bash
pacman -Ss <keyword>
```

- Search installed packages
```bash
pacman -Qs <keyword>
```

- Display package information (repository)
```bash
pacman -Si <package>
```

- Display installed package information
```bash
pacman -Qi <package>
```

- List all installed packages
```bash
pacman -Q
```

- List explicitly installed packages
```bash
pacman -Qe
```

- List orphaned packages
```bash
pacman -Qdt
```

- List files installed by package
```bash
pacman -Ql <package>
```

- Find which package owns a file
```bash
pacman -Qo <file>
```
---

## Package Cache Management

- Remove uninstalled packages from cache
```bash
sudo pacman -Sc
```

- Clear entire package cache
```bash
sudo pacman -Scc
```

- Download package without installing
```bash
sudo pacman -Sw <package>
```

- Verify package integrity
```bash
pacman -Qk <package>
```

- Check all packages for file issues
```bash
sudo pacman -Qkk
```
---

## Managing Package Groups

- List all package groups
```bash
pacman -Sg
```

- List packages in a group
```bash
pacman -Sg <group>
```

- Install entire group
```bash
sudo pacman -S <group>
```
---

## Database and Mirror Management

- Refresh all package databases
```bash
sudo pacman -Syy
```

- Optimize pacman database
```bash
sudo pacman-optimize
```

- Clean package database
```bash
sudo pacman -Sc
```

- Update mirrorlist (requires reflector)
```bash
sudo reflector --latest 20 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```
---

## Advanced Operations

- List packages by size
```bash
pacman -Qi | awk '/^Name/{name=$3} /^Installed Size/{print $4$5, name}' | sort -h
```

- Show dependency tree
```bash
pactree <package>
```

- Show reverse dependencies
```bash
pactree -r <package>
```

- List files not owned by any package
```bash
sudo pacman -Qkk 2>&1 | grep "No such file"
```

- Reinstall all packages
```bash
sudo pacman -Qqn | pacman -S -
```

- Mark package as explicitly installed
```bash
sudo pacman -D --asexplicit <package>
```

- Mark package as dependency
```bash
sudo pacman -D --asdeps <package>
```
---

## Configuration

- Main configuration file
```bash
sudo vim /etc/pacman.conf
```

- Mirror list
```bash
sudo vim /etc/pacman.d/mirrorlist
```

- Enable color output
```bash
# Uncomment "Color" in /etc/pacman.conf
```

- Enable parallel downloads
```bash
# Add "ParallelDownloads = 5" to /etc/pacman.conf
```
---

## Troubleshooting

- Fix broken packages
```bash
sudo pacman -S --needed $(pacman -Qnq)
```

- Unlock pacman database
```bash
sudo rm /var/lib/pacman/db.lck
```

- Verify all packages
```bash
sudo pacman -Qkk
```

- Force package installation
```bash
sudo pacman -S --overwrite '*' <package>
```

- Skip dependency checks (dangerous)
```bash
sudo pacman -Sd <package>
```
