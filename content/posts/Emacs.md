---
title: A Complete Idiot's Guide to Doom Emacs
date: 2020-09-01
draft: false
---

(This guide assumes familiarity with Vim, git and command line, but no prior knowledge of Emacs. [This](http://www.jesshamrick.com/2012/09/10/absolute-beginners-guide-to-emacs/) is a good guide from zero to Emacs. I was also helped/inspired by [Noel Welsh's](https://noelwelsh.com/posts/2019-01-10-doom-emacs.html) Doom guide, and that of mad genius [Tecosaur](https://tecosaur.github.io/emacs-config/config.html).)

After several aborted attempts to get started with Emacs, I've finally made some sense of it. Since there aren't many basic guides online, I thought I'd document my process. Vim (which I'm using to type this) is a lot simpler to get started with (as soon as you figure out how to quit...) I think that has to do with its greater simplicity, as well as the fact that there's basically only one flavour. (NeoVim is from a user's perspective mostly identical, and if you're using `vi` you probably know what you're doing.) Emacs by contrast is a whole world.

The first question I had to deal with is: which Emacs do I use? Vanilla Emacs looks like something from the Stone Age, and doesn't offer you enough out of the box to persuade you to learn it - at least that was my experience. I was tempted back first with [Spacemacs](https://www.spacemacs.org/), and finally settled on [Doom Emacs](https://github.com/hlissner/doom-emacs), which will be the subject of this guide.

To clarify, all of these involve installing Emacs, and then building stuff on top of it. Emacs adds a `.emacs.d` folder to your home directory for your personal config, and these both customize that to look snazzier and use some extra tools right out of the box. Both Spacemacs and Doom emphasise `Evil`, an Emacs layer allowing Vim keys to be used instead of learning Emacs keys (though they allow either to be configured). Doom also stresses quick loading time and simplicity: it strives to do some basic config and let you get on with your work, rather than going down the rabbit-hole of eternal tweaking.

After installing Emacs and cloning the Doom repo, you will have a `.doom.d` folder alongside `emacs.d`. This is where you will do everything. `.doom.d` contains three files:

- `init.el`
- `config.el`
- `packages.el`

`init.el` is where you select what you want Doom to take care of. This part is the most abstracted away from regular Emacs. Instead of installing, say, a package for Python development, you tell Doom you want to use Python and it will install the Python stuff it recommends.  If you want to know how to configure this, you need to look inside the repo itself: `~/doom-emacs/modules/lang/python/README.org` in this example. (Don't make changes here, though, unless you want to contribute to Doom development, in which case you're way beyond this humble guide.) That README will tell you what packages are used, and sometimes which flags you can add. For example, you can add a `conda` flag in Python by replacing `python` in `init.el` with `(python +conda)`. The more languages and other tools you add, the slower start-up will be, so take only what you need. You can edit it at any time, but you must then sync, either with `~/.emacs.d/bin/doom sync`, or if you have Emacs open with `M-x doom-reload`. (`M-x` is META-x, or alt-x, the Emacs key for a menu for typing in commands. In Evil this is `SPC :` However this stuff is found in many newbie guides, so I'll try focus on stuff that I struggled to find online.)

The reason you have to sync after changing `init.el` is that it relies on Doom doing some work behind the scenes to install and load
packages - those are the abstractions. `config.el`, by contrast, is a regular Emacs lisp document, so any changes you make in it can be
evaluated and applied immediately. `config.el` is where you'll make any custom changes you want. _Whenever people tell you online to add
stuff with_ `(setq blah blah)` _you should put it in here._ If you want to install any _packages_, which in Emacs are usually installed from
a repository called MELPA, but can also come from the web (eg GitHub), you put them in `packages.el`.

By default Emacs uses different workspaces, each one containing a project. When you start working you should add your project root, and then you can navigate within it with `SPC f f`.

Lastly, a word about modes. Continuing the musical analogy of chords (key combinations), Emacs has modes which are basically added functionality within a buffer. A major mode is usually the language type, and a buffer can only have one, while it can have many minor modes. Major mode chords in Evil begin with `SPC m`, after which you will see a guide in the minibuffer with your next options. (Always true in Doom.)

Hopefully this should be enough to get you started with a project, the correct major mode, and some nice looking defaults. I definitely haven't been persuaded to drop Vim as my default `$EDITOR`, but I see it as my day-to-day tool, with Emacs as more of a speciality tool with capabilities like [Magit](https://magit.vc/), `org-mode`, and way more.
