# rock-update

An easier way to update the firmware of your Radxa Rock (Pro).

## Installing

### Installing

To install the tool, run the following command:

    sudo curl -L --output /usr/bin/rock-update https://raw.githubusercontent.com/c0d3z3r0/rock-update/workbench/rock-update && sudo chmod +x /usr/bin/rock-update

## Updating

Then, to update your firmware, just run the following command:

    sudo rock-update

## Activating

After the firmware has been sucessfully updated, you'll need to reboot to load
the new firmware.

## Options

To upgrade/downgrade to a specific firmware revision, specify its Git hash
(from the https://github.com/c0d3z3r0/rock-firmware repository) as follows:

    sudo rock-update fab7796df0cf29f9563b507a59ce5b17d93e0390

### Expert options

There are a number of options for experts you might like to use.  These are all
environment variables you must set if you wish to use them.

#### `UPDATE_SELF`

By default, `rock-update` will attempt to update itself each time it is run.
You can disable this behavior by:

    sudo UPDATE_SELF=0 rock-update

#### `SKIP_BACKUP`

    sudo SKIP_BACKUP=1 rock-update

Avoids making backup of /boot and /lib/modules on first run.

#### `SKIP_REPODELETE`

    sudo SKIP_REPODELETE=1 rock-update

By default the downloaded files (/root/.rock-firmware) are deleted at end of update.
Use this option to keep the files.

#### `ROOT_PATH` and `BOOT_PATH`

    sudo ROOT_PATH=/media/root BOOT_PATH=/media/boot rock-update

Allows you to perform an "offline" update, ie update firmware on an SD card you
are not currently booted from. Useful for installing firmware/kernel to a
non-RPI customised image. Be careful, you must specify both options or neither.
Specifying only one will not work.

#### `BRANCH`

By default, clones the firmware files from the master branch, else uses the files
from the specified branch, eg:

    sudo BRANCH=next rock-update

will use the 'next' branch.

#### Troubleshooting

There are two possible problems related to SSL certificates that may prevent
this tool from working.

-   The time may be set incorrectly on your Rock, which you can fix
    by setting the time using NTP.

        sudo aptitude install ntpdate
        sudo ntpdate -u ntp.ubuntu.com

-   The other possible issue is that you might not have the `ca-certificates`
    package installed, and so GitHub's SSL certificate isn't trusted. If you are
    on Debian, you can resolve this by typing:

        sudo aptitude install ca-certificates
