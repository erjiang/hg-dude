# hg-dude

hg-dude is a simple Mercurial desktop notifier. It monitors hg repositories in
current directory for new commits/branches/tags and shows desktop notification if
anything new arrived.

## How it works

It simply uses `hg incoming` and parses its output to see what has changed.
Then it shows desktop
notification with `notify-send` / `kdialog` (Linux) or `growlnotify` (OSX). All
of this in infinite loop.

## How does it look

Ubuntu:

![hg-dude with notify-send](http://i.imgur.com/DRl2v.png)

## Requirements

On Linux:

* `notify-send` on Gnome (Fedora: _libnotify_ package, Ubuntu: _libnotify-bin_ package)
* `kdialog` on KDE (included in KDE)

On OSX:

* `growlnotify`, from [Growl Extras](http://growl.info/extras.php#growlnotify)
  (Homebrew: _growlnotify_ package)

## Installation

    $ curl -skL https://github.com/erjiang/hg-dude/raw/master/hg-dude >~/bin/hg-dude
    $ chmod +x ~/bin/hg-dude

\* Make sure `~/bin` is in your `$PATH` or put `hg-dude` script somewhere else
on your `$PATH`.

## Usage

hg-dude iterates over repositories that live inside _the dude directory_. This
directory is nothing more than container for cloned repositories of projects
you want to watch.  Name it like you want, here for example we use
_~/.hg-dude_:

    $ mkdir ~/.hg-dude
    $ cd ~/.hg-dude

Clone some repositories:

    $ hg clone ssh://hg@bitbucket.org/pypy/pypy
    $ hg clone ssh://hg@bitbucket.org/jespern/django-piston

Symlinked repositories work too. This way you can monitor already cloned
projects:

    $ ln -s ~/code/tmuxinator .

Now run this to monitor _pwd_:

    $ hg-dude

You can also pass directory name as first argument to specify which directory
to monitor instead of _pwd_.

    $ hg-dude ~/watched-repos

This way you can have multiple _dude directories_ each being monitored by
separate hg-dude process.

## Configuration

### Global

Set how often hg-dude should check for changes (in seconds, default: 60):

    $ export HG_DUDE_INTERVAL=30

Set path to icon used by desktop notifications (default: none):

    $ export HG_DUDE_ICON=~/my_icon.png

## Author

Eric Jiang (http://ericjiang.com/ @ericrjiang)

Based on git-dude by
Marcin Kulik (http://ku1ik.com/ | @sickill)
