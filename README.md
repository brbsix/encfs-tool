# encfs-tool

Shell script to easily interact with EncFS volumes. This was created for use on Android's mksh (and bash) shells, but should also work on similar *nix shells.

This script was created to fufill a personal use-case, namely to mount multiple EncFS volumes at once (generally via init script at startup) and to unmount (forcibly if necessary) multiple volumes upon poweroff or triggering event.

Other android apps such as Cryptonite facilitate the use of single EncFS volumes, but I know of no other tool that allows batch commands.


Features
--------

* run commands on individual volumes by name
* run commands on multiple volumes (in the VOLUME_DIR)
* check whether volumes are mounted or not
* mount and unmount volumes
* force-unmount volumes (killing associated processes first)

Installation
-----

Copy encfs-tool to your bin folder and then mark as executable.

```
su
mv encfs-tool /data/local/bin
chmod a+x /data/local/bin/encfs-tool
```

If you want to use batch commands, open encfs-tool in an editor and set VOLUME_DIR to the path where your EncFS volumes are stored.

NOTE: On Android, you may need to add /data/local/bin to your PATH. This involves editing your shell's rc file. If you are using the default mksh shell, it is located at /system/etc/mkshrc. For Bash, it is most likely at /system/etc/bash/bashrc. Append the following to the end of the file:

```export PATH="$PATH:/data/local/bin"```


Usage
-----

To get full usage information:

```encfs-tool help```

Be sure to run mount and unmount commands as superuser:

```
su
encfs-tool status_all
```
