---
layout: post
title:  "iCloud Drive whole-folder syncing: sometimes you do want everything"
date:   2016-06-15 22:16:42 +1030
categories: apple, shell
---

Some time last year I switched from Bittorrent Sync to iCloud for cloud file storage. Bittorrent Sync was great when it worked, but I had some early-adopter file loss and, more importantly, over time realised that I wasn't organised enough to run a home server to have a ground-truth version of all my stuff. Without an always-on PC, I found the operating model of Bittorrent Sync a little too brain-taxing.

However, one aspect of Bittorrent Sync that worked very well for me was the idea of ‘Selective Sync’, in which files were only copied to your local storage on demand. No need to white-list certain folders. This is a ‘it just works’ approach to the problem of having much larger cloud storage tiers than space on one's PC. Interestingly, this feature first debuted in Windows 7 or 8, only to be dropped again in Windows 10, and it's now becoming available in Dropbox via [Project Infinite](https://blogs.dropbox.com/business/2016/04/announcing-project-infinite/).

Turns out that iCloud has been quietly doing this for a while, too. I've had one or two occasions in which files didn't seem to sync as quickly as they should, but often a relaunch of Finder fixed those issues. After quite some months, I've been very impressed by iCloud Drive's reliability.

However, both Bittorrent Sync and iCloud Drive share a flaw in their implementation of this Selective Sync approach: sometimes you really do want to sync an entire folder of files. For example:

  * I might have a folder containing a LaTeX document with a number of sub-files and sub-folders containing, say, images. I need them all to compile the document.

  * I might be writing a script to process a bunch of source files, and of course all the source files need to be located locally.

The Finder interface to iCloud Drive provides no way of downloading/syncing an entire folder's worth of files. You could select each file not synced (those with the cloud+arrow icon) and open each one to force the sync, but that becomes unwieldy. Or, you could use a shell script one-liner to automate the process.

Basically, any file that's located in iCloud Drive but not stored locally has a placeholder file with name ‘`.name.ext.icloud`’, where `name.ext` is the file's proper name. So finding all such files and directing the Finder to `open` them is enough to trigger a sync.

Without going into the details, this can be performed with the following shell script:

    #!/bin/bash

    # print out each file to sync:
    find . -name *.icloud -print0 | xargs -n 1 -0 echo

    # "open" each file in Finder to force the sync:
    find . -name *.icloud -print0 | xargs -n 1 -0 open -a "Finder"

Run from a folder, this will recursively (i.e., in all sub-folders) find all files with the `.icloud` extension and open them in Finder to force the sync. This may have the side-effect of launching a bunch of files, but I know of no way to suppress this behaviour.

Because I only touch this kind of thing occasionally, I never remember the syntax to `find` and `xargs`. There are probably better ways to write this, but the code above works for me for now.

I think this isn't such an uncommon use case that I'm perhaps a little surprised it's not provided for in the UI for these cloud storage tools. Switching basically wholesale to cloud storage has been such a success for me that I imagine it will only be a few years before it's the norm.
