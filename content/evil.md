+++
title = "Evil Mode"
date = 2020-01-10T09:00:00Z
+++

As an Emacs beginner, I would like to learn Emacs's key bindings while change to vim's key bindings occasionally when I get stuck. So this is my settings for now, when I have deeper understanding of how Emacs & evil-mode works latter, I maybe change this settings for more typing effeciency.

# What is Evil Mode
Evil Mode is the extensible vi layer for Emacs. If you already known vim's key bindings, you would likely want to try it in Emacs. Home Page is [Here][0].

# Install Evil Mode
Install `evil` package from MELPA. See the [official documentation][1] for installation instructions. 

# Basic Usage
The goal is to enable Evil Mode, but set default state to `emacs` state.

Goto menubar: `Option` - `Customize Emacs` - `Specific Option` (or use `M-x customize-option`) to set `evil-mode` to `on` and set `evil-default-state` to `emacs`. 

This will add following two lines to your Emacs's `init.el`.
```
;; below (custom-set-variables
 '(evil-default-state (quote emacs))
 '(evil-mode t)
```

Now when I need goto `evil` state, I can press `C-z` to change to evil state and then happily using vim's key bindings. Another `C-z` will change state back to `emacs`.

# TODO: How to show evil state in powerline?
I have customized my emacs interface with powerline with basic setup. the evil-mode state didn't show up. How can improve this?

# TODO: What are other key bindings evil-mode generated besides `C-z`?
`C-h k C-z` gives me `C-z` is bounded to `evil-exit-emacs-state` command, what are other key bindings?

# TODO: Try evil-mode somewhere else other than editing
Evil-Mode can be used elsewhere other than editing, like `Dired`, `Org-Mode` etc., apparently a lot of work of remapping key bindings will be needed. How to do that in an elegant way? 

[0]: https://github.com/emacs-evil/evil
[1]: https://evil.readthedocs.io/en/latest/overview.html#installation-via-package-el
