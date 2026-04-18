# Using cut and sort

`cut` filters columns of text files and `sort` sorts alphabetically (or nummerically when using `-n` option)

- `cut -d : -f 3 /etc/passwd | sort` filters 3rd column of file /etc/passwd (column delimiter is ":") en sorts alphabetically
- `cut -d : -f 3 /etc/passwd | sort -n` filters 3rd column of file /etc/passwd (column delimiter is ":") en sorts nummerically

# Using Regular Expression

- Regular expressions are text patterns
- **Always** put regex between single quotes
- Do not confuse with shell globbing
- Regex's are used in tools such as `grep`, `aws` and `sed`
- When searching text with a regex, then use `grep -E`

Regular Expression Tutorial: [RegexLearn](https://regexlearn.com/learn/regex101) (includes practices)

Regular Expression Cheatsheet: [https://regexlearn.com/cheatsheet](https://regexlearn.com/cheatsheet)

# Using tr

- `tr` translates sets of characters into another set of characters
- Useful for converting lowercase into uppercase and the other way around
- `echo hello | tr [:lower:] [:upper]`
- `echo hello | tr [a-z] [A-Z]`
- `echo hello | tr [a-n] [m-z]`

# An introduction to awk

- `awk` is useful for filtering text and print specific values only
- It has advanced features that make it into a scripting language
- Advanced features are not often used anymore, but `awk`can make complex tasks easier
- `awk '{print $0}' /etc/passwd` print all lines in /etc/passwd
- `awk 'length($0)>60' /etc/passwd` print the lines in /etc/passwd that are longer then 60 characters
- `awk -F : 'length($0)>60 {print $1}' /etc/passwd` print the first column of the lines in /etc/passwd that are longer then 60 characters
- `awk -F : '/student/ {print $1}' /etc/passwd` print the first column of the lines in /etc/passwd that matches the regex

[AWK tutorial](https://leapcell.medium.com/awk-basics-tutorial-5257e9bd9cb9)

# Getting started with sed

- `sed` is useful for searching, replacing, inserting and deleting text from the command line
- `sed -n 5p /etc/passwd` print the 5th line in file /etc/passwd
- `sed -i 's/old/new/g' text.txt` Replace in-line "old" with "new" for all occurences in a line (in-place = change file text.txt instead of sending to standard output)
- `sed -i 2d text.txt` Delete second line in file text.txt
- `for i in \*.txt; do sed -i 's/old/new/g' $i; done` Loop where in all files with extend "txt" word "old" is replaced with word "new"

[SED tutorial](https://www.digitalocean.com/community/tutorials/linux-sed-command)
