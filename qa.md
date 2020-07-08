# Question & Answer

**Q: Can't login to macOS's Screen Sharing?**

A: `pkill loginwindow`

**Q: When to use parallel (`fd -x` or `GNU Parallel`)?**

A: Expecting outputs as a new format such as convert png to jpg.
Dealing with same format such as rename file name, use `for input in <pattern>; do <cmd> "$input";done` will be safer.

**Q: Zsh's autocomplete doesn't work?**

A: Just remove `~/.zcompdump*`. https://github.com/ohmyzsh/ohmyzsh/issues/518#issuecomment-356978957
