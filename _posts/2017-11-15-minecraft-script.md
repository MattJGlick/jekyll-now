---
layout: post
title: Minecraft Server Management Script
---

Once in awhile some of my gaming friends and I will standup a Minecraft server to play around for
a weekend or so. To make this easier I put together a script that handles all of the install and
management for me. We use a Spigot server which allows us to add plugins to tune the game a bit
to our needs. We use Digital Ocean for our hosting which has been terrific so far!

## Quickstart

```
chmod +x mc_server.sh
./mc_server setup
```

## Settings

These are the settings that need to be updated before the rest of the script will work properly:

```
BACKUP_DIR: Directory where backups should be stored
SHUTDOWN_DELAY: Delay between sending the shutdown command and actual shutdown (ex. 5)
SPIGOT_DIR: Directory where the spigot-*.jar lives
TMUX_NAME: name of the tmux session to be used (ex. mc)
```

## Usage

```
$ ./mc_server.sh
Usage: ./mc_server.sh {setup|start|stop|attach|restart|send_msg|status}

$ ./mc_server status
Server is up
There are 0 out of maximum 20 players online.
```

## Cron

To manage backing up the server, I have a cron job setup to backup the server once a day:

```
  crontab -l | { cat; echo "0 5 * * * $SPIGOT_DIR/mc_server backup"; } | crontab -
```

Overall this has worked out great for standing up and managing our Spigot server. If you'd like more
info on how we use our Minecraft server feel free to shoot me a message!
