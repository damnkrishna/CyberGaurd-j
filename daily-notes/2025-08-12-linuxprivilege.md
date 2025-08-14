# Linux Privilege Escalation 

Going from lower permission account to higher permission account by privilege escalation.

- It lets you gain system admin levels of access which allows you to perform actions such as:
    - Resetting passwords
    - Bypassing access controls to compromise data
    - Change the privilege of existing (or new) users
    - Execute only admin commands

## Enumeration: Important During Post-Compromise Phase

### Basic System Information Commands

- **hostname**: Shows the system's hostname
- **`uname -a`**: Info about kernel version used by system
  (for finding linux version )
- **`/proc/version`**: Info on kernel version and additional data
- **`/etc/issue`**: Contains some information about the operating system

### Process Monitoring

**ps command (process status)**: Will show processes running
- `ps -A`
- `ps aux`
- `ps axif`

### Environment and Directory Information

- **env command**: Will show environment variables
- **ls command**: `ls -la` => potential privilege escalation vectors

### User and Permission Information

- **id command**: Shows user's privilege and group membership
- **`/etc/passwd`**: To discover users on system
    - `/etc/passwd | cut -d ":" -f 1`
    - `/etc/passwd | grep home`

### Command History

- **history command**: Shows stored info such as passwords or usernames

### File Search

- **find command**: Used for searching files and directories

## Netstat Commands

- `netstat -a`: Shows all listening ports
- `netstat -at` or `netstat -au`: To list TCP or UDP protocols
- `netstat -l`: Lists ports in listening mode
- `netstat -s`: Lists network usage statistics by protocol
- `netstat -ano`: Display all sockets, do not resolve names, display timers
