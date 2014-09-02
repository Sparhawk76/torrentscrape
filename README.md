torrentscrape
=============

Torrentscrape is a set of Bash scripts that scrape public trackers and 
generate .strm files for use with the XBMCTorrent plugin to support library 
integration better.

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
configuration at ~/.config/torrentscrape.list

The fields in the configuration file are:
TYPE = either TV or Movies, I do plan to make an Anime specific scraper in the 
       future.
MODULE = which scraper script to run (eztv tpbtv yifi)
TITLE = Proper Title of the show, be sure to put "\" infront of any spaces or 
        special charachters
WANTED = Strings to search for in the torrent URL
UNWANTED = Strings to match unwanted torrents
URL = Copy a URL here from a search you have built up in your browser.

An example torrentscrape.list is posted below. Fields are separated by a 
<SPACE>, <TAB> will not work. 

# scraper config
#
#TYPE MODULE TITLE     WANTED  UNWANTED URL
TV eztv Grimm HDTV|720p JUNK https://eztv.it/shows/556/grimm/
TV eztv Marvels\ Agents\ of\ S.H.I.E.L.D. HDTV|720p JUNK https://eztv.it/shows/878/marvels-agents-of-shield/
TV eztv Game\ of\ Thrones HDTV JUNK https://eztv.it/shows/481/game-of-thrones/
TV eztv Mythbusters HDTV JUNK https://eztv.it/shows/192/mythbusters/
TV tpbtv The\ Strain 1080p JUNK http://thepiratebay.se/search/the%20strain/0/99/208/
Movies yify MOVIES 1080p JUNK https://yts.re/browse-movie/0/1080p/All/6/year/



Module Specific Notes
=====================

yifi
----

It is reccomended that after you run a full scrape of Movies you set MAXPAGES 
in torrentscrape-yifi to 1. This will cause it to scrape much quicker as it 
will only look up the newest page of magnet links. The only exception to this 
is when updating after adding a file to badmagnets, where you might need to 
look back further than the first page of Movie results.

By default it will scrape 50 pages of output, and will stop if it gets to a 
movie from 2007, these settings can also be changed in torrentscrape-yifi.
