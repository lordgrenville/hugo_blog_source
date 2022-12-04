---
title: Easy Things that are Hard
date: 2022-12-04
draft: false
---

Something that should be easy but weirdly isn't is sharing text or files between two of my devices, say a laptop and a phone. There are lots of sometime solutions for this - if you have a Macbook and an iPhone on the same account, you have a shared clipboard, and [KDE Connect](https://kdeconnect.kde.org/) is also designed to solve this, but unfortunately its support for macOS is [experimental](https://binary-factory.kde.org/view/MacOS/job/kdeconnect-kde_Nightly_macos/) and doesn't seem to support Apple Silicon. Failing that, there are the more prosaic workarounds: texting it to a trusted friend (and maybe deleting afterwards), or emailing it to yourself. These solutions are inelegant to me - why should I send a file all the way to a Google or WhatsApp or Dropbox server just to move it 20 centimetres physically, within the same local network? There must be a better way!

(My previous solutions have also included using my knowledge base [Joplin](https://joplinapp.org/), which also roundtrips to Dropbox \[side point: another rainy day project is to use local sync most of the time for this, with a separate regular backup to Dropbox, but this does at least pose more difficult problems of consistency and resolving conflicts, etc\], or else using the unpretentious [https://sharetxt.live](https://sharetxt.live), built for this purpose, but sharing everything publicly unless you log in.)

Anyway, I've recently been writing long messages to send on my phone, so I want to edit them in Emacs and then send them to my phone clipboard. This is actually easy to solve with a local server (so the title of this post is wrong I guess...), and I'm mainly just putting it here to remember the exact command. I use `buffer.txt` for editing, then in `app.py` I have:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def message():
    with open('buffer.txt') as f:
        return f"<p>{'<br>'.join(f.readlines())}</p>"
```

And then launch with `flask --debug run --host=0.0.0.0 --port=5001`. Explanations for the options:

-   `debug` is to auto-reload the server whenever one of the files in the directory changes (in this case `buffer.txt`)
-   `host` given explicitly is to make it available to other machines on the network, which is otherwise disabled as a security precaution. Python's `http.server` doesn't restrict this, but it only allows files to be viewed and downloaded, not code execution.
-   Explicit port is only needed because the default, 5000, is used by Apple for some dumb service of its own (`AirPlay Receiver`, whatever that is).

Then the text is accessible to any device connected to the local network at `http://<internal IP address>:5001`.
