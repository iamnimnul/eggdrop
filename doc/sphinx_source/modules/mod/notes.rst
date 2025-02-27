Last revised: January 1, 2002

.. _notes:

============
Notes Module
============

This module provides support for storing of notes for users from each other.
Note sending between currently online users is supported in the core, this
is only for storing the notes for later retrieval.

This module requires: none

Put this line into your Eggdrop configuration file to load the notes
module::

  loadmodule notes

There are also some variables you can set in your config file:

  set notefile "LamestBot.notes"
    Set here the filename where private notes between users are stored.

  set max-notes 50
    Set here the maximum number of notes to allow to be stored for each user
    (to prevent flooding).

  set note-life 60
    Set here how long (in days) to store notes before expiring them.

  set allow-fwd 0
    Set this to 1 if you want to allow users to specify a forwarding address
    for forwarding notes to another account on another bot.

  set notify-users 1
    Set this to 1 if you want the bot to let people know hourly if they have
    any notes.

  set notify-onjoin 1
    Set this to 1 if you want the bot to let people know on join if they have
    any notes.


Copyright (C) 2000 - 2023 Eggheads Development Team
