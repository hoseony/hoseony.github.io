---
layout: default
title: tmux
permalink: /notes/dotfiles/tmux
---

[← ../dotfiles](../dotfiles)

## tmux

Tmux might be one of the coolest additions to your workflow. It allows you to switch between several terminals easily, and it is highly customizable. Also, you can split screens (and more)!

I will be going over a few things that you might want if you decide to use it (I highly recommend this).

The default prefix for every command in tmux is ```ctrl + b```. I recommend changing the prefix. \\
To change this, you need to make ```.tmux.conf``` file. 

```c
# remap prefix from 'C-b' to 'C-a'
unbind 'C-b'
set -g prefix 'C-a'
bind 'C-a' send-prefix
```
I use ```ctrl + a```, but choose a key binding that you can comfortably use, as this is used very frequently.

Another powerful feature of tmux is the ability to split the screen. You can take a look at [this website](https://tmuxcheatsheet.com/). However, without changing the key binding, it is very painful and unintuitive.

```c
unbind '%'
unbind '"'
unbind '-'
bind '-' splitw -v -c "#{pane_current_path}"
bind '\' splitw -h -c "#{pane_current_path}"
bind '_' splitw -vb -c "#{pane_current_path}"
bind '|' splitw -hb -c "#{pane_current_path}"
```

To make tmux more aesthetic (since why not), I am currently using [tmux2k](https://github.com/2KAbhishek/tmux2k). To use this, you need [TPM](https://github.com/tmux-plugins/tpm), and in general it will make your life easier. Note that the key binding ```prefix + I``` is capitalized.

There are many miscellaneous things that will improve your tmux. You can find more in my [GitHub repo](https://github.com/hoseony/dotfiles_chezmoi/blob/main/dot_tmux.conf) if you wish. Also, in general, I recommend taking a look at other people's dotfiles on GitHub.

```c
set -g mode-keys vi
set -g monitor-activity on
set-option -sg escape-time 10
set -g aggressive-resize on
set -g base-index '1'
set -g focus-events on
set -g pane-base-index '1'
```
