# Question & Answer

__Q: Can't login to macOS's Screen Sharing?__

A: `pkill loginwindow`

__Q: When to use parallel (`fd -x` or `GNU Parallel`)?__

A: When expecting outputs in a new format, such as convert PNG to JPG. However, when dealing with same format, such as renaming files, it is safer to use `for input in <pattern>; do <cmd> "$input"; done` . __Creating a backup will be the safest choice__

__Q: Zsh's autocomplete doesn't work?__

A: Just remove `~/.zcompdump*`. https://github.com/ohmyzsh/ohmyzsh/issues/518#issuecomment-356978957

__Q: I can't use `source` inside cron?__

A: By default, cron runs in `/bin/sh` which doesn't have `source` unless you specfic SHELL environment variable in cron to `bin/bash`, or use `.`(sh POSIX standard). Furthermore, if your script is executable (x) you don't need to put `.` or `source`, just execute it `* * * * * ~/executable.sh`

__Q: Where is cron log?__

A: In Debian, check `/var/log/syslog`. None for Darwin.

**Q: HDMI doesn't work on macOS**

A: [Reset NVRAM](https://support.apple.com/HT204063) via this command `Option + Command + P + R`. https://forums.macrumors.com/threads/hdmi-port-no-longer-working-after-update-to-macos-11-big-sur.2268966/page-5?post=30857888#post-30857888

**Q: rsync - protocol version mismatch -- is your shell clean**

A: This issue arises from startup scripts executed on remote shell facilities that generate unwanted output, which confuses the rsync command. 
https://www.suse.com/support/kb/doc/?id=000021212
```shell
ssh user@remoteip true > debug.txt
cat debug.txt
grep -Ril "<debug_output>" .
```

**Q: How to get the tilde (~) to work correctly in macOS**

A: Remove `/Library/Preferences/com.apple.keyboardtype.plist`. https://gist.github.com/nezticle/871091a41ce322e81be947d83a5e4a86

