torrentscrape
=============

Torrentscrape is a set of Bash scripts that scrape public trackers and 
generate .strm files for use with the XBMCTorrent plugin to support library 
integration better.

I am doing all development on a XBMCbuntu based install, running the up to date 
version of XBMC, havent switched to Kodi yet. 

This is a bash script, so is not designed to be run from within xbmc, but 
instead run from a shell, or automated via crontab. It is designed to be linux 
only, but might run within cygwin on windows. On my system, I put torrentscrape 
in /usr/local/share/torrentscrape and made a symlink in /usr/local/bin to point 
to the main script:

ln -s /usr/local/share/torrentscrape/torrentscrape /usr/local/bin/torrentscrape

Requirements
============

realpath needs to be installed, "sudo apt-get install realpath" on debian based
systems

Setup
=====

If you need to change where torrentscrape looks for its config files you can 
change the settings in torrentscrape-core, from here out the guide assumes you 
left them with default settings.

A directory for broken magnets needs to be created as ~/.badmagnets/ ... in 
the event that a magnet link refuses to play in XBMCtorrent, just move the 
strm file to the badmagnets directory and re-run the scraper, and it will skip 
that magnet link in the future.

Torrentscrape looks for a configuration file with a list of websites and their 
configuration at ~/.config/torrentscrape.list, an example is provided in 
torrentscrape.list-example

The fields in the list file are:
TYPE = either TV or Movies, I do plan to make an Anime specific scraper in the 
       future.
MODULE = which scraper script to run (eztv tpbtv yifi)
TITLE = Proper Title of the show, be sure to put "\" infront of any spaces or 
        special charachters
WANTED = Strings to search for in the torrent URL
UNWANTED = Strings to match unwanted torrents
MAXPAGES = Maximum number of pages to parse
URL = Copy a URL here from a search you have built up in your browser.


Module Specific Notes
=====================

yifi
----

It is reccomended that after you run a full scrape of Movies you set MAXPAGES 
in the torrentscrape.list for yify to 1. This will cause it to scrape much 
quicker as it will only look up the newest page of magnet links. The only 
exception to this is when updating after adding a file to badmagnets, where 
you might need to look back further than the first page of Movie results.


CREDITS
=======

The start to these scripts came from XMAGP, which I used as a base to create 
these scripts. The original project can be found at:

https://gitorious.org/xmagp/xmagp/source/1aa903f1e38006f43efcd674083a4683d2383cdb:

This script uses the API at Bitsnoop.com for checking seed counts and for torrents
reported as fake.

