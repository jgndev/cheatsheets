# Homebrew Cheatsheet

Essential commands that should meet most of your needs as a [brew.sh](https://brew.sh) user.

| **Command**                     | **Description**                                              |
|---------------------------------|--------------------------------------------------------------|
| `brew install <package>`        | Installs a package (e.g., `brew install git`).               |
| `brew uninstall <package>`      | Removes a package.                                           |
| `brew update`                   | Updates Homebrew and formulae to the latest version.         |
| `brew upgrade`                  | Upgrades all installed packages to their latest versions.    |
| `brew upgrade <package>`        | Upgrades a specific package.                                 |
| `brew list`                     | Lists all installed packages.                                |
| `brew search <text>`            | Searches for packages matching the text.                     |
| `brew info <package>`           | Displays information about a package.                        |
| `brew doctor`                   | Checks the system for potential issues with Homebrew.        |
| `brew cleanup`                  | Removes old versions of packages and cleans cache.           |
| `brew tap <user/repo>`          | Adds a new tap (repository) for additional formulae.         |
| `brew untap <user/repo>`        | Removes a tap.                                               |
| `brew services list`            | Lists services managed by Homebrew.                          |
| `brew services start <service>` | Starts a service.                                            |
| `brew services stop <service>`  | Stops a service.                                             |
| `brew outdated`                 | Shows outdated packages that can be upgraded.                |
| `brew pin <package>`            | Pins a package to prevent upgrades.                          |
| `brew unpin <package>`          | Unpins a package to allow upgrades.                          |

For more details, visit [docs.brew.sh](https://docs.brew.sh).