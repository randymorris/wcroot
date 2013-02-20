wcroot
======
Invoking `wcroot` will determine whether the current directory is
inside a working copy of a version controlled repository and print the
full path to the root of the working copy to stdout.  If no working
copy is found then `wcroot` simply does nothing.


Currently supported working copy formats:

 * [Git](http://git-scm.com/)
 * [Mercurial](http://mercurial.selenic.com/)
 * [Subversion](http://subversion.apache.org/)

Example usage
-------------

Normal usage:

    [user@host ~/dev/root/subdirectory]$ wcroot
    /home/user/dev/root
    [user@host ~/dev/root/subdirectory]$

Path as a parameter:

    [user@host ~]$ wcroot ~/dev/root/subdirectory
    /home/user/dev/root
    [user@host ~]$

Outside of a working copy:

    [user@host ~/not/a/working/copy]$ wcroot
    [user@host ~/not/a/working/copy]$

In a script:

    # `cd` with no arguments will first attempt to change to the root of
    #  the current working copy.  If already at the root or no working
    #  copy is found, cd to $HOME.
    function cd() {
        root=$(wcroot)
        if [ $# -ne 0 ]; then
            builtin cd "$1"
        elif [ -n "$root" -a "$PWD" != "$root" ]; then
            builtin cd "$root"
        else
            builtin cd
        fi
    }
