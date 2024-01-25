# CREATING AND MANAGING USER ACCOUNTS FROM THE COMMAND LINE

- System administrators create user accounts with the [useradd] command.
- Once a user's account is created, the user needs to set a password with the [passwd] command.
- [usermod] command is used to change user-id or group.
- The useradd utility is used to add users to the Linux system. The useradd command obtains default values initially from /etc/login.defs and next from / etc/ default/useradd. Entries within the directory /etc/skel/ are used to populate the new user's home directory.
- The [passwd] utility allows you or root to change your password and allows a system administrator to manage password aging.
- a user can change their own password by executing the command passwd
- root can change other user password using the command [passwd <username>]
