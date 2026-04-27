# Using a Text Editor

Edit text files with **nano** or **vim**. Nano has a beginner-friendly user-interface but learn and use vim, because this text editor is very powerfull.

To setup your favourite text editor as the default use: `export EDITOR=$(which vim)`

Ubuntu is the only Linux distribution where by default vim is not installed. Install vim manually on Ubuntu: `sudo apt install vim`

vim has a very usefull tutorial **vimtutor** which you access by the command: `vimtutor`

# Browsing Text Files

- `more` first pager
- `less` more advanced pager

# Using head and tail to see File Start and End

- `head -10 /etc/passwd` first 10 lines
- `tail -10 /etc/passwd` last 10 lines
- `head -3 /etc/passwd | tail -1` 3rd line
- `sudo tail -f /var/log/messages/` watch the last lines (online updated)

# Displaying File Contents with cat and tac

`cat` has some nice options:

- `-A` shows all non-printable characters
- `-b` numbers lines
- `-n` numbers lines except empty lines5
- `-s` suppress repeated empty lines

`tac` is like `cat` but in reverse order and without the nice options

# Working with grep

- `grep linda *` list all files in current directory and lines that have the text linda
- `grep linda /etc/passwd` list all lines in file /etc/passwd that have the text linda
- `sudo grep linda /etc/* 2>/dev/null` suppress error messages
- `ps aux | grep httpd | grep -v grep` search for httpd process and exclude grep process searching for httpd

`grep` options:

- `-i` ignore case
- `-v` show all lines that do not contain pattern
- `-l` list filenames that contain pattern, without showing matching lines
- `-A5` show line that matches the pattern as well as the 5 lines after
- `-B5` show line that matches the pattern as well as the 5 lines before
- `-C5`combined -A5 and -B5
- `-R`recursively search pattern
- `-E` use extended regular expression
