Unisonbox
=========
Author: Tim Creech

### Disclaimer
This project is provided as-is, without any express or implied warranty. Although I have used it without incident for a year or so, I cannot be held responsible for any related losses or damages. I would advise the use of automated backups just in case something goes terribly wrong!

Explanation
-----------

This is a small collection of simple scripts I use on my personal machines to
effect Dropbox-like synchronization on my machines. Each machine stores all
synchronized files locally, and these scripts take care of regularly keeping
things up to date. A central server is required, around which your nodes will
form a simple star toplogy.

I created this for personal use, and thought that it might be useful as a
starting point for others who want to set up something similar.  You will
probably have to change each file in this repository a bit in order to get
things up and running.

*All* of the heavy lifting is done by the excellent Unison File Synchronizer from UPenn. (www.cis.upenn.edu/~bcpierce/unison/)

Installation
------------

Quick guide to getting a "box" set up.

### Client Requirements
* Unison (the same version on all participating nodes!)
* Something like crontab or launchd to regularly run the sync command
* The `choose-tcp-host` command (included in this repo)

### Server Requirements
* Properly populated `~/.ssh/authorized_keys`
* Unison

### General Idea
Create a script based on `boxsync` for your directory to sync. For example, I like to sync `~/school`, so I create a `~/bin/schoolsync` script based on `boxsync`. Edit this script to set up the configuration variables, which are mostly self-explanatory. Make sure that you give it the correct location of `choose-tcp-host`, and a good list of hostnames to check. For example, on your laptop client, you might set `HOSTLIST="server.local server.selfip.com"` to have the laptop access your server on the local network if available, and otherwise go over the internet. Of course, it's fine to just put a single host in this list. Based on the name you gave the script, a log will be created in /tmp/. For `schoolsync`, this log is `/tmp/schoolsync.log`. This script just needs to run on all the clients, not the sever.

You can do a test sync by manually invoking your sync script. After things are working and you are comfortable with what is happening, schedule the script to be run every few minutes automatically. Cron and launchd examples are included in this repository.

