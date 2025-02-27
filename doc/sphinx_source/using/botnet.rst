Botnet Sharing and Linking

==========================
Botnet Sharing and Linking
==========================


  The purpose of this document is to show you what a botnet is and how it
  could be useful to you. It also covers botflags userfile sharing.

What is a botnet?
-----------------

  A botnet consists of two or more bots linked together. This can allow bots to op each other securely, control floods efficiently, and share user lists, ban lists, exempt/invite lists, and ignore lists (if sharing is enabled).

Terms
-----

The following are some common terms used in this document:

**Botnet**
  A botnet consists of two or more bots connected together.

**Link**
  Link is the term used to describe a bot connecting to another bot.

**Hub**
   A bot is described as a hub-bot if one or more bots are linked to it.


**Leaf**
  A leaf is a non-hub bot connecting to a hub-bot. A leaf has only one other bot connected to it, its hub. Leaf bots can be assigned the "l" botflag to prevent other bots from linking to them.


**Link Bot**
  A link-bot is a bot that is linked to another bot. It may or may not be a hub-bot.


**Share**
  Share is the term used to describe the sharing of user records.


**Share Bot**
  A share-bot is a bot which shares user records with one or more linked bots.


**Aggressive Share**
  Aggressive share is a term used to describe the direction of sharing user-files. Aggressive share bots will SEND userfiles to another passive bot.


**Passive Share**
  Passive share is a term used to describe the direction of sharing user-files. Passive share bots will accept userfiles from an aggressive share bot.

**Address**
  The physical address, containing the address and port of the bot. For example: lame.org:3333. You can change a bot's address with::

        .chaddr <botname> <address> <port#>[/<relay-port#>]

**Relay Port**
  The relay port number of the bot is defined in the config file. Note that you can define one port for bots and another for user connections.

**Relay**
  A relay connection is used to relay (jump) to another bot via telnet or DCC chat. You can relay to another bot even if the remote bot is not linked. You can use::

   .relay <botname>

  to relay to another bot.

**Port**
  The telnet port is used by the bot to communicate with other bots and/or users. Note that you can define separate ports for user and bot connections.

Example bottree
---------------

::

  BotA
    |-+BotB
    `-+BotC

BotB is linked to a master sharebot, BotA, and a slave sharebot, BotC. BotB shares passively with [receives from] BotA and shares aggressively with [sends to] BotC.


Bot Flags
---------

Flags are attributes that determine what a bot can or is allowed to do.
Flags can be either global (such as +s) or channel specific (such as
\|+s #lamest). See '.help botattr' for help with setting these flags.

The following is a list of valid bot flags:

+------+---------------------------------------------------------------+
| a    | alternate (automatically link to this bot if the hub bot can't|
|      | be linked)                                                    |
+------+---------------------------------------------------------------+
| b    | ban sharing (passive bot is allowed to share bans with        |
|      | aggressive bot)                                               |
+------+---------------------------------------------------------------+
| c    | channel sharing (passive bot is allowed to share channel      |
|      | changes with aggressive bot)                                  |
+------+---------------------------------------------------------------+
| d    | share aggressively (SEND userfile to a passive bot),          |
|      | limited sharing (passive bot is NOT allowed to share anything)|
+------+---------------------------------------------------------------+
| e    | exempt sharing (passive bot is allowed to share exempts with  |
|      | aggressive bot)                                               |
+------+---------------------------------------------------------------+
| g    | global share (share all channels)                             |
+------+---------------------------------------------------------------+
| h    | hub (automatically link to this bot)                          |
+------+---------------------------------------------------------------+
| i    | isolate (isolate the party line across a bot link)            |
+------+---------------------------------------------------------------+
| j    | invite sharing (passive bot is allowed to share invites with  |
|      | aggressive bot)                                               |
+------+---------------------------------------------------------------+
| l    | leaf (bot is not allowed to link in other bots)               |
+------+---------------------------------------------------------------+
| n    | ignore sharing (passive bot is allowed to share ignores with  |
|      | aggressive bot)                                               |
+------+---------------------------------------------------------------+
| p    | share passively (ACCEPT userfile from an aggressive bot)      |
+------+---------------------------------------------------------------+
| r    | reject (bot will not be allowed to link)                      |
+------+---------------------------------------------------------------+
| s    | share aggressively (SEND userfile to a passive bot),          |
|      | unlimited sharing (passive bot is allowed to share anything)  |
+------+---------------------------------------------------------------+
| u    | user sharing (passive bot is allowed to share user changes    |
|      | with aggressive bot)                                          |
+------+---------------------------------------------------------------+
| 0-9  | user defined flags                                            |
+------+---------------------------------------------------------------+

Adding and linking bots
-----------------------

With the common terms out of the way, we can start with the process of linking two bots. Before you start, you need to know the address and port of each bot you wish to link.

Here is an example scenario:

      BotA is on lame.org listening on port 3333, and BotB is on irc.org
      listening on port 4444. First, you have to add each Bot to the other's
      userfile. On BotA, you would type '.+bot BotB irc.org 4444'. If BotB is
      on a common channel with BotA, BotB's hostmask is automatically added.
      Otherwise, you have to add the hostmask manually with the '.+host'
      command. On BotB, you would type '.+bot BotA lame.org 3333'.

At this point, you can link the two bots by typing '.link BotA' on BotB (or '.link BotB' on BotA). The bots will now give themselves random passwords which are *not* stored encrypted in the userfile. Note that you can link as many bots as you wish to your botnet.

Secure (TLS) Links
^^^^^^^^^^^^^^^^^^
Since Eggdrop 1.8.0, the ability to encrypt bot links using TLS is possible. On the hub bot you would prefix the port given in the `listen` command with a +, and when you add the hub bot to the leaf, you would prefix the port used in the `.+bot` command with a +. In other words, you would set `listen +5555` in the hub config and use `.+bot hubbot 1.2.3.4 +5555` on the leaf bot. These settings are explained more thoroughly in the `TLS botnet documentation. <https://docs.eggheads.org/using/tls.html#botnet>`_


Using botflags
--------------

Botflags are needed to assign special functions and tasks to your bots.
Bot flags are set with the '.botattr' command. See '.help botattr' for
help with this command. The following is a list of botflags and their
functions:

  "h" (hub)
    If you want your bot(s) to automatically link/relink, you can assign
    the +h botflag each bot's hub. Note that if you set multiple bots +h,
    the bot only attempts to link to one.


  "a" (alternate)
    If your bots are, for some reason, unable to link to their hub, they
    will attempt to connect to an alternate hub. You can assign a bot as
    an alternate hub by giving it the +a botflag.


  "l" (leaf)
    This flag, assigned to a link bot, will prevent the link bot from linking
    other bots to your botnet.


  "r" (reject)
    If you assign this flag to a link bot, the link bot will not be allowed
    to link to the botnet.


  "i" (isolate)
    This flag isolates a link bot's partyline from the rest of the botnet.
    Anything said on the link bot's partyline won't appear on the rest of
    the botnet.


  "s" (SEND userfile to)
    \+s   Giving a link bot this flag will make the bot share aggressively
     with the link bot. See 'Aggressive Share' in section 2 of this
     document for more information on aggressive sharing.

  "\|s" (channel-specific sharing)
    +s bots need this flag for each channel you want to share.


  "p" (ACCEPT userfile from)
    Giving a link bot this flag will make the bot share passively with
    the link bot. See 'Passive Share' in section 2 of this document for
    more information on passive sharing.

  "g" (global share)
    This flag allows the sharing of all channels with a link bot.

  "0-9" (user-defined)
    These 10 flags are user-defined can be used by scripters.


Making bots share user records
------------------------------

  Before you start preparing your bots for sharing, make sure that
  you've loaded the transfer and share modules. You also have to ensure
  that each channel you wish to share is set +shared (see '.help
  chanset' and '.help chaninfo').

  By using specific botflags, you can cause your bot to share
  aggressively with some link bots, and passively with others. For
  sharing to work, flags must be set properly on both the passive and
  the aggressive bots. An aggressive  bot will not share userfiles with
  another aggressive bot; a passive bot will not share userfiles with
  another passive bot.

  First off, let's say we have two bots we want to link. We will
  call one Lamestbot, and the other Lameshare. The first thing that needs
  to be done is each bot needs the other bot added to its user record.
  Your botnet should have a hub bot. This will have them connect
  automatically whenever they are started. Without a hub, you would have to
  manually link them with the .link command. For this situation we will
  make Lamestbot the hub for our small botnet. Let's also use a channel
  called #eggdrop as the one we want to share user channel flags with. Do
  the following:

  On Lamestbot::

    .+bot Lameshare eggdrop.com 3333

  This command adds a user record to
  Lamestbot for Lameshare. Lameshare is running from eggdrop.com and is
  on port 3333. If Lameshare were to have a separate port for users/relays
  we would just add a '/' and the port number, i.e. 3333/5555::

    .botattr Lameshare +s

  This tells us that Lamestbot will only send
  user files to Lameshare; Lameshare will not send them to it::

    .botattr Lameshare |s #eggdrop

  This sets up sharing of the channel
  flags for #eggdrop between the bots. Without this, they will not share
  channel flags only global flags for the users

  On Lameshare::

    .+bot Lamestbot best.com 3333/5555

  Again this will add a user on
  Lameshare called Lamestbot with the domain of best.com. The bot has
  two ports, 3333 for bot communications and 5555 for users/relays::

    .botattr Lamestbot +hp

  This command sets Lamestbot as the hub and
  also as a passive share, which means Lameshare will accept user files
  from Lamestbot:::

    .botattr Lamestbot |s #eggdrop

  This sets #eggdrop as a share channel

  Our botnet::

   Lamestbot
     `-+Lameshare

  Let's add a third bot called beldin to this scenario:

  On Lamestbot::

    .+bot beldin llama.com 3333

    .botattr beldin s|s #eggdrop

  Notice how i piped (the | character)
  the channel flag, also saving time.)

  Also note that you don't have to add beldin on Lameshare. Since
  they are already sharing, it was added automatically. The one thing that
  you should note is that no bot flags will be shared. If you set beldin as
  +s (Aggressive share) on the hub (Lamestbot) he will not be set on the
  other bots as that. The same with the channel +s flag. All other flags
  will be shared such as the o, f, etc. Now that we have three bots, we
  can also set up one as an alternate hub. The alternate hub is the bot
  that the bots will auto-connect to in the event the hub goes down or
  is unreachable.

  Let's make beldin an alternate hub for our little botnet.

  On Lameshare::

    .botattr beldin +a

  That's all there is to it. Again, since bot flags are not shared,
  you would have to add the bot flag +a for beldin on them all. The only
  ones you would not have to do this on are beldin and the hub (Lamestbot).
  Of course, if you had more bots, you would have to add beldin as a +a on
  them, but you would not do it on the hub or beldin.

  Our botnet::

    Lamestbot
      |-+beldin
      `-+Lameshare

Using certificates to authenticate Eggdrops
-------------------------------------------
Eggdrops can use certificates to authenticate when linking to each other instead of a password. First, you must ensure you have set the appropriate certificates in the `ssl-privatekey` and `ssl-certificate` settings in the config file, and then enable the `ssl-cert-auth` setting. Next, add the certificate on the partyline by using `.fprint +` to add the fingerprint for the certificate currently in use, or `.fprint <SHA1 fingerprint>` to manually add a fingerprint. Once the config file settings are set 0and fingerprints are added on the partyline, Eggdrops will attempt to use their certificates instead of passwords for authentication.

Copyright (C) 1999 - 2023 Eggheads Development Team
