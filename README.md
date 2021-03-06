JARLINT!
========

Overview
--------

Jarlint is a pretty basic Perl script that will look at your Java classpath, and look for the following:

* elements that don't exist in the filesystem
* duplicate elements (same path, more than once)
* binary duplicates (different paths, same bits)
* worrisome duplicates (same filename, different bits, different paths -- uh-oh!)
* multiple versions (a fuzzy match that'll look for e.g. foo.jar and foo-1.2.jar)

After trolling through your system, jarlint will produce a report that outlines what it found, what's a problem, and why. And it's marked up with [markdown](http://daringfireball.net/projects/markdown/) so it's readable as-is, but can also be easily prettied up with HTML conversion and CSS if you want to use it in a more formal setting. 

Much as I'd like to write this in something more fun, Perl is pretty reliably going to be on any box, and Java is too much of an arse-ache.

Dependencies
------------

You'll need to have the Digest::MD5 Perl module installed. That's pretty standard, though. To confirm that you have it, do this from the command line: 

    perl -MDigest::MD5

If nothing happens, you're good (hit ctrl-d to get on with things). If you get an error message, you're not good, and you'll need to get the module installed. 

Installation
------------

In the directory where you'd like to keep the jarlint script, run these two commands: 

    curl -fsSL https://raw.github.com/lglenn/Jarlint/master/jarlint > jarlint

    chmod a+x jarlint

Or:

* Download a installation tarball/zipfile from Github at https://github.com/lglenn/Jarlint/archives/master
* Un(tar|zip) the install file
* Copy the jarlint script to the plave you'd like to keep it
* Just to be sure, do a `chmod a+x jarlint` on it. 

Running jarlint
---------------

The script will look in the following places for the classpath, in this order:

1. A file with the name of the first parameter from the command line.
2. The first parameter from the command line.
3. The CLASSPATH environment variable.

Jarlint can read two kinds of files: text files that contain a CLASSPATH Unix-style environment variable declaration, and Blue Martini log files. In each case, jarlint will read the file until it finds the classpath, and then close it. It won't, for example, read all of a 2-gig Blue Martini log file. 

If the classpath contains relative paths (e.g. './lib/foo.jar'), make sure that you run jarlint from someplace where those paths will resolve correctly.

### Examples:

Pass the classpath on the command line:

    jarlint ./classes:./lib/foo.jar:./lib/bar.jar

Pass a filename on the command line:

    jarlint classpath.txt

Pass the name of a Blue Martini log on the command line: 

    jarlint website.log

Use the environment:

    export CLASSPATH=lib/foo.jar:lib/bar.jar:classes
    jarlint
