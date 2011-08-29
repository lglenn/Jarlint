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

The script looks at the environment for the classpath.

    CLASSPATH=lib/foo.jar:lib/bar.jar:classes
    jarlint


 