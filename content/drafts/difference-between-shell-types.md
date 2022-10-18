---
title: The difference between login, non-login, interactive and non-interactive shells
date: 2022-02-01
tags: []
draft: true
---

# She still doesn't know.

## Questions

* How is this distinguished by the OS?
* Is there a way for me to tell if I'm in a login/non-login interactive shell from my session?
  * It likely depends on the PID of the shell (if it's the first process under user, it's a login shell). You can also check the value of `$0` as in [this SO post][2]
* How do you tell the difference between an interactive/non-interactive shell?
  * [You can](https://tldp.org/LDP/abs/html/intandnonint.html) by checking for the existence of a prompt env var $PS1
* Can you distinguish between an interactive/non-interactive shell in the same way across all Linux distros?
* When do the profile/rc files run with respective to each combination of login/non-login interactive/non-interactive shells?
  * There is a limitation in calling bash from sh as in [this SO post][4]

## References

[1]: <https://unix.stackexchange.com/questions/50665/what-is-the-difference-between-interactive-shells-login-shells-non-login-shell> (SO answer to this question) 
[2]: <https://unix.stackexchange.com/questions/38175/difference-between-login-shell-and-non-login-shell> (Another SO answer) 
[3]: <https://tecadmin.net/difference-between-login-and-non-login-shell/> (Blog post on the differences)
[4]: <https://askubuntu.com/questions/766270/what-is-posix-compatible-mode-in-linux> (SO post about POSIX mode in bash)
