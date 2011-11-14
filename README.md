Unisonbox
=========

Explanation
-----------

This is a small collection of simple scripts I use on my personal machines to
effect Dropbox-like synchronization on my machines. Each machine stores all
synchronized files locally, and these scripts take care of regularly keeping
things up to date. You will probably have to change each file in this
repository a bit in order to get things up and running.

### Author

Installation
------------

Quick guide to getting a "box" set up.

### Client Requirements
* Unison (the same version on all participating nodes!)
* Something like crontab or launchd to regularly run the sync command
* The `choose-tcp-host` command (included in this repo)

### Server Requirements
* Properly populated `~/.ssh/authorized_keys`

### General Idea
Create a script based on `boxsync` for your directory to sync. I like to sync `~/school`, so I have created a `~/bin/schoolsync` script. Edit this script to set up the configuration variables. Make sure that you give it the correct location of `choose-tcp-host`, and a good list of hostnames to check. For example, on your laptop client, you might set `HOSTLIST="server.local server.selfip.com"` to have the laptop access your server on the local network if available, and otherwise go over the internet. Based on the name you gave the script, a log will be created in /tmp/. For `schoolsync`, this log is `/tmp/schoolsync.log`. This script just needs to run on all the clients, not the sever.

You can do a test sync by manually invoking your sync script. After things are working and you are comfortable with what is happening, schedule the script to be run every few minutes using. Cron and launchd examples are included in this repository.

