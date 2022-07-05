# MacOS Overview

## Executable PATH
- `PATH` is an environment variable that contains a colon-seperated list of directories where your shell will look for executables that are called by name on the command line without an explicit path to them 
- Ex: `/usr/bin:/bin:/home/bin`
    - Any executable called by name will be searched for in these directories in the order from left to right
    - if an executable exists in 2 directories, the one that is found first is executed
    - If no executable is found in any of the directories on the path, the shell will not execute the command and will throw a command not recognized error
- `/etc/paths` sets the PATH system wide for all users (macOS specific)
- `.~/zsh_profile` sets per-user preferences (`~` is the user's home directory)
- `PATH`, `$PATH`, and `${PATH}` all reference the same variable just in different contexts
    - `PATH` is for setting the variable (e.g. `PATH=/usr/bin`) 
    -  `$` denotes an environment variable
    - variable names are case sensitive so PATH is different than Path

## Bash/zsh Profile vs RC:
- `.bash_profile` is executed for login shells (e.g. logging into machine via console or via ssh)
- `.bashrc` is executed for interactive non-login shells (e.g. already logged in and open a new terminal window)
  - Also run when starting a new bash instance by typing `/bin/bash` such as the shebang at the top of some python scripts
- In OSX, terminal runs a login shell every time by default unlike other operating systems 

## Filesystem
- Does not follow the Filesystem Hierarchy Standard that Linux operating systems do so there are some similarities and differences
- `/` is the root of the MacOS filesystem
- `/System/Library/Kernels`: Contains the OS kernel (replaces `/boot` folder in FHS)
- `/Users`: replaces the `/home` folder in FHS
- `/var/root/`: replaces the `/root` folder in FHS 
- `/usr` contains user installed utilities and apps
    -  *user commands:*
      - `/usr/bin` for normal users
      - `/usr/sbin` for admin users
    - shared libraries:
      - `/usr/lib`
    - Man pages (manual page- software documentation)
      - `/usr/share/man`
    - executables that shouldn't directly be run by users
      - `/usr/libexec`
    - *a subdirectory to place programs, libraries, and other files that don't come with the base OS*
      - `/usr/local`
- `/dev` contains device files 
- `/etc` contains system configuration files and scripts
    - `/etc/paths` contains a list of paths used by `path_helper` to build and set the PATH to search for commands along
- `/bin`  contians executables to provide essential user utilities (e.g common command line commands like ls or pwd or cd)

`man hier`:

```wiki
 /             root directory of the filesystem

 /bin/         user utilities fundamental to both single-user and multi-user environments

 /dev/         block and character device files


 /etc/         system configuration files and scripts

 /mach_kernel  kernel executable (the operating system loaded into memory at boot time).

 /sbin/        system programs and administration utilities fundamental to both single-user and multi-
               user environments

 /tmp/         temporary files

 /usr/         contains the majority of user utilities and applications

               bin/      common utilities, programming tools, and apps
               include/  standard C include files

                         arpa/       C include files for Internet service protocols
                         hfs/        C include files for HFS
                         machine/    machine specific C include files
                         net/        misc network C include files
                         netinet/    C include files for Internet standard protocols; see inet(4)
                         nfs/        C include files for NFS (Network File System)
                         objc/       C include files for Objective-C
                         protocols/  C include files for Berkeley service protocols
                         sys/        system C include files (kernel data structures)
                         ufs/        C include files for UFS

               lib/      archive libraries
               libexec/  system daemons & system utilities (executed by other programs)
               local/    executables, libraries, etc. not included by the basic OS
               sbin/     system daemons & system utilities (executed by users)
               share/    architecture-independent data files

                         calendar/  a variety of pre-fab calendar files
                         dict/      word lists
                         man/       manual pages
                         misc/      misc system-wide ascii text files
                         mk/        templates for make
                         skel/      example . (dot) files for new accounts
                         tabset/    tab description files 
                         zoneinfo/  timezone configuration information
 /var/         multi-purpose log, temporary, transient, and spool files

               at/        timed command scheduling files; see at(1)
               backups/   misc. backup files
               db/        misc. automatically generated system-specific database files
               log/       misc. system log files
               mail/      user mailbox files
               run/       system information files describing various info about system since it was booted

               rwho/      rwho data files
               spool/     misc. printer and mail system spooling directories
               tmp/       temporary files that are kept between system reboots
               folders/   per-user temporary files and caches
```

## Useful Commands
- `man cmd` will display the manual page for the terminal command (useful for getting the flag descriptions for commands like `ls`)
- `|` pipe operator is great for doing additional commands to the output of the first command
- `echo "source /opt/ros/foxy/setup.zsh" >> .zshrc` is useful for adding things to the `.zshrc` without opening it up in an editor 
- `which python3` is usefull for figuring out where commands/executables are installed on the PATH
- `compaudit | xargs chmod g-w` basically runs an audit for insecure directories (usually related to read-write permissions) and removes any write permissions that should not be on directories ([Source](https://www.wezm.net/technical/2008/09/zsh-cygwin-and-insecure-directories/))
  - needed to use this to fix a compaudit warning when sourcing ros2-foxy-base

## Resources
1. [MacOS Filesystem](https://apple.stackexchange.com/questions/119230/what-is-standard-for-os-x-filesystem-e-g-opt-vs-usr)
2. [PATH Explanation](https://unix.stackexchange.com/questions/111550/what-is-path-on-a-mac-os)
3. [Bash Profile vs RC](https://apple.stackexchange.com/questions/51036/what-is-the-difference-between-bash-profile-and-bashrc)
4. [Homebrew symlinks in /usr/local/opt to /usr/local/Cellar](https://stackoverflow.com/questions/35337601/why-is-there-a-usr-local-opt-directory-created-by-homebrew-and-should-i-use-it)

