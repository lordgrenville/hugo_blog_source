+++
title = "Rooting my Nook Simple Touch"
author = ["Josh Friedlander"]
date = 2026-10-22
draft = false
+++

In around 2013-14 (so far back I can't even find the email receipt!) I got a [Nook Simple Touch](https://en.wikipedia.org/wiki/Nook_Simple_Touch). I've had it since then and still use it, although it was officially [EOL-d in 2024](https://help.barnesandnoble.com/hc/en-us/sections/26336578607131). It still works fine - the plastic exterior got kind of sticky at some point and I tried (not very successfully) to clean it and ended up scraping much of it off. But the software still works fine, and with [Calibre](https://calibre-ebook.com/download) I can easily put any books I want on it.

Since pretty early on I wanted to try root it, because:

1.  It came with a couple of books - an instruction manual, and some free classic - that I wanted to delete, because I was out of space
2.  I'm the sort of person that likes doing this. I mean being able to install arbitrary Android apps or a better reader or dictionary, sounds cool, right? Even if I don't actually do it, I want the right.

However, I never got around to it. It required some very simple equipment (an SD card reader??) and I was a bit nervous about the warnings that I could brick my device.

Anyway, it's 2026, it's old enough that I am less scared, my laptop (Lenovo T490s) has a built-in SD card reader (in a super-annoying place, at the back, such that you need to almost close the screen in order to get the card in and out, but still), you can also buy a new 32GB card for under $10. Plus there is AI - a mixed bag, it always has advice which is sometimes right and sometimes wrong, probably on net a help but also just good as moral support when I want to give up.

I finally did it yesterday, it was pretty straightforward but there were a couple of things I learned on the way that I wanted to record here:

1.  I had mostly used it with WiFi off (to save battery, and since I usually add books locally). So I had not gotten OTA firmware updates. I was on version 1.1, and it seemed like the rooting tool I used ([NookManager](https://github.com/doozan/NookManager)) would only work with the last one before EOL (2.2).
2.  To upgrade, you need to download a zip file of the new version, copy it to the top-level directory of the Nook, and then reboot and it will go into upgrade mode automatically. However, I found that it was not possible to skip versions, and the auto-detect upgrade only worked when I got the subsequent version, so I had to do it three times, from 1.1-&gt;1.2-&gt;2.1-&gt;2.2 . (And shoutout to the crazy people on XDA forums and the random sites still hosting older versions of obsolete firmware!)
3.  As an aside, all of this stuff was trial and error, with no log or feedback, just things silently not working until they did (and of course AI coming up with guesses all the time, which were sometimes helpful). So it's possible that some of this is wrong.
4.  Once I upgraded, I was able to copy the NookManager tool onto the SD card (using [balenaEtcher](https://etcher.balena.io/) in administrator mode in Windows), put it in the Nook while off, and then launch. Sometimes it would do nothing, sometimes it would get stuck at the `NookManager` loading screen, and one time I got all the way to the rooting menu but then it froze. Wasn't clear why.
5.  My AI suggested that the SD card I bought was too new, and that I try an older one from a camera or GoPro. I got hold of one, flashed, booted, and boom, I was in.
6.  Because the plastic has come off, the top right button doesn't really work (I just use swiping to turn the page). It is needed for navigating the `NookManager` menu. However I was able to push it by inserting a ball-point pen and pushing the contact firmly.
7.  Now I'm in! I have root access and a new browser. I don't really have any plans for using it differently (although it is nice to be on the more recent firmware, it feels a little faster). But it's great to have this done after only thirteen years.
