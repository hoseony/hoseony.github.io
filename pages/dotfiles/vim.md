---
layout: default
title: vim
permalink: /notes/dotfiles/vim
---

[← ../dotfiles](../dotfiles)

## Thoughts about vim / nvim

### Why would you ever consider using vim / nvim?
For me, it was an easy decision. I liked the idea that I do not need to constantly move my hands away from the keyboard while programming. Another reason was customization. Vim and Neovim make it easy to shape the editor around how you actually work, instead of adapting yourself to a fixed interface. This is something I discovered recently, but being able to work comfortably without relying on a GUI is also a surprisingly useful skill.

I am not arguing that it is better than modern IDEs like VS Code, but it is definitely something worth trying at least once.

### vim or nvim?
At the current stage, I mostly use nvim because I got tired of using vimrc while the general community has been shifting to nvim. It is not necessarily easier than vimscript, but its plugin ecosystem is much larger and more actively maintained.

Generally, there are two ways to approach Neovim: building a configuration from scratch or starting from a preset. I do not think one is universally better than the other.

At the moment, I keep two Neovim setups: one built on top of NvChad and another minimal configuration with only the features I use regularly. If you do not want to spend much time setting up Neovim yourself, starting from a preset is a perfectly reasonable choice. It gives you a modern environment immediately, with many common features already integrated.

The tradeoff is that you first need to understand and learn the decisions someone else has already made. Personally, I find starting from scratch more useful. It lets me add only what I actually need. When I feel that something is missing, I look for a plugin or write a small adjustment and add it, which makes more sense to me.

You can check my vim config. I have used Vim for more than a year with that configuration at this point, and it does fit my needs. However, the plugin manager in Vim just does not come close to modern nvim plugin managers such as Lazy.
