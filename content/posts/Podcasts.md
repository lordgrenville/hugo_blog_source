---
title: Carrying Podcasts From the Well On My Shoulders, Like In the Old Days
date: 2019-07-16
draft: false
---

In general my view on podcasts is the shorter the better. So I really
like [Bloomberg View](https://www.bloomberg.com/podcasts/view), which
runs just over a minute and distills the essence of a longer (usually
well thought-out) op-ed. (I guess by this logic the ideal podcast would
be 0 seconds - very Cagean.)

But it seems like the Berg is phasing this one out. It no longer appears
on the website or on most podcast providers, and the RSS feed I had
(from iTunes) on [Podcast
Addict](https://play.google.com/store/apps/details?id=com.bambuna.podcastaddict&hl=en_US)
(a truly excellent app) suddenly returned
`SSLHandshakeException: java.security.cert.CertPathValidatorException: Trust anchor for certification path not found`.
I emailed the developer and he promptly (shout-out Xavier! He really is
awesome) explained that SSL cert verification in modern versions of
Android is done by the device for all apps (except web browsers), so
this error is not coming from inside the app. I confirmed that I hadn't
accidentally disabled my trust of any previously accepted certificate,
and he later showed me that the SSL cert for the RSS feed was indeed
expired.

I emailed Bloomberg about this, but I think they are sunsetting this
podcast, and their support ticket confirmation email never showed up. In
the meantime I wanted to just grab those episodes, so I did it old
school.

    import requests
    import xml.etree.ElementTree as ET

    feed = requests.get('https://feeds.bloomberg.fm/BLM8578726790', verify=False).text
    # you need to disable verify because of the dodgy SSL. requests throws up a warning telling you that this is very foolish
    feed = ET.fromstring(feed)

After fooling around with the `xml` I get this:

    for child in feed.getchildren()[0].getchildren():
        if child.tag == 'item':
            x = child.getchildren()
            print(x[0].text)
            print(x[-2].text)

    >
    Bloomberg Opinion Radio: Weekend Edition for 7-12-19 (Podcast)
    https://assets.bwbx.io/av/users/iqjWHBFdfxIU/vrsTK.0wJcuQ/v4.mp3
    How to Tame Europe’s Game of Thrones: Editorial (Podcast)
    https://assets.bwbx.io/av/users/iqjWHBFdfxIU/vRijgKsrekSc/v4.mp3
    Ramesh Ponnuru on the Obamacare Lawsuit Paradox (Podcast)
    https://assets.bwbx.io/av/users/iqjWHBFdfxIU/vRzEW1v7.DEc/v4.mp3
    Demanding Straight Answers on Immigration: Editorial (Podcast)
    https://assets.bwbx.io/av/users/iqjWHBFdfxIU/viPbxsujOdcQ/v4.mp3

    etc..

And then I just grabbed the ones I wanted with `wget`:

    mkdir podcasts && cd podcasts/
    wget -O pelosi.mp3 https://assets.bwbx.io/av/users/iqjWHBFdfxIU/vAThJHLXwFKM/v4.mp3

    etc...

Sent them to my phone with Bluetooth, and added the `bluetooth` folder
as a virtual podcast. And there you go, podcasts the old fashioned way!
