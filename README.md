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

Running jarlint
---------------

The script will look in the following places for the classpath, in this order:

1. A file with the name of the first parameter from the command line.
2. The first parameter from the command line. 
3. The CLASSPATH environment variable. 

Examples: 

A file: 

    jarlint classpath.txt

Pass the classpath on the command line: 

    jarlint ./classes:./lib/foo.jar:./lib/bar.jar

Use the environment:

    export CLASSPATH=lib/foo.jar:lib/bar.jar:classes
    jarlint




 