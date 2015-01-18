# encfs-tool

Shell script to easily interact with EncFS volumes. This was created for use on Android's mksh (and bash), but should work on other *nix platforms.

This script was created to fufill a personal use-case, namely to mount multiple EncFS volumes at once (generally via init script at startup) and to unmount (forcibly if necessary) multiple volumes upon poweroff or triggering event.

Other android apps such as Cryptonite facilitate the use of single EncFS volumes, but I know of no other tool that allows batch commands.


Features
--------

* run commands on individual volumes by name
* run commands on multiple volumes (in the VOLUME_DIR)
* check whether volumes are mounted or not
* mount and unmount volumes
* shutdown command to force-unmount volumes (killing associated processes first)

Installation
-----

Copy encfs-tool to your bin folder and then mark as executable.

```
su
mv encfs-tool /data/local/bin
chmod 0755 /data/local/bin/encfs-tool
```

If you want to use batch commands, open encfs-tool in an editor and set VOLUME_DIR to the path where your EncFS volumes are stored.

*NOTE: On Android, you may need to add /data/local/bin to your PATH. This involves editing your shell's rc file. If you are using the default mksh shell, it is located at /system/etc/mkshrc. For Bash, it is most likely at /system/etc/bash/bashrc. Append the following to the end of the file:*

```export PATH="$PATH:/data/local/bin"```


Configuration
-----

**NOTE: This script assumes that mount and volume names follow a prescribed format.**

I.e. For a mount folder named `Folder` the EncFS volume is appropriately named `.Folder_encfs`

If all of your EncFS volumes are located in one directory, set `VOLUME_DIR` at the top of the script to that path.

Your mount passphrase/password can be supplied a number of ways. For automated use, it can be set at the top of the script under `PASSWORD` or stored in a file and passed as an argument `encfs-tool --file passfile.txt mount_all` (though this is certainly unadvisable unless you have an encrypted filesystem). Your password can also be passed in via stdin, i.e. `echo "password" | encfs-tool --stdin mount_all` (though this has it's issues as well).

The password will be prompted for interactively if `PASSWORD` is unset or the `--prompt` option is used.


Usage
-----

To get full usage information:

```encfs-tool help```

Be sure to run mount and shutdown/unmount commands as superuser:

```
su
encfs-tool mount_all
```

If ```VOLUME_DIR``` is set, then you can run commands as follows:

```
encfs-tool info_all
encfs-tool info Folder
```

If your EncFS volumes are spread out in various locations (or ```VOLUME_DIR``` is unset), you can run commands as follows:

```
encfs-tool info_all /path/to/volumes/
encfs-tool info /path/to/volumes/Folder
```
