# Shell

⭐️ [Explain Shell](https://explainshell.com/)

⭐️ [ShellCheck](https://www.shellcheck.net/)

[Why is printf better than echo?](https://unix.stackexchange.com/a/65819)

Be careful about shebang (#!/usr/bin/env bash) https://unix.stackexchange.com/a/496960
> If the shebang is #!/bin/bash and you start the script as __./script the script will be executed by bash__. Absolutely no problem here.

> However, if you execute zsh ./script or __source it . ./script to the running zsh instance, it is quite common that the syntax of bash and zsh won't match.__

Use `command -v <cmd>` instead of `which` https://stackoverflow.com/a/677212

Use `basenc` to encode/decode base64-url https://man7.org/linux/man-pages/man1/basenc.1.html

Maximum bash's random number ($RANDOM) is 32767. Min is 0. [Bash's random.c](https://github.com/bminor/bash/blob/f3a35a2d601a55f337f8ca02a541f8c033682247/lib/sh/random.c#L98)

To disable shell history temporarily, open new terminal session and enter `unset HISTFILE`. https://www.gnu.org/software/bash/manual/html_node/Bash-History-Facilities.html
> If `HISTFILE` is unset, or if the history file is unwritable, the history is not saved.

📚
* [The Open Group Base Specifications Issue 8: POSIX.1-2024](https://pubs.opengroup.org/onlinepubs/9799919799/)
* https://en.wikipedia.org/wiki/List_of_Unix_commands
* https://en.wikipedia.org/wiki/List_of_GNU_Core_Utilities_commands
* https://www.gnu.org/software/bash/manual/html_node/index.html
* [The Linux man-pages project](https://www.kernel.org/doc/man-pages/) [Online man pages: man7.org](https://man7.org/linux/man-pages/index.html)[Debian Manpages](https://manpages.debian.org)
* [Command Line Interface Guidelines](https://clig.dev/#guidelines)

## POSIX

### Quoting

Single (') is **strong** quoting, what you see is what you get.

Double (") is **weak** quoting, allow certain characters to have a special meaning.

```sh
echo '$HOME'
# $HOME
echo "$HOME"
# /home/pi
echo "Don't forget"
# Don't forget
echo 'Warning! Missing keyword: "end"'
# Warning! Missing keyword: "end"

echo "My home directory is $HOME, and my account is $USER"
echo 'My home directory is '$HOME', and my account is '$USER
echo 'My home directory is '"$HOME"', and my account is '"$USER"
# My home directory is /home/pi, and my account is pi

echo "Next year is $(expr $(date +%Y) + 1)"     # Command substitution
```

### Parameter Expansion

[The Open Group's Parameter Expansion](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18_06_02), [GNU's Parameter Expansion](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html)

The basic form of parameter expansion is `${parameter}`.

Colon (:) tests **unset/null**. Omission of the colon tests unset only.

form | parameter is unset | parameter is set & not null | parameter is null | meaning
---- | ------------------ | --------------------------- | ----------------- | -------
${parameter?word} | error & exit | parameter | null | yell if undefined
${parameter-word} | word | parameter | null | use word (default) if undefined
${parameter=word} | word | parameter | null | redefine if undefined
${parameter+word} | null | word | word | change if parameter is defined
${parameter:?word} | error & exit | parameter | error & exit | yell if undefined/null
${parameter:-word} | assign word | parameter | word | use word (default) if undefined/null ⭐️
${parameter:=word} | assign word | parameter | assign word | use word if parameter is undefined/null
${parameter:+word} | null | word | null | use word (default) if parameter is defined and not null

```sh
${ME:-"A complex phrase with spaces, variables like $HOME or $(date)"}
${MAXUSERS:-$(cat /etc/passwd | wc -l)}      # Get value from /etc/passwd if MAXUSER is null/undefine.

echo ${ME:?}
# sh: ME: parameter not set
echo "${ME:?Please define ME}"                # Set standard error message if ME is null/undefined
```

#### Substring removal

https://wiki.bash-hackers.org/syntax/pe#substring_removal

**From the beginning (Prefix)**
`${parameter#[word]}` Remove smallest pattern
`${parameter##[word]}` Remove largest pattern

```sh
MYSTRING='Be liberal in what you accept, and conservative in what you send'
echo ${MYSTRING#*in}
 what you accept, and conservative in what you send

echo ${MYSTRING##*in}
 what you send
```

**From the end (Suffix)**
`${parameter%[word]}`   Remove smallest pattern
`${parameter%%[word]}`   Remove largest pattern

```sh
MYSTRING='Be liberal in what you accept, and conservative in what you send'
echo ${MYSTRING%in*}
Be liberal in what you accept, and conservative

echo ${MYSTRING%%in*}
Be liberal
```

**Common use**

Filepath manipulation
```sh
FILE="/home/user/example.tar.gz"

echo "${FILE##*/}"
example.tar.gz

echo "${FILE#*.}"
tar.gz

echo "${FILE##*.}"
gz

echo "${FILE%%.*}"
/home/user/example

echo "${FILE%.*}"
/home/user/example.tar

echo "${FILE%/*}"
/home/user
```

### Special Parameters

@: Expands to the positional parameters, starting from one. That is, `$@` is equivalent to `"$1" "$2" ….`

?: Expands to the decimal exit status of the most recent pipeline.
```sh
curl nohost.localhost
echo $?
> 6         # Exit status 6 means "Couldn't resolve host. The given remote host was not resolved."
```

📚
* https://wiki.bash-hackers.org/scripting/nonportable
* [POSIX.1-2017 Online Document](https://pubs.opengroup.org/onlinepubs/9699919799/)
* [POSIX Shell Tutorial](https://www.grymoire.com/Unix/Sh.html)

## Basic

### if

Basic syntax `if TEST-COMMANDS; then CONSEQUENT-COMMANDS; fi`

Alternate form uses square bracket with space `test TEST-COMMANDS; [ TEST-COMMANDS ]`

With elif and else `if test-commands; then consequent-commands; elif more-test-commands; then more-consequents; else alternate-consequents; fi`

If **TEST-COMMANDS** is executed and return status is **zero (0)** then CONSEQUENT-COMMANDS is executed.

Run `man [`  or `man test` to open **test** manual

```sh
if grep --quiet 'software' /usr/share/man/man1/mkdir.1; then echo 'Found "software"'; fi

one=1
if [ ${one} -eq 1 ]
then
	echo "One is ${one}"
else
	echo 'This is else'
fi

# Equivalent to above statement.
test ${one} -eq 1 && echo "One is ${one}" \
|| echo 'This is else'
```

### Loop

#### for
```sh
for name [ in [word ... ]]
# for name [ in "$@" ]
do
    compound-list
done
```

Exit Status: The exit status of a `for` command shall be the exit status of the last command that executes. If there are no items, the exit status shall be zero.

#### while

```sh
while compound-list-1
do
    compound-list-2
done
```
Execute "compound-list-2" as long as "compound-list-1" has an exit status of zero.

Exit status: The exit status of the `while` loop shall be the exit status of the last "compound-list-2" executed, or zero if none was executed.

```sh
while read dict_word
do
	touch "$dict_word"
done < /usr/share/dict/words
```

```sh
# Additional improvements
while IFS= read -r dict_word
do
	touch "$dict_word"
done < /usr/share/dict/words
```
Above command will crate a new file with the first field of each line moved to the end of the line. `read`[^read-util] will return non-zero exit status if end-of-file was detected or an error occurred.

For an improvement version:
- `read` wouldn't trim leading and trailing whitespace from each line if (un)set Internal Field Separator (IFS)[^shell_variables] to `IFS=`
- `read -r` is raw option to prevent backslashes from being interpreted as escape sequences.

📚
- [The Open Group's Compound Commands](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18_09_04)
- https://en.wikipedia.org/wiki/For_loop#1989:_Bash
- [Bash's Looping](https://www.gnu.org/software/bash/manual/html_node/Looping-Constructs.html)

### set

`set` to display the names and values of all shell variables. [The Open Group's set](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#set), [GNU's set](https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin.html#The-Set-Builtin)
```sh
set
# UID=1000
# USER=pi
# USERNAME=pi
# VENDOR=unknown
# VIRTUAL_ENV_DISABLE_PROMPT=12
# VISUAL=nano
```

`apropos` to search the "name" sections of all manual pages. Usually a wrapper for the `man -k`.
```sh
apropos copy
```

`command` and `type` to display the kind of a command
```sh
command -v tldr
# /usr/local/bin/tldr
command -V tldr
# tldr is /usr/local/bin/tldr
command -v brew-update
# alias brew-update='brew update; brew outdated'
command -V brew-update
# brew-update is an alias for brew update; brew outdated
command -v rs-shell
# alias rs-shell='exec $SHELL -l'
command -V rs-shell
# rs-shell is an alias for exec $SHELL -l

type tldr
# tldr is /usr/local/bin/tldr
type brew-update
# brew-update is an alias for brew update; brew outdated
type rs-shell
# rs-shell is an alias for exec /bin/zsh -l
```

Standard input (FD 0), standard output (FD 1) and standard error (FD 2). https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18_07

```sh
ls existing.txt no.file >export_ls.txt
ls existing.txt no.file 1>export_ls.txt
# Redirect FD 1 to the file "export_ls.txt". Error messages are _emitted_ on FD 2.
```

```sh
ls existing.txt no.file >export_ls.txt 2>/dev/null
# Redirect FD 1 to the file "export_ls.txt" and FD 2 to the file "/dev/null/"
```

```sh
# Redirecting standard output and standard error
ls existing.txt no.file >export_ls.txt 2>&1 # POSIX
ls existing.txt no.file &>export_ls.txt # Bash
# Make FD 1 target "export_ls.txt" and FD 2 target FD 1's target
```

```sh
read line <file.txt
```
Read[^read-util] from 'file.txt'

```sh
# Appending file redirection
echo Hello >~/world
echo World >>~/world
# Make FD x append to the end of file.
```

`tee` https://en.wikipedia.org/wiki/Tee_(command)
```sh
# Copies standard input to standard output and displays the standard input result.
ls -l /var/log | tee var-log.txt | less # by default, tee will overwrite/create the file.
date | tee -a log.txt # -a is append option
date | sudo tee date.txt log.txt
```
![Tee](assets/tee.svg)

heredoc `<<` uses to feed data to a program without storing it in an external file and must followed by any identifier. For example, mine is 'ichiwa'
```sh
cat <<ichiwa
I love you so much.
I know I am naive.
ichiwa
```

herestring `<<<` has same function as heredoc but without delimeter. Mostly use for one line command. Might not be in every shell but available in bash, ksh,
or zsh.
```sh
cat <<<'ha ha ha I know' # Equivalent to "echo 'ha ha ha I know' | cat"

cat <<<'I love you so much.
I know I am naive.'
```

`&` Run a job in the background
```sh
<command> &

<command>
# command is running
Ctrl-Z
```

`jobs` Show status of all jobs

`fg <job_id>` Bring a specific job to foreground

`bg <job_id>` Resume a specific job  and run it in the background

`xargs` stands for eXtended arguments. Construct	argument list(s) and execute utility. [The Open Group's xargs](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/xargs.html), [man7's xargs](https://man7.org/linux/man-pages/man1/xargs.1.html), [FreeBSD's xargs](https://www.freebsd.org/cgi/man.cgi?query=xargs&sektion=1)

```sh
# note: echo doesn't accept stdin, only string argument.
# use `xargs` to contruct string arguments and execute utility `echo` to print files in `/bin`.
ls /bin | xargs echo
# (I)nsert mode. Same result. Can be any options such as % {} _ ^
ls /bin | xargs -I % echo %
# limit maximum arguments to 4 per time
ls /bin | xargs -n 4 echo
# trace mode. Print the command line on the standard error before executing it.
ls /bin | xargs -t echo
# read text file as standard input and download file by using `curl -O`.
# -n limit argument to 1
# -P (non-POSIX) enable parallel mode. Set option to 0, xargs will run as many processes as possible simultaneously.
xargs -P 0 -n 1 curl -O <urls.txt
# > curl -O https://example.com/file1
# > curl -O https://example.com/file2
# > curl -O https://example.com/file3
```

Dot (.) is:
* Current directory https://en.wikipedia.org/wiki/Path_(computing)#Unix_style
* Execute commands in the current environment (Equivalent to `source`) https://en.wikipedia.org/wiki/Dot_(command) && another good explanation  https://unix.stackexchange.com/a/114306
* Hidden file and directory https://en.wikipedia.org/wiki/Hidden_file_and_hidden_directory#Unix_and_Unix-like_environments

Backslash (\\) is
* Escape character, it preserves the literal value of the next character that follows.
* Backlash pairs with newline \<newline> will be removed from the input stream and effectively ignored, so it is treated as a line continuation

[Brackets](https://www.assertnotmagic.com/2018/06/20/bash-brackets-quick-reference/)
* `( cmd1; cmd2; cmd3 )` single round brackets: a command list embedded between parentheses runs as a subshell.
* `$( cmd1 )` single dollar round brackets: [command substitution](https://en.wikipedia.org/wiki/Command_substitution)
* `(( expression ))` double round brackets: [Bash's shell arithmetic](https://www.gnu.org/software/bash/manual/html_node/Shell-Arithmetic.html). This one will return exit code only.
* `$(( expression ))` double dollar round brackets: [Bash's arithmetic expansion](https://www.gnu.org/software/bash/manual/html_node/Arithmetic-Expansion.html#Arithmetic-Expansion) similar shell arithmetic but this one will return output result, instead of exit code.
* `<( cmd1 )` angle round brackets: [process substitution](https://en.wikipedia.org/wiki/Process_substitution) allows the input or output of a command to appear as a file.
* `[ expression ]` single square brackets and `[[]]` double square brackets: [Bash's conditional Expressions](https://www.gnu.org/software/bash/manual/html_node/Bash-Conditional-Expressions.html#Bash-Conditional-Expressions) is an alternate version of the built-in `test`. Yes, `[` is a Bash shell command!!!
* `{ }` single curly brackets: [Bash's brace expansion](https://en.wikipedia.org/wiki/Bash_(Unix_shell)#Brace_expansion)


## Network

`ifconfig` display the link and address status of network interfaces
```sh
ifconfig  # list all information on all network devices
ifconfig en0 up # bring en0 (Ethernet) up
ifconfig en1 down # down en1 (Wi-fi)
```

`dig (domain information groper)` check dns record
```sh
dig wikipedia.org
dig +short wikipedia.org # look up the ip
dig @1.0.0.1 # check DNS records of "wikipedia.org" by "1.0.0.1"
```

`traceroute` print the route packets take to network host
```sh
traceroute wikipedia.org
traceroute -q 10 wikipedia.org # set the number of probes to 10 probes
```

![Image of Traceroute Diagram](assets/traceroute_diagram.webp)

## Brace Expansion

Brace expansion generates a set of alternative combinations. Generated results need not exist as files.


```sh
echo {I,want,my,money,back}
I want my money back

echo _{I,want,my,money,back}-
_I- _want- _my- _money- _back-

echo {5..12}
5 6 7 8 9 10 11 12

echo {01..10}
01 02 03 04 05 06 07 08 09 10

echo {c..k}
c d e f g h i j k

echo {A..C}{0..13}
A0 A1 A2 A3 A4 A5 A6 A7 A8 A9 A10 A11 A12 A13 B0 B1 B2 B3 B4 B5 B6 B7 B8 B9 B10 B11 B12 B13 C0 C1 C2 C3 C4 C5 C6 C7 C8 C9 C10 C11 C12 C13


# Bash 4
echo {0001..5}
0001 0002 0003 0004 0005

echo {1..10..2}
1 3 5 7 9

echo {10..1..2}
10 8 6 4 2
```

### Example
```sh
# Bulk download
wget http://docs.example.com/documentation/slides_part{1..6}.html

mkdir /usr/local/src/bash/{old,new,dist,bugs}

# Rename file
mv myText.{txt,tex}

# Create new backup file /some/file.txt.bak
cp /some/file.txt{,.bak}

# Repeating arguments
somecommand --{force,delete}

for i in {1..100}
do
   #do something 100 times
done
```

## Filenames and Pathnames in Shell: How to do it Correctly (   https://dwheeler.com/essays/filenames-in-shell.html)

```sh
# Basic rules

## Double-quote parameter (variable) references and command substitutions
"$file"
"$(pwd)"
"$(dirname "$file")"

## Prefix all globs so they cannot expand to begin with “-”
cat ./*                   # Use this, NOT "cat *" ... Must have 1+ files.
for file in ./* ; do      # Use this, NOT "for file in *" (beware empty lists)
...
done
```

## Filename and extension extraction (https://stackoverflow.com/a/965069)

```sh
FILE="example.tar.gz"

echo "${FILE%%.*}"
example

echo "${FILE%.*}"
example.tar

echo "${FILE#*.}"
tar.gz

echo "${FILE##*.}"
gz
```

## Home (https://en.wikipedia.org/wiki/Home_directory)
| OS | Path |
| -- | ---- |
| Android	| /data/media/userid |
| BSD/Linux | /home/username     |
| macOS	   | /Users/username    |

## Shell init (https://github.com/rbenv/rbenv/wiki/unix-shell-initialization#shell-init-files)

### Zsh
1. /etc/zshenv or /etc/zsh/zshenv (can't be overriden)
2. $ZDOTDIR/.zshenv
3. login mode:
   1. /etc/zprofile
   2. $ZDOTDIR/.zprofile
4. interactive:
   1. /etc/zshrc
   2. $ZDOTDIR/.zshrc
5. login mode:
   1. /etc/zlogin
   2. $ZDOTDIR/.zlogin

Opening a new Terminal or access via SSH (interacitve mode): $ZDOTDIR/.zshenv +  $ZDOTDIR/.zprofile + $ZDOTDIR/.zshrc

Log in shell: $ZDOTDIR/.zshenv +  $ZDOTDIR/.zprofile + $ZDOTDIR/.zshlogin

Executing a command remotely with ssh (e.g. `ssh remote_machine 'date'`) or run a shell script: $ZDOTDIR/.zprofile +  $ZDOTDIR/.zshenv

macOS and Linux have different meaning between graphical mode [^shell-modes], that means __`.zprofile`__ is a candidate place to put custom setting that required in any mode.

__Note from Zshdoc (https://zsh.sourceforge.net/Intro/intro_3.html)__
> `.zprofile` is similar to `.zlogin`, except that it is sourced before `.zshrc`.

> `.zlogin` is not the place for alias definitions, options, environment variable settings, etc.

[^shell-modes]: https://github.com/rbenv/rbenv/wiki/unix-shell-initialization#shell-modes

[^read-util]: https://pubs.opengroup.org/onlinepubs/9699919799/utilities/read.html

[^shell_variables]: https://pubs.opengroup.org/onlinepubs/009695399/utilities/xcu_chap02.html#tag_02_05_03
