# enable terminal color theme
Edit your .bash_profile (since OS X 10.8) — or (for 10.7 and earlier): .profile or .bashrc or /etc/profile (depending on availability) — in your home directory and add following code:
```
export CLICOLOR=1
```
CLICOLOR=1 simply enables coloring of your terminal.

LSCOLORS=... specifies how to color specific items. 

# second way Recommanded using the default color
find the the bash config file
add
```
alias ls = 'ls --color=auto'
```
