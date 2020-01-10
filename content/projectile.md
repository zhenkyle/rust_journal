+++
title = "Projectile"
date = 2020-01-16T15:00:00Z
+++

[Projectile][1] is a popular project interaction library for Emacs. Here is it's official [documentation][2].

# Overview

Project means a groups of files together, especially code, accroding to the [EmacsWiki CategoryProject][3] page. 
Different project management libraries have different views of projects. 
As far as I know, a project will always have a root directory in which contains all project files.
There are many Projectile alternatives,including CEDET, which seem like came out earlier and more advanced, 
but I haven't tried it yet. 
EmacsWiki recommends it is probably not useful to use both of them at the same time, for the same project. 
So I decided to try Projectile first.

My basic understanding of project management came from Sublime text. 
The feature I wanted most is the ability to goto anything in a project very quickly and search anything very quickly.
Let's see how to install and use Projectile with these two questions in mind.

# Install

Install `projectile` package from MELPA. Add the following lines to your `init.el` is good enough for me to go.
```
(projectile-mode +1)
(define-key projectile-mode-map (kbd "s-p") 'projectile-command-map)
(define-key projectile-mode-map (kbd "C-c p") 'projectile-command-map)
(setq projectile-completion-system 'helm)
```

Note:
1. the first line enables Projectile mode, it is the same as `projectile-global-mode` but the latter is deprecated.
2. The second line defines `s-p` as Projectile's keymap prefix, `s` means `Super` key here.
3. the third line defines another keymap prefx `C-c p`, in case of you don't have a usable `Super` key.
4. the last line change projectile's completion system from the default `ido` to `helm`, of course I happened have `helm` package insalled. `helm` is easy to configure for basic usage, but that's another story for another time.

    Enable `helm` as completion system is different than install the [helm-projectile][4] package. The latter which is also writen by Projectile's author offers a second level of intergration with `helm`, but I decided not to install it right now, becourse it seems like less maintained by the author and will add complexity. This [indepth post][5] explained how `helm-projectile` works, it should be readed before you try.

## Enable `s-p` key bindings on Gnome desktop

I can use `s-p` on my Chrome book without any problem, the `Super` key on Chrome book is the magnifying glass key, however I can't use `s-p` key bindings on my Arch Linux Gnome desktop, because `Super`+`p` key is alread taken by Gnome.

After found [this post][6], I realized `Super + p` is bounded to "Switch monitor" in Gnome. Go in the dconf-editor via the command "dconf-editor" in a terminal, then go at:
```
/org/gnome/mutter/keybindings/switch-monitor
```
and disable "use default value" and delete:
```
'<Super>p',
```
give me back `s-p` key in Emacs.

# Basic Usage

Getting key bindings help with `C-c p ?` or `C-c p C-h`.

Execute `M-x` following `projectile-` to see all Projectile commands.

## Project

A project is a basically folder, Projectile automatic detect projects, without any configuration.

* Add a project to projects list

    Every time we open a file, Projectile detect if it is inside a project using a set of practical rules, if a new project is recongnized, Projectile will add it to it's projects list.
	
	If the automatic detection fails, you can also add a `.projectile` project marker into the root directory to force the folder to be detected as a project.

* Delete a project in projects list

    When the projects list goes too larger, I'd like to remove unused project in it.
	
    `M-x projectile-remove-known-project` can remove a selected project.
	
	`M-x projectile-clear-known-projects` can clear the project list.

* Switch project

    `C-c p p` Switch project and execute `projectile-find-file` by default.

* Show projects in project list
    
	`C-c p p` is also a convenice way to show  projects in the project list.

## File

`C-c p f` or `M-x projectile-find-file` go to any files in current project. This is what I expected the most.
Try it, it is very pleasant to use.

## Grep

`C-c p s g` or `M-x projectile-grep` find any thing in all files in current project. Try it now, it is very easy to use. The problem is that it is not increasement searching which is not cool. But it is reliable and very fast -- because it use external `find` and `grep` tools, so I decided to get used to it.

# Conclusion
I'm happy with my Projectile's settings right now. As time goes by, I may try some more advanced features when I needs it.


[1]: https://github.com/bbatsov/projectile
[2]: https://www.projectile.mx/
[3]: https://www.emacswiki.org/emacs/CategoryProject
[4]: https://github.com/bbatsov/helm-projectile
[5]: https://tuhdo.github.io/helm-projectile.html
[6]: https://askubuntu.com/questions/68463/how-to-disable-global-super-p-shortcut
