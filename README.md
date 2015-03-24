Simple IRC ⟷  Skype Gateway Bot
================================

Best used as a [dockerized bridge](https://github.com/caktux/skypebridge)

FEATURES
--------

* Mirror messages from IRC channel to Skype chatroom and vice versa
* Support regular messages, emotes (`/em`) and Skype message edits
* Only from IRC side
   * In chat, trigger mirroring transparently by adressing the bot with `ON` or `OFF`
   * Direct messages to bot
      * Turn mirroring to Skype `ON` or `OFF` for the user, get user's present `STATUS`
      * Query for Skype users mirrored to IRC channel using `INFO #channel`
   * Search friends' usernames/full name with `FRIEND <part of name/username>` (shorthand `FR`)
   * Get a friend's online status and infos with `ABOUT <part of name/username>` (shorthand `AB`)
   * List stored channel topic/names with `CHANNELS` (shorthand `CH`)

* **Private messages bridge, no need to run Skype on your machine anymore!**

**This bot deliberately prefers IRC to Skype!**

INSTALL
-------

On Ubuntu/Debian you need `python-irclib` and `python-skype` as well as Skype itself to run the script.

For `python-skype` I used the version 1.0.31.0 provided at `ppa:skype-wrapper/ppa`. Although newer version is packaged even for Ubuntu 11.04, this package didn't work out of the box on Ubuntu 12.04. Using latest source version from https://github.com/awahlig/skype4py works fine on Ubuntu 14.04.

CONFIGURE
---------

Copy `config.py.sample` to `config.py` and edit that newly created file. Enable the personal bridge by setting `pm_bridge` to `True`, optionally removing the entries in `mirrors` if you only want to run a pm bridge. 

You can configure the IRC servers and Skype chatrooms to mirror in the same `config.py`. You may define one IRC server and as many pairs of IRC channels and Skype chatrooms as you like. Skype chatrooms are defined by the blob, which you can obtain writing `/get blob` in a chatroom. **New cloud-based rooms (the new default) do not work, you need to create old-style P2P group chats with `/createmoderatedchat`**.

You may need to join your Skype chatroom to be mirrored before actually starting the gateway, because it seems that Skype API isn't always able to successfully join the chatroom using a blob provided (I usually get a timeout error). So make sure you have an access to chatroom using GUI before starting to hassle with the code. You might also need to `/get blob` a few times before it works, even with `/createmoderatedchat`.

The default values provided in `config.py.sample` should be enough to give the program a test run.

If you want to use an option to save broadcast states for IRC users, working directory for the script has to be writable.

RUN
--- 

To run the gateway, Skype must be running and you must be logged in. You can do command line log in using `echo username password | skype --pipelogin` or you may just enable auto login from GUI. If you start `skype2irc.py` there will be a pop up window opened by your Skype instance on first run to authorize access to Skype for Skype4Py. You can either allow access just once or remember your choice.

You can run `skype2irc.py` just from command line or use `ircbot.sh` to loop it. You can also run it from plain terminal providing the X desktop Skype will be started like `DISPLAY=":0" ./skype2irc.py`.

It could also make sense to run it using `ssh -X user@host` session, virtual framebuffer or with something similar.

Make sure to try as a [dockerized bridge](https://github.com/caktux/skypebridge) for easier deployment on a server, and it's much better to run that proprietary software in a container. Enjoy!
