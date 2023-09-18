# Operating systems

📚
 * [SUSE Linux Enterprise Server Documentation](https://documentation.suse.com/sles/15-SP1/html/SLES-all/index.html): Detailed documentations that  cover almost everything about Unix-like system. E.g. sudo, rsync, booting system, systemd, networking, file system, Apache HTTP server and Docker.
 * [The Linux kernel user’s and administrator’s guide](https://www.kernel.org/doc/html/latest/admin-guide/index.html): The following is a collection of user-oriented documents that have been added to the kernel.org over time. There is, as yet, little overall order or organisation here — this material was not written to be a single, coherent document!
 * Filesystem Hierarchy Standard: https://refspecs.linuxfoundation.org/fhs.shtml and https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard
 * The Linux Kernel documentation: https://www.kernel.org/doc/html/latest/index.html

---

Linux, BSD and Unix systems, the encrypted credentials are stored in `/etc/shadow` or `/etc/master.passwd`.
Password in this file contains contains algorith ID, salt and hash ("$id$salt$hashed"). For example, `$1$s83Ugoff$EDT83WAAFpCQHWDp07E9Ux`. "$1$" is MD5, "$5$" is SHA-256 and "$6$" is SHA-512.

### Temporary folder & shared memory
* `/tmp` is for more temporary files and must be made available for programs that require temporary files.
* `/var/tmp`  is for persistent files (as it may be preserved over reboots) .
* `TMPDIR` for Unix and [POSIX](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap08.html). `TEMP`, `TEMPDIR` and `TMP` for non-POSIX.
* `/dev/shm` is a system-wide shared memory in the form of a [RAM disk](https://en.wikipedia.org/wiki/RAM_disk)Debian uses tmpfs [^wiki_tmpfs][^kernel_tmpfs] for `/dev/shm` and `/run`

Some system doesn't have `TMPDIR`, to use in shell script try this `"${TMPDIR:-/tmp}"`  

```
┌───────────┬──────────────┬────────────────┐
│ /dev/shm  │ always tmpfs │ Linux specific │
├───────────┼──────────────┼────────────────┤
│ /tmp      │ can be tmpfs │ FHS 1.0        │
├───────────┼──────────────┼────────────────┤
│ /var/tmp  │ never tmpfs  │ FHS 1.0        │
└───────────┴──────────────┴────────────────┘
```

 https://en.wikipedia.org/wiki/Temporary_folder
 https://en.wikipedia.org/wiki/Shared_memory
 [Appropriate use of various tmp directories](https://superuser.com/a/1030777)

## Raspberry Pi

📚
 * [Official Documentation](https://www.raspberrypi.com/documentation/)
 * [My Raspberry Pi OS cheat sheet](https://gist.github.com/Chengings/48e18165244e03a6eb0c3cdaadaf82b7#file-raspios-sh)
 * [Awesome Raspberry Pi](https://github.com/thibmaek/awesome-raspberry-pi)
 * [The Raspberry Pi Guide for scientists and anyone else](https://raspberrypi-guide.github.io/)

`pinout`: a utility for querying Raspberry Pi GPIO pin-out information. https://raspberrypi.stackexchange.com/a/106645

### Set DNS Servers

Add `static domain_name_servers=1.2.3.4 5.6.7.8` to `/etc/dhcpcd.conf` file and restart dhcpd service by using `sudo systemctl restart dhcpcd.service`. [Configuring Networking](https://www.raspberrypi.com/documentation/computers/configuration.html#static-ip-addresses)

## macOS

### Agents and Daemons

Daemons are managed by launchd on behalf of the OS in the system context, which means they are unaware of the users logged on to the system. Daemons are strictly background processes that respond to low-level requests.

Agents are managed by launchd, but are run on behalf of the currently logged-in user (that is, in the user context). Agents can communicate with other processes in the same user session and with system-wide daemons in the system context.


#### Launch Criteria

 * change to file system object: WatchPaths 
 * periodic: StartInterval
 * wall time: StartCalendarInterval

	
#### Launch behaviour 

run purely on demand:
 * KeepAlive = false (default)
 * RunAtLoad = false (default)

run once when loaded and thence on demand 
 * KeepAlive = false (default)
 * RunAtLoad = true

#### Required property list keys

 * Label: Contains a unique string that identifies your daemon to launchd.
 * ProgramArguments: Contains the arguments used to launch your daemon.


#### Running a Job Periodically

The following example creates a job that is run shell script every 30 minutes (1800 seconds).

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">

<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>my.name.gitpull</string>

    <key>Program</key>
    <string>/Users/name/scripts/git-pull.sh</string>

    <key>StartInterval</key>
    <integer>1800</integer>

    <key>StandardErrorPath</key>
    <string>/tmp/my.name.gitpull.stderr.log</string>
  </dict>
</plist>
```

The following example starts the brew's update job at 12:09 AM. Like the Unix cron subsystem, any missing key of the StartCalendarInterval dictionary is treated as a wildcard - in this case, the day is omitted, so the job is run every day.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">

<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>my.name.update.brew</string>

    <key>ProgramArguments</key>
    <array>
      <string>/usr/local/bin/brew</string>
      <string>update</string>
    </array>

    <key>StartCalendarInterval</key>
    <array>
      <dict>
        <key>Hour</key>
        <integer>0</integer>
        <key>Minute</key>
        <integer>9</integer>
      </dict>
    </array>
  </dict>
</plist>
```

#### Monitoring a Directory

The following example starts the job whenever any of the paths being watched have changed.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">

<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>my.name.localdict</string>
    
    <key>WatchPaths</key>
	  <array>
      <string>/Users/name/Library/Spelling/LocalDictionary</string>
	  </array>

    <key>ProgramArguments</key>
    <array>
      <string>cp</string>
      <string>/Users/name/Library/Spelling/LocalDictionary</string>
      <string>/Users/name/BACKUP/LocalDictionary.txt</string>
    </array>
  </dict>
</plist>
```

#### Effects of Sleeping and Powering Off

If you schedule a `launchd` job by setting the `StartCalendarInterval` key and the computer is **asleep** when the job should have run, your **job will run when the computer wakes up**.

All other `launchd` jobs are skipped when the computer is turned off or asleep; they will not run until the next designated time occurs.

Consequently, if the computer is always off at the job’s scheduled time, both `cron` jobs and `launchd` jobs never run. For example, if you always turn your computer off at night, a job scheduled to run at 1 A.M. will never be run.

#### Load, Unload, Debug, Enable and Disable
```shell
launchctl load -w ~/Library/LaunchAgents/my.name.gitpull.plist

launchctl print gui/501/my.name.gitpull.plist

launchctl list my.name.gitpull

launchctl enable my.name.gitpull

launchctl disable my.name.gitpull

launchctl unload -w ~/Library/LaunchAgents/my.name.gitpull.plist

# List non-apple daemon services

launchctl list | grep -v com.apple | sort --key 3
```

**References**
* https://developer.apple.com/library/archive/technotes/tn2083/_index.html#//apple_ref/doc/uid/DTS10003794
* https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/Introduction.html#//apple_ref/doc/uid/10000172i-SW1-SW1
* https://www.launchd.info/
* `man launchd.plist` `man launchd` `man launchctl`

[^kernel_tmpfs]: https://www.kernel.org/doc/Documentation/filesystems/tmpfs.txt
[^wiki_tmpfs]: https://en.wikipedia.org/wiki/Tmpfs