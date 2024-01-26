# Working with the linux shell

- A shell is a program that functions as a user interface and command-line interpreter when using a command-line interface.
- two types of user interfaces are: command line interface and graphical user interface.
- A process is a single instance of a program that operates in its own memory space. The operating system assigns a `unique process ID (PID)` each time a program is started. This PID is used to control and track resources assigned to the program

## MANAGING VARIABLES

- A variable is a memory location that is assigned a name and is used to store data.
- Two types of variables are: shell variables(local variables) and environment variables(global variable).
- syntax for shell: `variable_name=value`.
- to view content of the variable execute the command: `echo $<variable_name>`  the $ sign here means metacharacter.
- `set` command displays list of all the shell variables and functions in the current process.
- unlike shell variables environment variables are visible to child process
- To convert a shell variable to an environment variable, you need to assign an `export` attribute to the variable. When a parent spawns a child process, all variables with this attribute are visible to the child
- Convert existing shell variables to environment variables by running the command, `export <variable name>;` this assigns an export attribute to existing variables.
The `unset` command deletes the variable and removes it from the environment. The `env` command displays a list of all environment variables in the current shell.
- Running `declare -p ‹variable_name>` displays the variable's properties. The `-x` in the properties section of the output signifies that it is an environment variable.
- Each user in operating system has its own environment.

## CONFIGURING ALIAS

- An alias is a command shortcut.
- its syntax is: `alias  <alias_name>='<command>'`
- The command `alias ls='ls --color=auto'` creates an alias to replace the default ls. Aliases take precedence over all other commands, so every time the ls command is run, the command ls  — color=auto executes.
- An alias exists only in the shell in which it was created or loaded.
- executing `alias | grep command=` displays the list of the aliases loaded into the memory.
- the backslash `\` precedes the ls command temporarily negates the alias
- the command `unalias ls` permanently removes the alias

## SETTING UP THE LOCAL ENVIRONMENT

- A locale is a set of environmental variables that defines the language, country, and character encoding settings (or any other special variant preferences) for your applications and shell session on a Linux system. These environmental variables are used by system libraries and locale-aware applications on the system.
Locale affects things such as the time/date format, the first day of the week, numbers, currency and many other values formatted in accordance with the language or region/country you set on a Linux system.
- the command `localectl` is used to view and modify system locale and keyboard
- `localectl list-locales` is used to list all the locales in the system.
- locale categories are associated witha locale name. the locale name defines the formatting for a specific region. format of locale name is:  `language_region.encodingRegion@modifier`

## BASH CONFIGURATION FILES

- Variables, aliases, and shell option settings executed on the command line are stored in memory. These settings disappear when the user logs out of the system.
- But when you create aliases and variables that make your job easier, you want to keep those settings. Configuration files define settings that remain persistent even after logging off or rebooting.
- Log In Script Order: when a user logs into a linux system, customization scripts are read in the following order when using the bash shell:
  1. /etc/profile
  2. /home/user_name/.bash_profile
  3. /home/user_name/.bashrc
  4. /etc/bashrc

REDIRECTION

- Redirection permits a user to alter from the defaults for stdin, stdout, or stderr to a device or file using their file descriptors.
File Descriptors:
- A file descriptor is a reference, or handle, used by the kernel to access a file. A file descriptor table is created for every process. This table tracks all files opened by the process. A unique index number, or file descriptor number, is assigned to a file when it is opened by a process
