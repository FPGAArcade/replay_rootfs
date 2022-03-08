# replay_rootfs 

- [![image](https://github.com/FPGAArcade/replay_rootfs/actions/workflows/image.yml/badge.svg)](https://github.com/FPGAArcade/replay_rootfs/actions/workflows/image.yml)
- **[Latest release](https://github.com/FPGAArcade/replay_rootfs/releases/latest)**  

## Instructions

The build produces two artifacts:
- replay_de10_image
- replay_de10_update

Both of these contain the complete bootchain (identical binaries) for the DE10-Nano: 
1) Bootloader (barebox)
2) Kernel (Linux)
3) RootFS (Buildroot)

The only difference is the distribution format.

The `image` archive contains a pre-configured `sdcard.img`, suitable for writing directly to an SDCARD.  
This is typically done using `dd`, [Etcher](https://www.balena.io/etcher/), or similar software.  
Please note that this is a **destructive** operation - the old contents of the sdcard **will be lost**.

The `update` archive is basically the contents of the `Boot` partition of the SDCARD image above.  
As such it's suitable for updating from a previous version of `replay_rootfs`.  
Simply overwrite the old contents of the `Boot` partition with the new files from the archive.  
This can be done either on the DE10-Nano directly, or on your host PC.

In short : if you already have an SDCARD prepared, go ahead an use the `update`, otherwise use the full `image`.

During the first boot the system will reconfigure the partition table, and create an additional exFAT partition spanning whatever is left of the SDCARD.  
This partition is effectively the `userdata` partition (called `Data`), which will contain the FPGA bitstreams and other configuration files.  
The process takes about 30seconds, after which the DE10-Nano will reboot. The installation process is now complete.
