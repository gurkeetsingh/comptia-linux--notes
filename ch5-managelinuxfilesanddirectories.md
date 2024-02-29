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
- `-F` is used to show the type of files.

## managing linux files

- everything in linux is referenced by a file. even a directory is a file.

Files, Filenames and inodes:

- `linux files` consist of a filename, inode and data block(s).
- when a file is created it is given a name by the user or application and assigned a unique `inode` number (index number) by the filesystem
- operating system uses the inode number not the filename to access the file and its information
- A `linux filename` may contain upto `255` characters. must not contain a forward slash or null character
- filenames in linux are `case sensitive`

Creating and validating files with `touch` and `stat`:

- creating a new file can be accomplished by executing the `touch` command.
- `stat` command is used to view the timestamps(`access, modification, change`) and inode numbers of the file use the stat command
- On `ext-based` filesystems such as `ext 3` and ext 4, all inodes are `created` when the filesystem is `built`, so it is possible to run out of inodes even though there is plenty of disk space available! `XFS filesystems` support `dynamic inode allocation`, building inodes as needed, so they do not suffer from inode exhaustion issues.

Soft and Hard links:

- A link is a method of referring to data stored in an inode or another file.
- basically it is an `pointer`.
- this allows us to change data in one file and have that change reflected in other filenames.
- A `hardlink` associates the filename with the file's inode number.
- to `create` hardlink use the command `ln filename hardlinkfile`.
- hardlink only works when used wihtin the `same filesystem`.
- in stat when link is 2, it means that one file inode has 2 filenames.
- you can use the command `unlink` to remove the link of the file from the same inode number used by more than 1 file. its syntax is: `unlink hardlinkfile`.
- `SOFTLINK`
- A `symbolic link` also called a soft link.
- it can reference a file in the same filesystem, another filesystem, directories, or even across the network.
- each symbolic link file has it own inode
- the data within `symlink` contains the filename it is linked to, similar to shortcut in windows or macos
- its syntax is:`ln -S sourcefile destinationfile`
- in softlink the link count don't change this is because a soft link creates its own inode instead of adding another filename to the current inode.

how files are stored on most filesystem:

- a file's `metadata` is stored in an inode. `Inode` contain all the information about a file. such as permission, number of links, user and group owner, file size, time stamps and data pointer(to datablocks) but not the `FILENAME`.
- when a file is created it is assigned an inode numbers from a list of available inode number in the system

Creating new directories with `mkdir`:

- syntax to create a directory is: `mkdir directoryName`.
- you can use an absolute path or relative path to create a directory somewhere other than the current directory.
- the `mkdir -p` command creates a directory `tree`.
