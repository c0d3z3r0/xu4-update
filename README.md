# xu4-update

An easier way to update the firmware of your Odroid-XU4.

## Installing

To install the tool, run the following command:

    sudo curl -L --output /usr/bin/xu4-update https://raw.githubusercontent.com/c0d3z3r0/xu4-update/master/xu4-update && sudo chmod +x /usr/bin/xu4-update

## Updating

Then, to update your firmware, just run the following command:

    sudo xu4-update

## Activating

After the firmware has been sucessfully updated, you'll need to reboot to load
the new firmware.

## Options

To upgrade/downgrade to a specific firmware revision, specify its Git hash
(from the https://github.com/c0d3z3r0/odroid-xu4 repository) as follows:

    sudo xu4-update fab7796df0cf29f9563b507a59ce5b17d93e0390

### Expert options

There are a number of options for experts you might like to use.  These are all
environment variables you must set if you wish to use them.

#### `UPDATE_SELF`

By default, `xu4-update` will attempt to update itself each time it is run.
You can disable this behavior by:

    sudo UPDATE_SELF=0 xu4-update

#### `SKIP_BACKUP`

    sudo SKIP_BACKUP=1 xu4-update

Avoids making backup of /boot and /lib/modules on first run.

#### `SKIP_REPODELETE`

    sudo SKIP_REPODELETE=1 xu4-update

By default the downloaded files (/root/.xu4-firmware) are deleted at end of update.
Use this option to keep the files.

#### `ROOT_PATH` and `BOOT_PATH`

    sudo ROOT_PATH=/media/root BOOT_PATH=/media/boot xu4-update

Allows you to perform an "offline" update, ie update firmware on an SD card you
are not currently booted from. Useful for installing firmware/kernel to a
non-RPI customised image. Be careful, you must specify both options or neither.
Specifying only one will not work.

#### `BRANCH`

By default, clones the firmware files from the master branch, else uses the files
from the specified branch, eg:

    sudo BRANCH=next xu4-update

will use the 'next' branch.

#### Troubleshooting

There are two possible problems related to SSL certificates that may prevent
this tool from working.

-   The time may be set incorrectly on your XU4, which you can fix
    by setting the time using NTP.

        sudo aptitude install ntpdate
        sudo ntpdate -u ntp.ubuntu.com

-   The other possible issue is that you might not have the `ca-certificates`
    package installed, and so GitHub's SSL certificate isn't trusted. If you are
    on Debian, you can resolve this by typing:

        sudo aptitude install ca-certificates
