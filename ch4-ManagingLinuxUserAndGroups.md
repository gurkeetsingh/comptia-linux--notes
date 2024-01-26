# Managing linux user and groups

- Linux uses a method called Discretionary access control `DAC` to permit or restrict access to files.
- On `DAC` account owner decides who has permission to access, delete, or modify their files.

## Linux user accounts

- A user is a person or service that requires access to system files or resources.
- A user_account is a method of providing or restricting access to system resources.

## Linux user IDs and privileges

- linux implements user ID ranges to organize users.
- Depending on the `UID` the individuals have few or many privileges.
- The user `root` or `UID 0` is a privileged linux account and the administrator of the system. the root user can do anything on the computer.
- Linux allows multiple users to share a UID. but it is not advisable to assign user ID 0 to multiple user.

## CREATING AND MANAGING USER ACCOUNTS FROM THE COMMAND LINE

- System administrators create user accounts with the `useradd` command.
- Once a user's account is created, the user needs to set a password with the `passwd` command.
- `usermod` command is used to change user-id or group.
- The useradd utility is used to add users to the Linux system. The useradd command obtains default values initially from /etc/login.defs and next from / etc/ default/useradd. Entries within the directory /etc/skel/ are used to populate the new user's home directory.
- The `passwd` utility allows you or root to change your password and allows a system administrator to manage password aging.
- a user can change their own password by executing the command passwd
- root can change other user password using the command `passwd <username>`
