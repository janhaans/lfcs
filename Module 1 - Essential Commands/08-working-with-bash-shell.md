# Using I/O direction and piping

- Standard input (0) `<` - from keyboard, file; not often used
- Standard output (1) `>` - to screen, file (overwrite)
- Append `>>` - to file
- Standard error `2>` - to screen, `/dev/null`, error file
- Standard output AND standard error `&>` - to screen, file

- A pipe is used to pipe the output of one command as the input for a second command, for example:

```
ps aux | grep httpd
```

- `tee` is a combination of redirection and piping. In example below the output of `ps` command is redirected to file `psfile` and piped to command `grep`

```
ps aux | tee psfile | grep httpd
```

# Working with history

- Commands a user type are written to history file `~/.bash_history` when you close the terminal window or logout
- `history -c` clear current history
- `history -w` overwrites the entire history file with the current session's history
- `history -a` appends new lines from the current session to the end of the history file
- `history -d <line number>` deletes line number form the current session's history
- `!<line number>` repeats command at line number in history file

- `last` shows list of when you last logged in

# Using command line completion

- Use [Tab]-key for command line completion of commands,variables and files
- When the first [Tab]-key does not complete then there are multiple options which will be listed when you do a second [Tab]-key
- Install the bash completion package for additional completion features

# Using variables

```
VARNAME=value  // define variable varname
echo $VARNAME  // read variable varname
```

- Variable names are case-sensitive. It is recommended to use uppercase for variable names
- By default variable are only visible to the current shell. Use `export` to make a variable visible to subshells:

```
export VARNAME=value
```

- Use `env` to list all the (environment) variables of current shell
- `PATH` variable list all directories for which Linux will search for commands

# Using other bash features

- Use `alias` to define custom commands
- Custom commands are defines in bash startup files: `/etc/profile`
- `alias` shows all custom commands
- `alias listing='ls'` define command `listing`
- `unalias listing` removes command `listing`

**Bash keyboard shortcuts**

- `Ctrl-l` clear screen
- `Ctrl-u` wipe current command line
- `Ctrl-a` move to beginning of line
- `Ctrl-e` move to end of line
- `Ctrl-d` interrupt current process
- `Ctrl-x` exit shell

# Working with bash startup files

- `/etc/environment` contains a list of variables and is the first file processed in bash startup (empty in Redhat)
- `/etc/profile` is startup script which is executed while users login (**do not change this file** but add your customizations in a separate script in directory 'etc/profile.d`)
- `/etc/profile.d` is directory with additional startup scripts which are executed while users login
- `~/.bash_profile` is user specific startup script which is executed while user login
- `~/.bash_logout` is user specific logout script which is executed while user logout
- `~/.bashrc` is user specific startup script which is executed when user starts a new subshell

When you have changed a bash startup scripts you execute them by logging out and in or use the `source` command:

```
source /etc/profile.d/<name startup script>.sh
source ~/.bashr
```
