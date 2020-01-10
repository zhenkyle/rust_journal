+++
title = "Install Emacs stable release on Chrome OS"
date = 2020-01-11T15:00:00Z
+++

What I want is to install the stable version of Emacs on my Chromebook. After all, my Chromebook is on stable channel. The most recent stable version of Emacs is 26.3 now, the most recent version of Chrome OS is 79 now, and the most recent Debian version on Chrome OS 79's Linux enviroment is Strech now.

Install Emacs stable release on a rolling release Linux like Arch linux is a piece of cake, because you are always up to update.
Install Emacs stable on Debian/Ubuntu unstable is also easy, there are prebuild 26.3 version you can install directliy. 
However, As of Chrome OS 79, the Crostini Linux enviroment is still at `stretch` -- the `oldstable` release, the newest package we can get is `emacs25`. Install Emacs stable on Chrome OS require extra works.

Why I can't get ease with `emacs25` on Debian Stretch is that When I install `evil-mode` via MELPA, I get some error saying `undo-tree` can not be installed. It seems like it is related to some BUG in Emacs 25, but has been fixed in Emacs 26 which is the stable version now. So Emacs 26 is what I needed.

The first thing I tried is install Emacs 26.3 via flatpak, although I can get emcas26 up and runinng, I can't do any useful thing with it, the `m-x term` is a shell inside flatpak container, which is not I want. I think install Emcas in container is the wrong way. So what I have to do is to install it as a normal application.

I spend some time searching for prebuilt Emacs stable (26.3) packages for Debian stretch (oldstable) on EmacsWiki and Debian sites without lucky, so that means I have to build my Emacs 26.3 myself. There are 3 ways to do this, orderd by recommendations priority.

1. use Debian backport method if the version of software required is in newer version of Debian
    Debian Wiki says this way won't mess up with your package system.

2. use Ubuntu PPA port to Debian method if the version of required is in Ubuntu PPA
3. build directly from sources

Because Emacs version 26.3, which is what I needed, is on Debian unstable (sid), so I decided to go with the first method, following the [Simple Backport Creation Guide][1]. After some tweak, I built and installed it with success.

The Debian Simple Backport Guid should be followed exactly, but in case I will needed to do this again, there some gotcha to be remembered.

1. The `rmadison` command is from `packaging-dev`, you can use it to check which version is available in Debian archive.

2. Before started, uninstall all packages whose name begin with `emacs` and `emacsen` with `apt purge`, if you installed old version of Emacs before.

2. In order to download Emacs source form `sid`, you need to add these lines to your `source.list`
    ```
    deb http://deb.debian.org/debian sid main non-free
    deb-src http://deb.debian.org/debian sid main non-free
    ```
    Only add the second line will not will. Then do
    ```
    apt update
    ```
    And then download source with 
    ```
    apt source -t sid emacs
    ```
    After that and before building, delete these lines form your `source.list` and do `apt update` again. This is important, or else you will build your emacs on wrong debian version. Remember we want to build Emacs on Strech.
    
3. `fakeroot debian/rules binary` require a lot time, it can be safely skipped.

4. In my enviroment, I need `emacsen-common` to sucessful install `emacs`, and also need `emacs-common-non-dfsg` for Emacs Info document, which is from `non-free` channel.

5. To install a deb file under current path, you need to prefix it with `./`

6. I need to specify all deb files in order to successful install, which is
```
apt install ./emacs_*_*.deb ./emacs-common_*_*.deb \
./emacs-bin-common_*_*.deb ./emacs-gtk_*_*.deb
```

7. Backup these deb files to some place, you can reinstall them someday without rebuild

8. In order to make text bigger, add `sommeiler -X --dpi=175` to `/usr/share/application/emacs.desktop`'s `Exe` section.

9. In order to see all fonts in Emacs Hello file with `C-h h`, I need to install these fonts
    ```
    apt install -t stretch-backport fonts-noto fonts-noto-cjk
    ```
	Note: strech-backport channel's fonts is newer than strech channel's.


After all these steps, I can happily play with emacs stable release on my Chromebook now :-)

[1]: https://wiki.debian.org/SimpleBackportCreation


