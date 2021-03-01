# macos enable italic fonts
You have to update your TERMINFO file.

Thanks to wincent's video and his github pages
Watch the video and look at his github pages, they're excellent.

I have the following note stored on my HD:

We can have italics in the terminal.

This works in iTerm as well as Terminal.

We have to adapt the terminfo database to tell it to display italics.

Create a plain text file which contains the following:

```
xterm-256color|xterm with 256 colors and italic,
  sitm=\E[3m, ritm=\E[23m,
  use=xterm-256color,
```
Save it as xterm-256color.terminfo.txt

Then execute the following command:
```
tic -o ~/.terminfo xterm-256color.terminfo.txt
```
This will create a ~/.terminfo/some_arbitrary_number/ directory, and inside that directory is a xterm-256color file.

What it does according to the manpage:
```
       The command tic translates a terminfo file from source format into com-
       piled  format.   The  compiled  format  is  necessary  for use with the
       library routines in ncurses(3X).
# install hack font for italic font
download hack font
double-click font file to install font into macos
       The results are  normally  placed  in  the  system  terminfo  directory
       /usr/share/terminfo.  There are two ways to change this behavior.

       First, you may override the system default by setting the variable TER-
       MINFO in your shell environment to a valid (existing) directory name.

       Secondly, if tic cannot get access to /usr/share/terminfo or your  TER-
       MINFO  directory,  it  looks for the directory $HOME/.terminfo; if that
       directory exists, the entry is placed there.

       Libraries that read terminfo entries are expected to check for  a  TER-
       MINFO  directory first, look at $HOME/.terminfo if TERMINFO is not set,
       and finally look in /usr/share/terminfo.

       -o dir   Write  compiled  entries to given directory.  Overrides the TER-
                MINFO environment variable.
```
So with the given command we are writing a new terminfo entry in the hidden ~/.terminfo directory. It takes the capabilities of the existing xterm-256color entry 
(from /usr/share/terminfo/) and adds italics mode to it.

# Addendum for tmux

tmux uses its own terminfo files, they also need to be updated to use italics.

    create a tmux.terminfo.txt file which contains


tmux|tmux terminal multiplexer,
  sitm=\E[3m, ritm=\E[23m,
  smso=\E[7m, rmso=\E[27m,
  use=screen,

    create a tmux-256color.terminfo.txt file which contains


tmux-256color|tmux with 256 colors,
  sitm=\E[3m, ritm=\E[23m,
  smso=\E[7m, rmso=\E[27m,
  use=screen-256color,

and run the tic command.

tic -o ~/.terminfo tmux-256color.terminfo.txt
and
tic -o ~/.terminfo tmux.terminfo.txt
