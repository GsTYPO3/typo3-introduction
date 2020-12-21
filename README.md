# TYPO3 CMS Introduction Package with DDEV Local

Get going quickly with TYPO3 CMS Introduction Package and DDEV Local.

This repository provides a full setup and ready to use TYPO3 CMS instance
based on the TYPO3 CMS Introduction Package and using DDEV Local.

The installation steps are done on `ddev start` if TYPO3 is not already setup.
Have a look at the [DDEV Local configuration](.ddev/config.yaml), especially
the post-start hooks which are doing the whole magic.

## Quick Start

* Install [Docker](https://docs.docker.com/#docker-products) and [DDEV Local](https://ddev.readthedocs.io/en/stable/)
  (and on Windows also Git). On Windows, WSL2 is highly recommended.
* Clone or [download](https://github.com/GsTYPO3/introduction/archive/master.zip)
  and extract this repository
* Open a shell, head to the installation folder created before and run `ddev start`

A new browser window opens and displays the login page to the TYPO3 Backend.

Enjoy!

## Windows and Symlinks

To create and show the symlinks correctly on Windows you have to enable the
Developer Mode or start your shell (Git Bash, cmd, PowerShell etc.) elevated
(as adminstrator).

Otherwise the linked folders and files are shown as normal files with some text
information about the target inside. This does not hurt the functionality in
the container, but could be a little bit confusing on the host if you don't know 
about this behavior.

I'm currently working on a patch for DDEV here to simplify this behavior on
Windows. In one of the next releases this will work out-of-the-box without
changing to Developer Mode or using an elevated shell!

## How to use

### Useful Commands

* Start project: `ddev start`
* Stop project: `ddev stop`
* Open frontend: `ddev launch`
* Open backend `ddev launch typo3`

### Reset the Project

⚠️ This procedure will delete the database and all files created. Any changes you
made before will be lost. Be sure to create a proper backup if needed.

To reset the project and start from scratch, run `ddev reset`.

### Change TYPO3 CMS Version

⚠️ This procedure will delete the database and all files created. Any changes you
made before will be lost. Be sure to create a proper backup if needed.

To change the TYPO3 CMS version run `ddev reset [version]`. Valid versions are
10.4 or 9.5 or just their major version part.

E.g., to use the Introduction Package with TYPO3 CMS 9.5 run `ddev reset 9`.

## The Magic Behind the Scenes 

To simplify the usage of this demo there is a lot of magic implemented which I
try to explain here.

If something remains unclear, [open an issue](https://github.com/GsTYPO3/introduction/issues/new/choose)
and I will try to explain it.

### Automatic Setup

Kudos go to the [TYPO3-Console](https://github.com/TYPO3-Console) and its
other packages [composer-auto-commands](https://github.com/TYPO3-Console/composer-auto-commands#readme)
and [composer-typo3-auto-install](https://github.com/TYPO3-Console/composer-typo3-auto-install#readme).

`composer-auto-commands` makes the usage of scripts in the `composer.json` known
from the [TYPO3 CMS Base Distribution](https://github.com/TYPO3/TYPO3.CMS.BaseDistribution/blob/10.x/composer.json#L39-L47)
superfluous. In this case the package takes care to run the following commands:

* [install:generatepackagestates](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/InstallGeneratepackagestates.html)
* [install:fixfolderstructure](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/InstallFixfolderstructure.html)
* [database:updateschema](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/DatabaseUpdateschema.html)
* [cache:flush](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/CacheFlush.html)
* [extension:setupactive](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/ExtensionSetupactive.html)

`composer-typo3-auto-install` additionally takes care of the initial setup in case no 
LocalConfiguration.php can be found. Important default values are set with the help of
the environment variables set in [.env](.env).
The admin name and password are currently commented out, the required user information
is collected via various prompts. Have a look at the [TYPO3-Console Documentation](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/InstallSetup.html)
for supported variables.

Finally, the `.env` file is loaded via the help of [Helhum's dotenv-connector](https://github.com/helhum/dotenv-connector#readme).

More information is available with the links above and in the [TYPO3-Console Command Reference](https://docs.typo3.org/p/helhum/typo3-console/master/en-us/CommandReference/Index.html).

### DDEV's Custom Commands

DDEV Local has the great possibility to create [custom commands](https://ddev.readthedocs.io/en/stable/users/extend/custom-commands/).
The features to change the TYPO3 Core version and reset the project are implemented
with the help of the custom command [reset](.ddev/commands/host/reset) which is a
simple bash script.

### DDEV's Configuration

Additionally to the [project configuration](.ddev/config.yaml) a [docker-composer.\*.yaml](.ddev/docker-compose.environment.yaml) 
file is provided to add the environment variable `TYPO3_CONTEXT`. Read more about this
feature in the [DDEV Documentation](https://ddev.readthedocs.io/en/stable/users/extend/custom-compose-files/).

## License

This project is released under the terms of the [GNU GENERAL PUBLIC LICENSE](LICENSE).
