# Question & Answer

__Q: Can't login to macOS's Screen Sharing?__

A: `pkill loginwindow`

__Q: When to use parallel (`fd -x` or `GNU Parallel`)?__

A: Expecting outputs as a new format such as convert png to jpg.
Dealing with same format such as rename file name, use `for input in <pattern>; do <cmd> "$input";done` will be safer. __Create backup will be safest choice__

__Q: Zsh's autocomplete doesn't work?__

A: Just remove `~/.zcompdump*`. https://github.com/ohmyzsh/ohmyzsh/issues/518#issuecomment-356978957

__Q: I can't use `source` inside cron?__

A: By default, cron runs in `/bin/sh` which doesn't have `source` unless you specfic SHELL environment variable in cron to `bin/bash`, or use `.`(sh POSIX standard). Furthermore, if your script is executable (x) you don't need to put `.` or `source`, just execute it `* * * * * ~/executable.sh`

__Q: Where is cron log?__

A: In Debian, check `/var/log/syslog`. None for Darwin.

**Q: HDMI doesn't work on macOS**

A: [Reset NVRAM](https://support.apple.com/HT204063) via this command `Option + Command + P + R`. https://forums.macrumors.com/threads/hdmi-port-no-longer-working-after-update-to-macos-11-big-sur.2268966/page-5?post=30857888#post-30857888
