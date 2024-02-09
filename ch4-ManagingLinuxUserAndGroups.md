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
- the user root has access to all files and commands and has full control of the operating system, including ability to bypass operating system or application restrictions.
- any user assigned the`user ID 0` has `root privileges`.
- Linux allows multiple users to share a UID. but it is not advisable to assign user ID 0 to multiple user.

Meaning of user IDs 0-99:

- Administrative users 0-99 are added to the operating system during the installation process.Acc to the `Linux standard base(LSB)` core specification user accounts within this range are created by the operating system and may not be created by an application (libre office).

User and system accounts:

- user account provides nonprivileged(Non-privileged users are users who do not have the proper permissions) access to system resources.
- User account ID ranges are specified by the variables `UID_MIN` and `UID_MAX` in `/etc/login.defs`, the file that defines new user defaults, such as the location of the user's mailbox, their user ID, and their password aging defaults.
- The default `minimum UID is 1000`, and the default `maximum UID is 60000`, but it can be as high as `4.2 billion` depending on the CPU model and Linux version.
- A Linux service (an application that is running in the background, such as abrt) may be assigned a user account. The user account ID for a service is in the `range 0-99` or between the values set by `SYS_UID_MIN` and `SYS_UID_MAX` in `/etc/login.defs`.
- A system account is created by executing the command `useradd --system <system-account-name>`. there are many services that are not assigned a user account
- `Service or system accounts` are nonprivileged accounts created by a system administrator or application, and are sometimes used to restrict access to configuration or data files. Unlike user accounts, system accounts cannot log on to the system, do not require a password, do not have password aging applied, and do not have home directories.

## Where linux user account information is stored

where linux stores user configuration files on the local system. Information for users and  groups is storedin the following coniguration files:

`/etc/passwd` a user database file:

- contains `user account` information
- it is an example of `flat-file database`.
- A flat file is a collection of data stored in a two-dimensional database in which similar yet discrete strings of information are stored as records in a table. The columns of the table represent one dimension of the database, while each row is a separate record. The information stored in a flat file is generally alphanumeric with little or no additional formatting. The structure of a flat file is based on a uniform format as defined by the type and character lengths described by the columns.
- each line of the file contains a `unique` user record
- each record contains `seven fields`.
- A `: (colon)` is used as a delimeter to separate the fields.
- the format for a record in `/etc/passwd` file is: `user_name:password:uid:gid:comment:home_directory:default_shell`
- system accounts donot require a default shell. these accounts have either `/sbin/nologin` or `/bin/false` in the default_shell field.

`/etc/shadow` the protected user passsword file:

- it is a flat file database that store user password and password aging expiration.
- each record in in `/etc/passwd` should have a corresponding record in `/etc/shadow`
- the format for a record in /etc/shadow is: `username:password:last_modified:min_days:max_days:warn_days:inactive:expire`
- password field stores the user's password in encrypted format using hash.
- if password field contains two `!!` marks, an account password have never been assigned.
- the default values of `min_days`, `warn_days` and `max_days` is stored in `/etc/login.defs`.  

## CREATING AND MANAGING USER ACCOUNTS FROM THE COMMAND LINE

- System administrators create user accounts with the `useradd` command.
- Once a user's account is created, the user needs to set a password with the `passwd` command.
- `usermod` command is used to change user-id or group.
- The useradd utility is used to add users to the Linux system. The useradd command obtains default values initially from /etc/login.defs and next from / etc/ default/useradd. Entries within the directory /etc/skel/ are used to populate the new user's home directory.
- The `passwd` utility allows you or root to change your password and allows a system administrator to manage password aging.
- a user can change their own password by executing the command passwd
- root can change other user password using the command `passwd <username>`
