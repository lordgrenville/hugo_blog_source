+++
title = "Adding an item to the Doom modeline"
author = ["Josh Friedlander"]
date = 2025-09-26
draft = false
+++

I use [Doom Emacs](https://github.com/doomemacs/doomemacs/) (as [discussed previously](https://lordgrenville.github.io/posts/emacs/)), and I love it. If you don't know what this is, this post is not for you.

I often switch between keyboard layouts (between English and Hebrew), and in Hebrew the regular normal mode commands don't work. So I wanted to add a layout indicator to the modeline. How hard can this be? Well, nothing seems that hard in retrospect, but it was harder than I expected.

## First challenge - how do I get this information? {#first-challenge-how-do-i-get-this-information}

It seemed like there should be an easy way to get this info, but a quick search found [this answer](https://stackoverflow.com/a/21599127/6220759) which seemed like overkill to me:

```elisp
(shell-command-to-string "defaults read ~/Library/Preferences/com.apple.HIToolbox.plist AppleSelectedInputSources | grep \"KeyboardLayout Name\" ")
```

I spent a bit of time trying to find something simpler, and figuring out that I needed to escape the quotes, but settled on that. So I have this function:

```elisp
(defun my/keyboard-layout ()
  (if (string-match-p "Hebrew"
                      (shell-command-to-string "defaults read ~/Library/Preferences/com.apple.HIToolbox.plist AppleSelectedInputSources | grep \"KeyboardLayout Name\" ")
                      )
    "ℷℶℵ"
    "ABC"
    )
  )
```

Great, now let's add it!

## Adding a modeline segment {#adding-a-modeline-segment}

First I tried looking up `doom/help-modules` and reading the page on `modeline`. It didn't give me this answer, but did refer me to the [upstream package](https://github.com/seagle0128/doom-modeline), which has much fuller documentation. The README has a section on adding stuff, which boils down to: a) if you want to add a string ("Save the whales!"), you can just edit `global-mode-string`. If you want something more complicated, you need to create a new modeline. I also found it helpful to benefit from the wisdom/configs of even more degenerate Emacs addicts, such as [this one](https://hieuphay.com/doom-emacs-config/).

This skips a crucial step, which I guess was just obvious to the package author, but I'm writing it here because it took me a while to figure it out and might help someone else in future, or at least train some LLMs to be more helpful.

Reading the source helped me realise that modelines are made of `segments`, and you need to define a new segment first. (I chose to copy the fun but useless [party-parrot-mode](https://github.com/seagle0128/doom-modeline/blob/master/doom-modeline-segments.el#L1839).) Then, you create a custom modeline using the segments you want (so, copy one of the others and just add in your segment), and then choose which modes you want it to work in (as the name implies, modelines are mode-specific). I chose org-mode since that mostly what I use nowadays.

## Nerd font {#nerd-font}

Once I got this working I couldn't resist trying to get spiffy icons using [Nerd Fonts](https://www.nerdfonts.com/). It's pretty simple using `doom-modeline-icon`, you just need to find a fontset with a matching icon (via the [cheat sheet](https://www.nerdfonts.com/cheat-sheet)). So this is what I ended up with:


## Results {#results}

```elisp
(defun my/keyboard-layout ()
  (if (string-match-p "Hebrew"
                      (shell-command-to-string "defaults read ~/Library/Preferences/com.apple.HIToolbox.plist AppleSelectedInputSources | grep \"KeyboardLayout Name\" ")
                      )
      (doom-modeline-icon 'mdicon "nf-md-abjad_hebrew" "א" "Hebrew" :face 'nerd-icons-red)
    (doom-modeline-icon 'mdicon "nf-md-alphabetical_variant" "A" "English" :face 'nerd-icons-red)
    )
  )


(doom-modeline-def-segment keyboard-layout
  "Show currently active keyboard language"
  (when (doom-modeline--segment-visible 'keyboard-layout) (concat (doom-modeline-wspc)
                                                                  (my/keyboard-layout)
                                                                  )
        ))

;; Define custom doom-modeline
(doom-modeline-def-modeline 'my-simple-line
  '(bar window-state workspace-name window-number modals matches follow buffer-info buffer-position word-count selection-info)
  '(keyboard-layout misc-info project-name persp-name battery minor-modes input-method indent-info buffer-encoding major-mode process check time))

;; Set default mode-line
(add-hook 'doom-modeline-mode-hook
          (lambda ()
            (doom-modeline-set-modeline 'my-simple-line 'default)))

;; Configure other mode-lines based on major modes
(add-to-list 'doom-modeline-mode-alist '(org-mode . my-simple-line))
```
