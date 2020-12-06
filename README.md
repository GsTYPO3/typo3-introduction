# TYPO3 CMS Introduction Package with DDEV Local

Get going quickly with TYPO3 CMS Introduction Package and DDEV Local.

This repository provides a fully setup and ready to use TYPO3 CMS instance
based on the TYPO3 CMS Introduction Package and using DDEV Local.

The installation steps are done on `ddev start` if TYPO3 is not already setup.
Have a look at the [DDEV Local configuration](.ddev/config.yaml), especially
the post-start hooks which are doing the whole magic.

## Quick Start

* Install [Docker](https://docs.docker.com/#docker-products) and [DDEV Local](https://ddev.readthedocs.io/en/stable/)
  (and on Windows also Git). On Windows WSL2 is highly recommended.
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

E.g. to use the Introduction with TYPO3 CMS 9.5 run `ddev typo3 9`.

### Reset the Project ⚠️

⚠️ The procedure will delete the database and all created files. Any changes you
made before will be lost. Be sure you create a proper backup if needed.

To reset the project and start from scratch run `ddev reset`.

## The Magic behind

To simplify the usage of this demo there is a lot of magic implemented which I
try to explain here.

Something still not clear? Please [open an issue](https://github.com/GsTYPO3/introduction/issues/new/choose)
and I will try to explain it.

### Automatic Setup

Kudos here go to the [TYPO-Console](https://github.com/TYPO3-Console) and its
other packages [composer-auto-commands](https://github.com/TYPO3-Console/composer-auto-commands#readme)
and [composer-typo3-auto-install](https://github.com/TYPO3-Console/composer-typo3-auto-install#readme)
which make this possible at all.

`composer-auto-commands` makes the usage of scripts in the `composer.json` known
from the [TYPO3 CMS Base Distribution](https://github.com/TYPO3/TYPO3.CMS.BaseDistribution/blob/10.x/composer.json#L39-L47)
superfluous. In this case the package takes care to run to following commands:

* [install:generatepackagestates](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/InstallGeneratepackagestates.html)
* [install:fixfolderstructure](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/InstallFixfolderstructure.html)
* [database:updateschema](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/DatabaseUpdateschema.html)
* [cache:flush](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/CacheFlush.html)
* [extension:setupactive](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/ExtensionSetupactive.html)

`composer-typo3-auto-install` additionally takes care about the initial setup if
it's not already done, means no LocalConfiguration.php can be found. Important
default values are set with the help of the environment variables set in the
[.env](.env). The admin name and password are currently commented which leads to
the user gets queried during the setup for this values. Also have a look at the
[TYPO3-Console Documentation](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/InstallSetup.html)
to get an idea of the supported variables.

The `.env` file finally is loaded by the help of [Helhum's dotenv-connector](https://github.com/helhum/dotenv-connector#readme)
during the Composer run.

Get more information with the links above and in the [TYPO3-Console Command Reference](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/Index.html).

### DDEV's Custom Commands

DDEV Local has the great possibility to create [custom commands](https://ddev.readthedocs.io/en/stable/users/extend/custom-commands/).
The features to change the TYPO3 Core version and reset the project are implemented
with the help of the custom commands [typo3](.ddev/commands/host/typo3) and
[reset](.ddev/commands/host/reset) which are simple bash scripts.

### DDEV's Configuration

Every DDEV Local user knows the [project configuration](.ddev/config.yaml). In
addition a [docker-composer.*.yaml](.ddev/docker-compose.environment.yaml) file is
provided to add the environment variable `TYPO3_CONTEXT`. Read more about this
feature in the [DDEV Documentation](https://ddev.readthedocs.io/en/stable/users/extend/custom-compose-files/).

## License

This project is released under the terms of the [GNU GENERAL PUBLIC LICENSE](LICENSE).
