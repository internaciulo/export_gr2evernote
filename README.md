export2enex and export_gr2evernote
==================

Exports previously-starred articles from Google Reader to Evernote

Executive Summary: Unless you like crappy imported notes, you should use export2enex.py.
export_gr2evernote.py uses Evernote's e-mail submission feature, which mangles
any HTML in the note, rendering it a pile of markup gibberish.

Run with -h to see available options.

If you use Google Reader (and probably even if you don't), you probably know 
that Google has announced they're shutting it down on July 1.  I've
got hundreds of starred articles in Reader, and I'd like to get them into
a service that I have more control over.  Since Evernote stores your data
locally on your devices, I've found it's a good service for keeping my 
data in the cloud without running the risk of losing it if/when Evernote
goes away.

export2enex takes the exported JSON file produced by Google's Takeout
(namely, 'starred.json') and dumps it into Evernote, using Evernote's 
export file format (.enex).  Unlike export_gr2evernote.py, this approach
does a pretty good job of preserving the formatting of the note.  Also,
since it's all local, there are no limits to how many notes you can 
import in one go.  Unless you have a compelling reason to use the 
e-mail submission script (like, say, you want ugly notes with a bunch
of extraneous markup), you should use this script to export your Reader
JSON into Evernote enex format.  Once you have it in enex format, you
can import it into Evernote using the desktop client.
    Usage: export2enex.py [options] > filename.enex

export_gr2evernote.py takes the exported JSON file produced by Google's 
Takeout (namely, 'starred.json') and dumps it into Evernote, using Evernote's 
e-mail note submission feature.  It doesn't do any formatting of what it
sends to Evernote, so it will most likely look pretty ugly in Evernote.
I looked into the possibility of using ENML (Evernote's markup language),
but apparently it's not possible to submit notes via email that are encoded with
ENML--the ENML is escaped so that it just appears as normal text in the note 
in Evernote.
There is an ENML editor (http://enml-editor.ping13.net/) that allows you 
to edit your notes, but that's a manual process that I've found to be
quite tedious due to all the special characters that are escaped (e.g.,
&quot; ).  I think it might be possible to do some processing of the raw 
JSON to make it easier to use this editor as a final, finishing step, but
I haven't investigated that too closely yet.

Note that if you have a lot of starred articles, you can blow through your 
daily e-mail upload limit quite easily!  As of this writing, free accounts 
have a limit of 50 e-mails per day; premium accounts have a limit of 250.
To accomodate that limitation, the script keeps track of where it left off 
each day (by writing a python pickle file in the current working directory) 
so that when you run it on subsequent days, you can simply use the --continue 
option to continue your article dump.
