---
title: Fast refreshing files on Windows when running React on WSL
date: 2022-05-24
tags: [react, web, development, fast, refresh, windows, wsl]
---

I ran into some trouble where React fast refresh stopped working when I ran a devcontainer on Windows. If I mounted my devcontainer on a Windows file path, fast refresh stopped working; however, if I mounted the devcontainer on a path in WSL 2, React fast refresh _did_ work.

First of all, running a devcontainer on the Windows filesystem with WSL 2 negatively impacts performance. Running the React development server in the devcontainer when mounted to a WSL 2 path was so much faster than on Windows (a few seconds vs 2 mins) - so there is at least that benefit.

It's still unclear why fast refresh stopped working when the devcontainer was running on Windows.

<!-- References -->
[1]: <https://gist.github.com/Jarred-Sumner/1f13f48c12e84a7d9a05365018834475> (How React Fast Refresh works)
[2]: <https://www.reddit.com/r/nextjs/comments/p6d6fj/fast_refresh_not_working_when_using_docker_and/> (Reddit post about fast refresh not working)

<!-- Questions and comments - refer to IDs with QC prefix

1. Find out why fast refresh didn't work when devcontainer was running on Windows
-->

