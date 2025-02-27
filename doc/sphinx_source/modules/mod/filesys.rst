Last revised: Dec 30, 2017

.. _filesys:

==============
Filesys Module
==============

This module provides an area within the bot where users can store and manage
files. With this module, the bot is usable as a file server.

This module requires: transfer

-----------------
Config file setup
-----------------

Put this line into your Eggdrop configuration file to load the filesys
module::

    loadmodule filesys

There are also some variables you can set in your config file:

  set files-path "/home/mydir/eggdrop/filesys"
    Set here the 'root' directory for the file system.

  set incoming-path "/home/mydir/eggdrop/filesys/incoming"
    If you want to allow uploads, set this to the directory uploads should be
    put into. Set this to "" if you don't want people to upload files to your
    bot.

  set upload-to-pwd 0
    If you don't want to have a central incoming directory, but instead
    want uploads to go to the current directory that a user is in, set this
    setting to 1.

  set filedb-path ""
    Eggdrop creates a '.filedb' file in each subdirectory of your file area
    to keep track of its own file system information. If you can't do that
    (for example, if the dcc path isn't owned by you, or you just don't want
    it to do that) specify a path here where you'd like all of the database
    files to be stored instead.

  set max-file-users 20
    Set here the maximum number of people that can be in the file area at
    once. Setting this to 0 makes it effectively infinite.

  set max-filesize 1024
    Set here the maximum allowable file size that will be received (in KB).
    Setting this to 0 makes it effectively infinite.

---------------
Partyline usage
---------------

^^^^^^
.files
^^^^^^

  Moves you into the file transfer sub-system, if it has been enabled on this
  bot. From there you can browse through the files online and use dcc file
  transfers to download and upload.

^^^^^^^^^^^^^^^^^^^^^^^^^
.cancel <file> [file] ...
^^^^^^^^^^^^^^^^^^^^^^^^^

  Tells the bot to stop sending a file that is pending (either
  queued, waiting, or in the process of being transferred).

^^^^^^^^^^^^^^^
.cd <directory>
^^^^^^^^^^^^^^^

  Changes your current directory if possible.  this works exactly
  like the unix command.

^^^^^^^^^^^^^^^^^^
.cp <source> <dst>
^^^^^^^^^^^^^^^^^^

  Copies a file or group of files from one place to another.

^^^^^^^^^^^^^^^^^^^^^^^^^^
.desc <file> <description>
^^^^^^^^^^^^^^^^^^^^^^^^^^

  Changes the description for a file.  if you are a master or
  file janitor, you can change the description for any file.
  otherwise you can only change the descriptions for files you
  have uploaded.

  The description is restricted to 3 lines of 60 characters
  each, and is broken up between words.  you can force a line
  break by putting a '|' in the comment.

^^^^^^^^^^^^^^^^^^^^^^^^^
.filestats <user> [clear]
^^^^^^^^^^^^^^^^^^^^^^^^^

  Reports on the users upload & download statistics. Optional argument
  'clear' clears a users upload and download statistics.

^^^^^^
.stats
^^^^^^

  Clears a users upload & download statistics.

^^^^^^^^^^^^^^^^^^^^^^^^^^
.get <filename> [nickname]
^^^^^^^^^^^^^^^^^^^^^^^^^^

  Sends you the file(s) requested, over IRC.  you should get a
  DCC SEND notice on IRC, and have your client accept it.  if
  your nickname on IRC is different than the one you use on the
  bot, you should specify a nickname too.  you can also use that
  to send files to other people.  if a file you want is actually
  on another bot, it may take a little bit longer so be patient.
  if that bot isn't on the botnet right now, it will say the file
  isn't available.

  There is a limit to the number of transfers you can have going
  simultaneously, so if you go over this limit, the remainder of
  your file requests will be queued. As the first files finish
  transferring, the queued files will be sent.

^^^^^^^^^^^^^^^^^^^^^^^^
.hide <file> [files] ...
^^^^^^^^^^^^^^^^^^^^^^^^

  Marks a file as hidden, so that normal users can't see it. 
  Only a master or file janitor using %b'lsa'%b can see hidden files.

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.ln <bot:filepath> <localfile>
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   Creates a link to a file on another bot. The filepath has to
   be complete, like '/gifs/uglyman.gif'.  If the bot is not
   connected to the botnet, nobody will be able to download the
   file until that bot connects again. The local filename can be
   anything you want.

   Example:  ln Snowbot:/gifs/uglyman.gif ugly.gif

^^^^^^^^^^^^^^ 
.ls [filemask]
^^^^^^^^^^^^^^

   Displays the files in the current directory. Subdirectories
   are shown with "<DIR>" next to them, and other files will display
   their size (typically in kilobytes), who uploaded them (and when),
   and how many times each file has been downloaded. If a description
   of the file exists, it is displayed below the filename. You can
   restrict the file listing by specifying a mask, just like in unix.

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.mkdir <dir> [flags [channel]]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  Creates a subdirectory from this one, with the given name.  If
  flags are specified, then those flags are required to enter or
  even see the directory.  You can even specify a channel that the
  flags are matched against. You can use the %b'mkdir'%b command again
  to alter or remove those flags.

^^^^^^^^^^^^^^^^^^^
.mv <source> <dest>
^^^^^^^^^^^^^^^^^^^

  Moves a file or group of files from one place to another (it
  can also be used to rename files).

^^^^^^^^
.pending
^^^^^^^^

  Gives you a listing of every file you've requested which is
  still waiting, queued, or in the process of transferring.
  It shows you the nickname on IRC that the file is being sent
  to, and, if the transfer is in progress, tells you how far
  along the transfer is.

^^^^
.pwd
^^^^

  Tells you what your current directory is.

^^^^^
.quit
^^^^^

  Exits the file system.

^^^^^^^^^^^^^^^^^^^^^
rm <file> [files] ...
^^^^^^^^^^^^^^^^^^^^^

   Erase a file for good.

^^^^^^^^^^^^
.rmdir <dir>
^^^^^^^^^^^^

  Removes an existing directory, if there are no files in it.

^^^^^^^^^^^^^^^^^^^^^^^^^
.share <file> [files] ...
^^^^^^^^^^^^^^^^^^^^^^^^^

  Marks a file as shared. This means that other bots can get
  the file remotely for users on their file systems. By default,
  files are marked as unshared.

^^^^^^^^^
.optimize
^^^^^^^^^

  Cleans up the current directory's database. If you have a large
  directory with many files you may want to use this command if
  you experience slow-downs/delays over time. Normally, the db
  should clean up itself though.

^^^^^^^
.unhide
^^^^^^^

  Makes a file be not hidden any more.


^^^^^^^^^^^^^^^^^^^^^^^^^^
.unshare <file> [file] ...
^^^^^^^^^^^^^^^^^^^^^^^^^^

  Removes the shared tag from a file.


^^^^^^^^^^^^^^^
.filesys module
^^^^^^^^^^^^^^^

  This module provides an area within the bot where users can store and
  manage files. With this module, the bot is usable as a file server.

  The following commands are provided by the filesys module:

  For filesystem users:
      files



Copyright (C) 2000 - 2023 Eggheads Development Team
