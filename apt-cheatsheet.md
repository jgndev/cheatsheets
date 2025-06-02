# APT Package Manager Cheatsheet

---

## Updating and Upgrading Packages  

- Refresh package index from repositories
```bash
sudo apt update
```

- Upgrade installed packages to latest versions
```bash
sudo apt upgrade
```

- Upgrade with dependency additions/removals
```bash
sudo apt full-upgrade
```
---

## Installing and Removing Packages  

- Install a package (e.g., `nginx`)
```bash
sudo apt install <package>
```

- Install specific version (e.g., `nginx=1.18.0-0ubuntu1`)
```bash
sudo apt install <package>=<version>
```

- Remove package, keep config files
```bash
sudo apt remove <package>
```

- Remove package and config files
```bash
sudo apt purge <package>
```

- Remove unneeded dependencies
```bash
sudo apt autoremove
```
---

## Searching and Querying Packages  

 - Search packages by name/description (e.g., `nginx`)
 ```bash
apt search <keyword>
 ```

- List all installed packages
```bash
apt list --installed
```

- List packages with available upgrades
```bash
apt list --upgradable
```

- Show package details (e.g., `nginx`)
```bash
apt show <package>
```

- List available versions across repositories
```bash
apt madison <package>
```
---

## Managing Repositories

- Add a PPA (e.g., `ppa:nginx/stable`)
```bash
sudo add-apt-repository <ppa>
```

- Remove a PPA
```bash
sudo add-apt-repository --remove <ppa>
```

- Edit `/etc/apt/sources.list`
```bash
sudo apt edit-sources
```

- View repository configuration
```bash
cat /etc/apt/sources.list
```

- List additional repository files
```bash
ls /etc/apt/sources.list.d/
```
---

## Package Maintenance and Cleanup  

- Remove obsolete package files from cache
```bash
sudo apt autoclean
```

- Clear entire package cache
```bash
sudo apt clean
```

- Simulate package removal
```bash
sudo apt remove --dry-run <package>
```

- Fix interrupted installations
```bash
sudo dpkg --configure -a
```

- Resolve broken dependencies
```bash
sudo apt -f install
```
---

## Holding and Pinning Packages  

- Prevent package upgrades (e.g., `nginx`)
```bash
sudo apt hold <package>
```

- Allow held package to upgrade
```bash
sudo apt unhold <package>
```

- Alternative way to hold a package
```bash
echo "<package> install" | sudo dpkg --set-selections
```

- Pin package versions via priority settings
```bash
sudo vim /etc/apt/preferences
```
---

## Advanced Commands  

- Show package dependencies
```bash
apt depends <package>
```

- Show packages depending on the specified package
```bash
apt rdepends <package>
```

- Show installed and available versions, priorities
```bash
apt-cache policy <package>
```

- Install build dependencies for a package
```bash
sudo apt build-dep <package>
```

- Download source code for a package
```bash
sudo apt source <package>
```
