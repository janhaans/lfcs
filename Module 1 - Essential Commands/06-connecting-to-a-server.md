# Understanding the root user

- Root user is the almighty, administrative user
- Root user lives in the Linux kernel space where no permissions exist and therefore there are no restrictions what a root user can do (unlimited account).
- Using Root should be avoided.
- After being logged in as ordinary user you can use `su` to get the root user shell if you know the password of root user (not recommended)
- The best alternative is to use `sudo` which requires specific setup

# Understanding su

- `su` is switch user, it allows you to open a shell as a specific user
- Use `su` to open a subshell; not all environment variables are set as the target user
- Use `su -` to open login shell; all environment variables are set as the target user (recommendend)
- User root can use `su` to become any other user without entering a password
- Regular users can use `su` to become any other user if the regular user enters the password of the target user

**Note**: On Ubuntu the root user does not have a password and therefore a regular user cannot `su -` to switch to root user. On Ubuntu a regular user uses `sudo` command to execute administrative commands.

# Using sudo

- `sudo` grants regular users the permissions to run administrative commands
- The default "admin" user has `sudo` privileges by default:
  - On Redhat, because of membership of the group "wheel"
  - On Ubuntu, because of membership of the group "sudo"
- Use `sudo <administrative command>` to run a administrative account
- Use `sudo -i` top open root shell (not recommended) (identical to the command `sudo su -`)
- Use command `id` to check if your user account is memebr of group wheel (Redhat) or sudo (Ubuntu)

# Sudo configuration

- Use `visudo` to open `/etc/sudoers` configuration file and to validate the changes before saving.
- Alternatively, add drop-in files in `/etc/sudoers.d` directory
- Add following line to `/etc/sudoers` configuration file to cache the `sudo` credentials for 4 hours

```
Defaults timestamp_type=global,timestamp_timeout=240
```

Use `visudo` to add an new `sudo` configuration in `/etc/sudoers` by using the following format:

```
<username> <hostname.example.com>=(<run_as_user>:<run_as_group>) <path/to/command>
```

- `<username>` is the user that enters the command, for example, user1. If the value starts with %, it defines a group, for example, %group1.
- `<hostname.example.com>` is the name of the host on which the rule applies.
- The section `(<run_as_user>:<run_as_group>)` defines the user or group as which the command is executed. If you omit this section, `<username>` can execute the command as root.
- `<path/to/command>` is the complete absolute path to the command. You can also limit the user to only performing a command with specific options and arguments by adding those options after the command path. If you do not specify any options, the user can use the command with all options. Multiple commands can be entered here, separated by `'`.

**Note:** You can apply the rule to all users, hosts, or commands by replacing any of these variables with `ALL`

**Warning:** By using `ALL` in some or multiple segments of a rule, can cause serious security risks.

You can negate the arguments by using the ! operator. For example, !root specifies all users except root. Note that allowing specific users, groups, and commands is more secure than disallowing specific users, groups, and commands. This is because allow rules also block new unauthorized users or groups.

**Warning:** Avoid using negative rules for commands because users can overcome such rules by renaming commands with the alias command.

The system reads the /etc/sudoers file from beginning to end. Therefore, if the file contains multiple entries for a user, the entries are applied in order. In case of conflicting values, the system uses the last match, even if it is not the most specific match.

To preserve the rules during system updates and for easier fixing of errors, enter new rules by creating new files in the /etc/sudoers.d/ directory instead of entering rules directly to the /etc/sudoers file. The system reads the files in the /etc/sudoers.d directory when it reaches the following line in the /etc/sudoers file:

```
#includedir /etc/sudoers.d
```

Note that the number sign (#) at the beginning of this line is part of the syntax and does not mean the line is a comment. The names of files in that directory must not contain a period and must not end with a tilde (~).

**Example**

```
linda   ALL=/usr/bin/passwd, ! /usr/bin/passwd root, /usr/bin/useradd, /usr/bin/usermod
```

Explanation: User `linda` can run the commands `passwd`, `useradd` and `usermod`, except run the command `passwd root` (not allowed to change the password of root user). Note the section `(<run_as_user>:<run_as_group>)` is omitted and the commands are executed as user root.

# Using ssh to connect to remote server

- The `sshd` service may need to be installed and enabled

```
Ubuntu: sudo apt install openssh-server
Redhat: sudo dnf install openssh-server; sudo systemctl enable --now sshd
```

- Install `ssh` client to access the `ssh` server (installed by default on Linux and MacOS)
- Use `scp` to copy files between laptop and server or between servers

[SSH Tutorial](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys)
