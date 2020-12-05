# TYPO3 CMS Introduction Package with DDEV Local

Get going quickly with TYPO3 CMS Introduction Package and DDEV Local.

This repository provides a fully setup and ready to use TYPO3 CMS instance
based on the TYPO3 CMS Introduction Package and using DDEV Local.

The installation steps are done on `ddev start` if TYPO3 is not already setup.
Have a look at the [DDEV Local configuration](.ddev/config.yaml), especially
the post-start hooks which are doing the whole magic.

## Quick Start

* Install Docker and DDEV Local (and on Windows also Git). On Windows WSL2 is
  highly recommended.
* Clone or [download](https://github.com/GsTYPO3/introduction/archive/master.zip)
  and extract this repository
* Open a shell, head to the installation folder created before and run `ddev start`

A new browser window opens and shows you the login page to TYPO3 Backend.

Enjoy!

## Windows and Symlinks

To create and show the symlinks correctly on Windows you have to enable the
Developer Mode or start your shell (Git Bash, cmd, PowerShell etc.) elevated
(as adminstrator).

Otherwise the linked folders and files are shown as normal files with some text
information about the target inside. This does not hurt the functionality in
the but container but could be a little bit confusing on the host side if you
don't know about this behavior.

## How to use

### Useful Commands

* Start project: `ddev start`
* Stop project: `ddev stop`
* Open frontend: `ddev launch`
* Open backend `ddev launch typo3`

### Change TYPO3 CMS Version ⚠️

⚠️ The procedure will delete the database and all created files. Any changes you
made before will be lost. Be sure you create a proper backup if needed.

To change the TYPO3 CMS version run `ddev typo3 [version]`. Valid version are
10.4 or 9.5 or just their major version part.

E.g. to run the Introduction with TYPO3 CMS 9.5 run `ddev typo3 9`.

### Reset the Project ⚠️

⚠️ The procedure will delete the database and all created files. Any changes you
made before will be lost. Be sure you create a proper backup if needed.

To reset the project and start from scratch run `ddev reset`.

## Links

* [Install Docker](https://docs.docker.com/#docker-products)
* [Install DDEV Local](https://ddev.readthedocs.io/en/stable/)

## License

This project is released under the terms of the [GNU GENERAL PUBLIC LICENSE](LICENSE).
