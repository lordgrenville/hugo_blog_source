---
title: Scraping Kevin Lewis
date: 2021-11-11
draft: false
---

Kevin Lewis' daily _Findings_ blog at National Affairs is a great way to stay on top of social science news, presenting a daily themed collection of abstracts of recent papers. The site is free to read, but doesn't offer an RSS feed, which is my preferred way to consume it. I decided to write a short Python script to scrape new posts into a local XML file.

The basic script I started with went to [the author's page](https://www.nationalaffairs.com/authors/detail/kevin-lewis), found the box with most recent posts, followed and scraped each link, encoded them as RSS (basically URL-encoding the HTML tags), added opening and closing RSS XML tags, and saved the file. In further iterations I added the ability to open the file if it exists, check if an item exists (and not scrape it), and cleaned up the code. Once I was happy with it, the last thing I wanted to add (for now!) was the ability to run it on the reg. The code is [here](https://github.com/lordgrenville/scrape_kevin).

My first instinct was to run `crontab -e` and set up a weekly run there. But I found that since my Macbook goes to sleep quite aggressively to save power, often the job wouldn't be carried out. Turns out that macOS has a built in tool called `launchd` which is recommended over cron, and can also run after waking if it missed its cue.

To add it I created a file called `~/Library/LaunchAgents/update_lewis.plist`, with the command arguments as outlined [here](https://www.launchd.info/). Then I called `launchctl load ~/Library/LaunchAgents/update_lewis.plist` (cancel with `unload`), and voilà!
