# online-linux-format

This tool allow you to rearrange partitions or even apply a different disk image on a running Linux server with only SSH and superuser access, requiring Kernel 3.18 or higher and systemd.

If the target server is not on a Cloud provider, or somehow it is not possible to boot with a LiveCD or turn the server off and connect the disk on a different machine in order to repartition it this tool can help you with this task.

Before continue be aware that these operation is extremely risky, I give no warranty about it, it is recommended that you try before on a cloned virtual machine, and if you decide to proceed do it at your own risk, it is very likely that you are going to break your system and I am not liable for any damages arising from its use.

## Backup

This tool offer a backup routine that simply create a tarball file with some important files, the creation of a backup do not prevent your server to break, but can help to recreate another machine with the same files it in case of a lost.

There is two types offered by this tool, a slim one, and a full one: The slim one copies only some configuration files, you will require to reinstall the server apart, it is inteded only to help reconfigure it; The full backup can be used as base image and can be applyed to others servers, but can be very large.

Copy the file `exclusions.sample` to `exclusions` and edit it in order to ignore large directories (can be found with `du -hd2 ... | sort -rhk1 | head`), or even to not ignore some default ignored files such as logs and caches.

    ./run backup username@hostname password
    # or
    ./run slim username@hostname password

It is required to have enough free space on `/tmp` mount point on target machine in order to store the generated file. The file will be copied to `backups` directory on origin machine.

The password is optional, but if the it is not provided make sure you have configured correctly the `.ssh/config` and keys files, as well as the server do not ask for password when launching `sudo`.

# Usage

Copy the file `partitions.sample` to `partitions` and edit it to fit your needs.

## Troubleshooting

This tool is inteed to stop working in case of any command to fail, it can happen if some required kernel module is not provided, as this tool is ofered with no guarantee there is nothing you can do in some cases, but even so you can file a bug with your user case and perhaps, someday, I can provide a workaround, be as detailned as possible about your server configuration.
