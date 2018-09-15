Borg-ENV
========

*An environment manager for [BorgBackup](https://github.com/borgbackup/borg)*

**WARNING: Borg-ENV is currently under development and is considered unstable.
Make sure you have *backups of your backups*! I'm not responsible for any damage
caused by the usage of this software.**



What is Borg-ENV?
-----------------

Borg-ENV lets you manage multiple environments for different BorgBackup
repositories so you can easily manage multiple Borg repos on the cli without
having to always type the repository url or change exported environment
variables by hand when switching to another repository.



Core Features
-------------

### Manage environments

*Not fully implemented yet*

You can create new environments and edit, rename and delete them. It is also
possible to clone an environment to a new config.

The editor in which you can change the config is chosen by the `$EDITOR`
variable. It will fallback to `vim` (exit vim: press `ESC` and type `:q` and hit
`Enter` ;D)

*Currently implemented is creating and editing*

    $ borg-env create my-hdd
    ... an editor will open in which you can define the environment variables ...

    $ borg-env edit my-hdd
    ... that editor again ...

    $ borg-env rename my-hdd usb-hdd
    Renamed "my-hdd" to "usb-hdd".

    $ borg-env clone usb-hdd server
    Cloned "usb-hdd" to new environment "dummy".

    $ borg-env delete dummy
    Do you really want to remove the environment "dummy"?
    (Type uppercase yes to confirm): YES
    Deleted environment "dummy".



### Set the shell environment

*Not implemented yet*

Load an environment config and use borg directly from the cli.

    $ borg-env set usb-hdd
    $ borg list
    ... List of archives on local hard drive ...

    $ borg-env set server
    $ borg list
    ... List of archives on the borg server ...

Besides Borg specific environment variables, it is possible to define arbitrary
other variabes that might be used by your backup scripts.



### Run a command in a specific environment

If you don't want to pollute your shell environment or you want to issue just
a single command in a different environment, you don't need to switch to it.
Simply use the run command and specify in which environment the command
should be executed.

    $ borg-env run usb-hdd borg list
    ... List of archives on local hard drive ...

    $ borg-env run server borg list
    ... List of archives on the borg server ...

    $ borg-env run server bash -c "echo $BORG_RSH"
    ssh -i ~/.ssh/keys/borg.id_rsa

For the use case of running Borg there is also an alias:

*Not implemented yet*

    $ borg-env borg hdd create ::dummy-backup /home


