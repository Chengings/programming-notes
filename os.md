# Operating symtems

📚
 * [SUSE Linux Enterprise Server Documentation](https://documentation.suse.com/sles/15-SP1/html/SLES-all/index.html): Detailed documentations that  cover almost everything about Unix-like system. E.g. sudo, rsync, booting system, systemd, networking, file system, Apache HTTP server and Docker.
 * Filesystem Hierarchy Standard: https://refspecs.linuxfoundation.org/fhs.shtml and https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard


---

Linux, BSD and Unix systems, the encrypted credentials are stored in `/etc/shadow` or `/etc/master.passwd`.
Password in this file contains contains algorith ID, salt and hash ("$id$salt$hashed"). For example, `$1$s83Ugoff$EDT83WAAFpCQHWDp07E9Ux`. "$1$" is MD5, "$5$" is SHA-256 and "$6$" is SHA-512.

### Temporary folder https://en.wikipedia.org/wiki/Temporary_folder
* `/tmp` is for more temporary files and must be made available for programs that require temporary files.
* `/var/tmp`  is for persistent files (as it may be preserved over reboots) .
* `TMPDIR` for Unix and [POSIX][]. `TEMP`, `TEMPDIR` and `TMP` for non-POSIX.

[POSIX]: https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap08.html

## Raspberry Pi

📚
 * [Awesome Raspberry Pi](https://github.com/thibmaek/awesome-raspberry-pi)

`pinout`: a utility for querying Raspberry Pi GPIO pin-out information. https://raspberrypi.stackexchange.com/a/106645
