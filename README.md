# Alpine Linux Bootstrap for Linode
_Should work everywhere else. If you have access to a console that can mount your volumes, and run a shell script._

A simple script that can be executed in recovery mode to bootstrap Alpine Linux on a Linode server.

## Creating a Linode

This script assumes your Linode will have **four** disks for boot, root, data and swap.

| **Name**  | **Mountpoint** | **Minimum recommended** | **Filesystem** |
|-------|------------|---------------------|------------|
| /boot | /dev/sda   | 128 MB              | ext4       |
| /     | /dev/sdb   | 3 GB                | ext4       |
| /data | /dev/sdc   | Rest of your space  | ext4       |
| swap  | /dev/sdd   | 512 MB              | swap       |

_Name is the mountpoint in the OS, Mountpoint is the mountpoints in the control panel._

If you decide not to use a swap disk, you will need to manually delete the relevant parts from the script (which should be fairly easy).

## Configuration profile

### Label and notes

**Label**: Alpine

### Boot Settings

**Kernel**: GRUB 2

### Block Device Assignment

+ /dev/sda
  - boot
+ /dev/sdb
  - root
+ /dev/sdc
  - data
+ /dev/sdd
  - swap

### Filesystem/Boot helpers

Turn everything off.

Boot the Linode into recovery mode with the disks assigned as above.

## Executing the Script

Connect to the Linode with Lish either via SSH or the browser console. To download and run the script:

    curl -o- https://gist.githubusercontent.com/snowydane/8f8cfce9334f2b36cddb6065ceed6d7f/raw/16d3db4013a23829758f6230f2ad9cec60857b9f/alpine-boostrap.sh | bash

Once that finishes, shut the Linode down from recovery mode and, staying in the Lish console, run:
  
    boot 1

After a bit, you should be at the Alpine login screen. The root user, by default, does not have a password. At this point, you can install an SSH server, which pretty much completes the installation.

## Credit

This script is basically [Andy Leap's guide](https://github.com/andyleap/docs/blob/master/docs/tools-reference/custom-kernels-distros/install-alpine-linux-on-your-linode.md) written as a working script (with fixed networking!), so big thanks to him.

Jason Chen for original [script](https://github.com/jcorme/alpine-linode-bootstrap/blob/master/README.md)

Github user [jcorme](https://github.com/jcorme) for his [version](https://github.com/jcorme/alpine-linode-bootstrap)
