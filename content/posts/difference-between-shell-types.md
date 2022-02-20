---
title: The difference between login, non-login, interactive and non-interactive shells
date: 2022-02-01
tags: []
---

# She still doesn't know.

## Questions

* How is this distinguished by the OS?
* Is there a way for me to tell if I'm in a login/non-login interactive shell from my session?
* How do you tell the difference between an interactive/non-interactive shell?
* [You can](https://tldp.org/LDP/abs/html/intandnonint.html) by checking for the existence of a prompt env var $PS1
* Can you distinguish between an interactive/non-interactive shell in the same way across all Linux distros?
* When do the profile/rc files run with respective to each combination of login/non-login interactive/non-interactive shells?

## References

* [SO answer to this question](https://unix.stackexchange.com/questions/50665/what-is-the-difference-between-interactive-shells-login-shells-non-login-shell)
* [Another SO answer](https://unix.stackexchange.com/questions/38175/difference-between-login-shell-and-non-login-shell)
* [Blog post on the differences](https://tecadmin.net/difference-between-login-and-non-login-shell/)