+++
title = "Cleaning up with find(1)"
author = ["Josh Friedlander"]
date = 2024-02-15
draft = false
+++

I often use `SPC /` in [Doom Emacs](https://github.com/doomemacs/doomemacs) for `+default/search-project`. I also often use `C-x v ​~` for `vc-revision-other-window` to compare a file in another branch in version control. I noticed the other day while searching my project that it was finding a whole lot of matches in files I had compared with another branch, which look something like `file.h~staging~`. But I had closed them, so why were they still showing up?

I looked at `+default/search-project`, and saw that it calls the related function in [Vertico](https://github.com/minad/vertico) (the completion framework I use), which is basically just running a text search on the directory. So...maybe these files are still there? Yes - turns out `vc-revision-other-window` leaves behind the files it creates, so it doesn't need to check them out again if you need them again. ([Here](https://stackoverflow.com/a/49112657/6220759) is a solution someone else came up with for this problem.)

I just wanted to run a one-off cleanup, since I had a lot of cruft there. I figured I could use `find` with a regex, which I could, but I just had to figure out that the regex needs to match the _whole_ name, not just part of it. So my final result was:

> `find . -regex ".*\.~.*~$" | xargs rm`

(At some point in the future, I would like to make a function that will kill the temp buffer, close the window it opened, and delete the file.)
