Select Terminfo Descriptions
------------------------------------------------------------------------------

It's good to carry some terminfos around in our provisioned home dirs,
rather than deal with systems that don't have the descriptions or have
up-to-date ones.

Then of course, we do have to keep them up to date.  The library
``libtinfo.so`` will look in ``~/.terminfo/`` first for a compiled
database -- as long as `$TERMINFO` does not override that -- before
consulting the system locations.


Updating from upstream
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For example::

   $ git url
  https://github.com/ThomasDickey/ncurses-snapshots

   $ git tag -l | grep ^v | sort -V | tail -1
  v6_5_20250802

   $ git checkout `!!`
   $ mkdir ~/.terminfo2
   $ tic -x -o ~/.terminfo2 -e tmux-256color ~/upsrc/ncurses/misc/terminfo.src

Now to compare the old and new::

   $ infocmp -A ~/.terminfo -B ~/.terminfo2 tmux-256color tmux-256color

If it changed and those changes are desired, replace ``t/tmux-256color``
in the source repo and commit.

Note that the compiled database does dereference all `use=` sections, so
the desciption is indeed standalone.
