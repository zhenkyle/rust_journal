+++
title = "Change color"
date = 2020-01-10T15:00:00Z
+++

Followed this interesting video blog: [Switching to GNU Emacs][1], I changed my Emacs's color to [Dracula theme][2], my Emacs looks more like a morden text editor now.

# What is Dracula theme
Dracula theme is a dark theme for Emacs.

# Install
Install `dracula-theme` from MELPA

## Using Customize to change theme
Goto menubar: `Options` - `Customize Emacs` - `Customize Theme`, select `dracula` theme ,then click `Save Theme Settings`.

This will add the following line to you `init.el`.
```
;; under (custom-set-variables
 '(custom-enabled-themes (quote (dracula)))
```

## Another way to change theme
Another way to change theme is manually add the following line to your `init.el`:
```
(load-theme 'dracula t)
```

# Tweak Emacs
As I learned from [Switching to GNU Emacs][1], I can further tweak Emacs to have a more professional look.

## Add Relative Line numbers
Goto menubar `Options` - `Show/Hide` - `Line Number for All Lines`, check `Relative Line Numbers`.

To make above option persistent, you must click menubar `Options` - `Save Options (Save options set from menu above)`, this will add following two lines to your `init.el`.

```
;; under (custom-set-variables
 '(evil-default-state (quote emacs))
 '(global-display-line-numbers-mode t)
```

## Hide toolbar
Click menubar `Options`-`Show/Hide`-`Tool bar`- `None`.

Click menubar `Options` - `Save Options (Save options set from menu above)` to make it persistent.

To tun on toolbar temporarily, use `M-x tool-bar-mode`.

## Hide scorllbar
Click menubar `Options`-`Show/Hide`-`Scroll bar`- `No Vertical Scroll Bar`, and save options.

To tun on scrollbar temporarily, use `M-x scroll-bar-mode`.

## Hide menubar
Click menubar `Options`-`Show/Hide`-`Menu Bar`, and save options.

To tun on menubar temporarily, use `M-x menu-bar-mode`.

# TODO: tweak fonts
After apply `Dracula theme`, The fonts in my setting is not exactly like the screenshot in `Dracula theme`'s home page. How to change fonts? Are there any recommendations?

[1]: https://www.youtube.com/watch?v=Y8koAgkBEnM
[2]: https://draculatheme.com/emacs/
