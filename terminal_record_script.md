# script

`/usr/bin/script` - záznam prace v příkazové řádce

```
Usage:
 script [options] [file]

Make a typescript of a terminal session.

Options:
 -I, --log-in <file>           log stdin to file
 -O, --log-out <file>          log stdout to file (default)
 -B, --log-io <file>           log stdin and stdout to file

 -T, --log-timing <file>       log timing information to file
 -t[<file>], --timing[=<file>] deprecated alias to -T (default file is stderr)
 -m, --logging-format <name>   force to 'classic' or 'advanced' format

 -a, --append                  append to the log file
 -c, --command <command>       run command rather than interactive shell
 -e, --return                  return exit code of the child process
 -f, --flush                   run flush after each write
     --force                   use output file even when it is a link
 -E, --echo <when>             echo input (auto, always or never)
 -o, --output-limit <size>     terminate if output files exceed size
 -q, --quiet                   be quiet

 -h, --help                    display this help
 -V, --version                 display version

For more details see script(1).
```

Možné použití (prikald z upgrade Debian bullseye -> bookworm):

## 4.4.1. Recording the session
It is strongly recommended that you use the `/usr/bin/script` program to record a transcript of the upgrade
session. Then if a problem occurs, you will have a log of what happened, and if needed, can provide exact 
information in a bug report. To start the recording, type:

```
# script -T ~/upgrade-bookworm-<step>.time -a ~/upgrade-bookworm-<step>.script
```    
or similar. If you have to rerun the typescript (e.g. if you have to reboot the system) use different **step** 
values to indicate which step of the upgrade you are logging. Do not put the **typescript** file in a temporary 
directory such as `/tmp` or `/var/tmp` (files in those directories may be deleted during the upgrade or during 
any restart).

The **typescript** will also allow you to review information that has scrolled off-screen. If you are at the 
system's console, just switch to **VT2** (using `Alt+F2`) and, after logging in, use 
`less -R ~root/upgrade-bookworm.script` to view the file.

After you have completed the upgrade, you can stop **script** by typing `exit` at the prompt.

**apt** will also log the changed package states in `/var/log/apt/history.log` and the terminal output in 
`/var/log/apt/term.log`. **dpkg** will, in addition, log all package state changes in `/var/log/dpkg.log`. 
If you use aptitude, it will also log state changes in `/var/log/aptitude`.

If you have used the `-T` switch for **script** you can use the **`scriptreplay`** program to replay the whole 
session:

```
# scriptreplay ~/upgrade-bookwormstep.time ~/upgrade-bookwormstep.script
```
