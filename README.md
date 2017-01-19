What This Is
=======

It's a lightweight SSH mode for Emacs.
I used this a whole lot at my last job,
which required me bouncing through lots of hops to get to a destination.
Other SSH modes were failing me here, unable to keep up with dirtrack and other things.
I just wanted a slim comint wrapper.

Put another way:
I like Plan 9's `acme`.
If you like Plan 9's `acme`, you might enjoy this.


Why You Should Use This
==================

* You have to use strange SSH implementations like like HP iLOs
* You could benefit from a client that bunches up input by line (for
  instance, you have a high-latency connection and hate being 20
  keystrokes ahead of what's echoed back)
* You need an SSH implementation for Emacs that's fully debugged with
  putty on Windows
* You'd like to have a working `dabbrev-expand` (`M-/`) in your shell
  sessions
* You think it would be nice to have instant search over your entire
  session, even if it spans multiple hosts
* You're a weirdo
* You're a fan of `cmd` in `acme`


Why You Should Not Use This
=================

* You rely heavily on tab completion and can't switch to `dabbrev-expand` (`M-/`)
* You use lots of things that absolutely require a terminal emulator (like Nethack or irssi)
* You love using `more` and `less` more than you love using `cat` and Emacs built-in navigation


How To Use This
========
Drop it somewhere that you can load it up.
Then, in your emacs initialization file:

    (load "neale-ssh.el")
    (setq ssh/default-host "woozle.org")
    (setq ssh/frequent-hosts '("woozle.org" "zork.net"))


Things I've Found Useful
===============

Using `plink`/`putty`
------------------

I have to work in Windows sometimes,
which means I'm using `plink.exe`.
I created an "emacs" profile in `putty` that has everything set up the way I want for `plink`.
Then I tell emacs to use it:

    (setq ssh-explicit-args (if (eq system-type 'windows-nt) '("-load" "emacs") '()))


Editing Remote Files
-----------------

At some point after starting to use this,
you are going to find yourself wanting to edit a remote file,
and then you are going to scratch your head.

You could use `cat filename`,
edit the text straight up in the ssh buffer,
then `cat > filename` to write it back out.

I've been using `ed` a lot,
which combined with emacs editing isn't too bad
(but also not fantastic).

A New Hope For Remote File Editing
---------------

I've been trying to get some key bindings set up that will:
* Dump the remote file
* Capture the dump in a new buffer
* Bind something in the new buffer to send a `cat > $original_filename` command and dump the output

But I'm having quite a bit of trouble with Emacs dropping characters for some reason.
If you're interested in helping,
have a look at [neale-comint-edit.el](neale-comint-edit) and see what you can twiddle out of it.

