# Managing storage

## device naming conventionsf

- a device name format is `xxyz`. 
- `xx` is the device type, some example are storage devices include storage devices such as `sd` (SCSI/SATA), `tty` for terminals
- `y` indicates the device logical unit number, a unique identifier for a device within the group of devices.
- `z` indicates the partition number. A block device may be split into numbered partitions 

## Viewing disk partitions

`lsblk`:

- this command is displays the list of block devices and their partitions.

`fdisk -l`:

- it displays the partition table of all block devices

`parted -l`:

- the command `parted -l devicename` and fdisk -l will both display disk partition information
- the parted command will print some detailed logical volume information

## creating partitions

- A partition is a section of a physical disk device treated as a logical block device
- the commands `fdisk, parted, gdisk` are applications used to create partitions on a disk device

## partition considerations

partition availability:

- a SCSI device can have upto 15 partitions and IDE device can have 63 partitions

disk space availability:

- space is available to add additional partitions by determining the difference between the total number of sectors on the device and the ending sector of the last partition

partition size:

- most operating systems and applications have documentations that indicates the amount of disk space they require

swap partition size:

- swap space is virtual memory space created on a swap filesystem
- swap space should be larger than the amount of memory installed on the system

## fdisk partitioning utility

- fdisk utility is used to modify a partition table of a disk device. any changes made while working within the application are `stored in the memory until` the changes are written to the disk partition table
- the command `fdisk devicepath` is used to manage partitions for a specific device 

Creating a partition:

- enter `n` to create a new partition and then specify whether you want to create a primary(p), extended(e) or logical(l) partition.
- you can create a logical partition only in an `extended partition` if an extended partition does not exist you will not be offered the choice to create a logical partition
- press the enter key to select the default partition number which are 1 to 4
- you cannot use the partition number that has been already allocated.
- the next entry is selecting the `starting sector`. most of the time default is selected unless you want to change the starting sector to some other position.
- then you can specify the `size of the partition` by entering the number of sectors, or the size in kb, mb or gb, using `+5G` for 5 gb
- after specifying the size you should verify your new partition by entering `p`
- the ID column contains the `filesystem code`. A partition entry in the partition table will need a partition type to help the Operating System know how to handle the partition.
- filesystem code is changed by entering `t` and then entering the number of the partition you want to change and then type the partition number code

Deleting a partition:

- to delete a partition using fdisk enter `d` at the command prompt and specify the partition number to delete
- any data that resides on the partition will be lost once you commit the change to disk

## parted partitioning utility

- parted utility is important because it can handle both a `mbr` and `gpt` parted scheme.
- enter parted at the shell prompt and then use the `select` command to specify which disk to manage
- the parted utility writes partition changes immediately to the disk. `be cautious` and certain of the changes you made
- `mkpart` subcommand at the parted prompt is used to create a partition.
- Command: `mkpart [part-type name fs-type] start end` , parttype name- like primary, logical, extended, filesystem type, then starting and ending location of partition on a disk
- use `help` subcommand to get all the command and their work

## gdisk partitioning utility

- it is used to manage a `gpt` partition
- gdisk understands extensible firmware interface `EFI` hard drive structure
- it can be used for: convert a MBR to a GPT partition table.
- enter `?` to view a list of gdisk subcommand

## Block device encryption

- block device encryption is used to protects the data confidentiality on the block device, even if the device is removed from the system, by encrypting data as it is written and decrypting data as it is read.
- to access the device you must enter a `passphrase` during system startup to activate a decryption key
- CREATING AN ENCRYPTED BLOCK DEVICE'
- `linux unified key setup(LUKS)` supports physical volumes, logical volumes, RAID, and physical block device
- command= `cryptsetup luksFormat devicename` to format the device as an encrypted device but it will erase all the data on that disk or device, then enter the `passphrase` twice, the device will be formatted

## Creating Filesystem

- a filesystem manages the storage and retrieval of data.
- linux support multiple filesystem via kernel modules and abstraction layer called the virtual filesystem

## Available filesystem

- to use a specific filesystem a appropriate kernel module must be available 
- to determine which filesystem is available use the command: `ls -l /lib/modules/$(uname -r) /kernel/fs`
- uname -r means current kernel version
- to determine which kernel filesytem modules are currently loaded, execute: `cat /proc/filesystems` the term `nodev` in result of this is known as no device, means that the filesystem is not located on a block device but is loaded in memory
- the command `blkid` displays the UUID and filesystem type of a partition

## Building a filesystem

- once you create a partition prepare it for storing a data by creating a filesystem on it
- use the command `cat /proc/filesystems` to view the loaded filesytems on the system. in this output the `nodev` means that the filesystem is available on the memory and not on the block device(storage disk or device)
- `sudo blkid` shows the UUID and the filesystem type of the partition
- `df -hT` is used to display the filesytem type
- A `Universally Unique Identifier (UUID)` is a `128-bit` value that is unique across all devices and systems. UUIDs are used to identify many types of objects, including storage devices, partitions, and RAID arrays. They are randomly generated using system hardware information and time stamps. UUIDs do not change even when hardware configurations change or devices are reconnected. 
- some of the commands are mkfs, xfs, btrfs, mkswap

using `mkfs` to create a filesystem:

- it is used to make an ext2, ext3, or ext4 filesystem on a partition
- specify which filesystem to use with `-t` option
- `mkfs -t ext4 /dev/sda8`
- after execution check output
- multiply the number of blocks and blocksize to get the size of the partition
- number of inodes will tell you how many files can you store on that partition. when you reaches the inode limit you cannot create or store any new file on that system even if there is free space available
- `tune2fs` command is used to adjust various filesystem parameters on ext2, ext3 and est4 filesystem. command: `tune2fs -L labelname /dev/sda` places label on the filesystem, `-j` is uses to add journal to the ext2 filesystem

## managing swap space

- swap space is virtual memory created on block devices
- when ram becomes full some memory must be released to make space for a execution of additional programs
- to do this a memory management unit witll take pages of data stored in RAM that are not currently being used and swap them to virtual memory
- `CREATING A SWAP PARTITION`
- add a partition of `type 82` which is linux swap using the fdisk command if the next command does not work. for now it shows device or resource busy
- execute the `mkswap` command to create a swap area on a partition. `mkswap devicepath`
- when swap partition is created it is not available to the operating system until `enabled`. 
- to enable the swap partition execute the command `swapon partitionpath`
- the priority of the filesytem will determine when the operating system will use it. if the user doesnot specify the priority number then the kernel will assign the negative priority number to it. if the two partition have same priority then they will be accessed in round robin method means that both have a given time in which they work
- to disable an existing swap partition execute `swapoff devicepath`

## Mounting a filesystem

- a mount point is a logical connection between a directory and a filesytem and a connection is made with the `mount` command
- prior to mounting a device create a empty directory for a mount point
- the dir `mnt` is used to mount a temporary automounted filesystem from a network filesystem and `media` is used to mount a media devices like a usb or disk
- mount command requires a `root access`
- `mount -t filesystem_type device mount_point`
- -t filesystem type is optional, if the destination directory is omitted then it mounts the filesystems listed in the /etc/fstab and same happen if you only specify the mount point
- mount command with no switches displays mounted filesytem and its too many in output
- command `cat /proc/mounts` displays mounted filesystems. proc dir contains the current state of the kernel
- to remount a filesystem with new options execute `mount -o remount newMountOptions mountPoint`
- it can be unmounted by using the command `umount device` or `umount mountpoint`

## Mounting filesystem automatically at boot

- devices can be automatically mounted by creating an entry in the filesystem table named `/etc/fstab` or by creating a mount system unit.
- prior to making `changes` in `/etc/fstab` make a backup of that file. errors in this file can prevent your system from booting but it can be recovered from a backup version of /etc/fstab by booting in rescue mode.
- `ADDING A MOUNT POINT IN /etc/fstab`
- this file contains a mount parameters for a device
- `sudo mount -a` is used to mount all the devices on the system but it is done automatically at the boot if that device has a option of `auto or defaults` enable

