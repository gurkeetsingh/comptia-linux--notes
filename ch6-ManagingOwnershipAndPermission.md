# Managing Ownership and Permission

there are 2 task to accomplish when managing user access to a linux system:

- control who can `access` the system
- define what users can do after they have logged into the system

access control is implemented by `defining users and groups` and then defining what those users and groups are `authorized to do` after they log into the 

- by default the owner of a directory on a linux system receives `read, write and execute` permission to the directory
- the `group owner` of a file or directory will be the primary group of the user owner who created that file or dir

## Managing ownership from the command line

- file and directory ownership is not fixed entity.
- only root can change the user who owns a file or directory

using `chown` to change ownership:

- The chown utility changes the user or group that owns a file or directory.
- ownership only specifies who `owns what`, not what `one can do or cannot do` with files or directory
- syntax: `chown user:group fileOrDirectory`
- use `-R` option with chown to change the ownership on many files at once in current directory
- `chgrp` is used to change the group of the file or dir. its syntax is `chgrp groupname fileordir`

## Managing file and directory permission

How Permissions work:

- Permission are used to specify exactly what an end user may do with files and directories in the filesystem like reading, writing or executing.
- permissions can be configured to prevent an end user from even seeing a file within directory.

## Working with special permission

## Configuring file attributes and access control lists

linux offers advanced features to provide more security for rfiles an