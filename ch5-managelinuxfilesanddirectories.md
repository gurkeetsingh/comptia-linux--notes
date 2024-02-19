# Managing linux files and Directories

- linux stores data on a physical hard disk, which in most of the cases are subdivided into a partition.
- what data is stored on partition or disk and what `filesystem` are used to manage the data are determined as a part of `system design process`
- each partition has a filesystem on which data is stored

The logical location of a directory has no relationship to where the data is physically stored. A `hierarchy` is a method of organizing objects based on some classification. The `Filesystem Hierarchy Standard (FHS)` defines a suggested `logical location of directories` and files on Linux (and UNIX) distributions. These definitions include what should be `contained` in specific directories and files.
Currently, the `Linux Foundation` manages the FHS.

## purpose of directories

- `/` The root directory, or top-level directory (pronounced slash directory, and the parent to all other files and directories)
- `/bin` Contains user commands, and can be linked to /usr/bin. contains executable commands or binaries
- `/boot` Contains files required to boot the system
- `/dev` Contains special device driver files for hardware devices
- `/etc` Contains global configuration files
- `/1ib` Contains system library files, also known as shared objects
- `/mnt` A mount point for temporarily mounted filesystems
- `/media` A mount point for removable media, such as DVD and USB drives
- `/opt` Directory intended for installation of third-party applications
- `/sbin` Contains system binaries used by root for booting or repairing the kernel; linked to /usr/sbin
- `/tmp` Directory for temporary files; known as a pseudo-filesystem because it resides in memory and, optionally, swap space
- `/usr` A suite of shareable, read-only UNIX system resources
- `/var` Contains files that vary in size (e.g, log files, e-mail files, and printing files)
- `/home` Contains home directories for user accounts
- `/root` The user root home directory (not to be confused with the / directory)
- `/run` Another pseudo filesystem (resides on memory) and contains system information gathered from boot time forward; cleared at the start of the boot process.
- `/srv` Contains data for services (e.g., HTTP and FTP) running on the server
- `/sys` Provides device, driver, and some kernel information
- `/proc` Another pseudo-filesystem that contains process and hardware information

the `absolute path` to a file is the path from the root (/) directory. it always begin with /

## viewing directory contents with ls

- when you provide an absolute path to a directory ls display the contents of that dir

options for `ls`:

- `-a` display all files including hidden files. hidden file names are prefixed with a `dot`. many configurations file are hidden.
- `-r` displays the directory contents recursively, ie it displays the contents of the current dir as well as the contents of all subdirectories

## managing linux files

- everything in linux is referenced by a file. even a directory is a file.

Files, Filenames and inodes:

- `linux files` consist of a filename, inode and data block(s).
- when a file is created it is given a name by the user or application and assigned a unique `inode` number (index number) by the filesystem
- operating system uses the inode number not the filename to access the file and its information
- A `linux filename` may contain upto `255` characters. must not contain a forward slash or null character
- filenames in linux are `case sensitive`
