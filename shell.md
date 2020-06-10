# Shell

⭐️ [Explain Shell](https://explainshell.com/)

## Basic

`apropos` to search the "name" sections of all manual pages. Usually a wrapper for the `man -k`.
```
apropos copy
```

`type` to display the kind of a command
```
type tldr
# tldr is /usr/local/bin/tldr
type brew-update
# brew-update is an alias for brew update; brew outdated
type rs-shell
# rs-shell is an alias for exec /bin/zsh -l
```

Standard input (FD 0), standard output (FD 1) and standard error (FD 2)

```
ls existing.txt no.file >export_ls.txt
ls existing.txt no.file 1>export_ls.txt
# Redirect FD 1 to the file "export_ls.txt". Error messages are _emitted_ on FD 2.
```

```
ls existing.txt no.file >export_ls.txt 2>/dev/null`
# Redirect FD 1 to the file "export_ls.txt" and FD 2 to the file "/dev/null/"
```

```
# Redirecting standard output and standard error
ls existing.txt no.file >export_ls.txt 2>&1
ls existing.txt no.file &>export_ls.txt
# Make FD 1 target "export_ls.txt" and FD 2 target FD 1's target
```

`read line <file.txt`
Read from 'file.txt'

```
# Appending file redirection
echo Hello >~/world
echo World >>~/world
# Make FD x append to the end of file.
```

Run a job in the background
```
<command> &

<command>
# command is running
Ctrl-Z
```

Show status of all jobs

`jobs`

Bring a specific job to foreground

`fg <job_id>`

Resume a specific job  and run it in the background

`bg <job_id>`

---
## Network

`ifconfig` display the link and address status of network interfaces
```
ifconfig  # list all information on all network devices
ifconfig en0 up # bring en0 (Ethernet) up
ifconfig en1 down # down en1 (Wi-fi)
```

`dig (domain information groper)` check dns record
```
dig wikipedia.org
dig +short wikipedia.org # look up the ip
dig @1.0.0.1 # check DNS records of "wikipedia.org" by "1.0.0.1"
```

`traceroute` print the route packets take to network host
```
traceroute wikipedia.org
traceroute -q 10 wikipedia.org # set the number of probes to 10 probes
```

![Image of Traceroute Diagram](assets/traceroute_diagram.webp)
---
## Brace Expansion

Brace expansion generates a set of alternative combinations. Generated results need not exist as files.


```
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
```
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
