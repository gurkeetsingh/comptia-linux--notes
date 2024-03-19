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

- enter parted at the shell prompt and then use the `select` command to specify which disk to manage
- the parted utility writes partition changes immediately to the disk. `be cautious` and certain of the changes you made
