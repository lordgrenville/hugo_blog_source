---
title: Tar Hack
date: 2020-05-11
draft: false
---

There’s a funny [xkcd cartoon](https://xkcd.com/1168/) about the `tar` command:

![](https://imgs.xkcd.com/comics/tar_2x.png)

How does one remember those ridiculous single letter commands? My preferred solution is to first consult with [TLDR](https://tldr.sh/), but Justin Abrahams has a fun solution [over at his blog](https://justin.abrah.ms/bash/forgotten_friend_3.html):
```bash
  extract () {
    if [ -f 1 ] ; then
      case 1 in
        *.tar.bz2)        tar xjf 1        ;;
        *.tar.gz)         tar xzf 1        ;;
        *.bz2)            bunzip2 1        ;;
        *.rar)            unrar x 1        ;;
        *.gz)             gunzip 1         ;;
        *.tar)            tar xf 1         ;;
        *.tbz2)           tar xjf 1        ;;
        *.tgz)            tar xzf 1        ;;
        *.zip)            unzip 1          ;;
        *.Z)              uncompress 1     ;;
        *)                echo "'1' cannot be extracted via extract()" ;;
    esac
    else
      echo "'1' is not a valid file"
    fi
```
(Appended, naturally, to `.bashrc`.)
