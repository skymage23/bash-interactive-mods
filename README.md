# bash-interactive-mods
A (small) SDK for developing and using what I call "interactive mods" ("imods") in Bash.

# What are "Interactive Mods"?
"Interactive mods", or "imods", are Bash shell scriptlets that are intended to enhance
the interactive shell experience. What makes these different from regular
programs is that they treat the human needs as a common linking factor
between them.  Their developer understands that it is the brain of the
user that holds state for the system.

Consider how a Shared Object (Dynamic Library, for the Windows folks) holds
utility functions that are useful in multiple contexts and call orders 
and know that "imods" are likewise for human users. They are
libraries of utility functions that can support a variety of needs, and
exist mainly to make trivial to do what would otherwise be a large and costly
ordeal, time-wise.

As an example, consider working on native code you intend to have on both your own
custom variant of Chromium OS and your own custom variant of Android. A rare situation,
but it is a good example of what types of problems "imods" are intended to solve.
Doing this will require you to simultaneouly work with the Chromium OS SDK and the Android
Open Source Project (AOSP) SDK. One commonality of SDKs in general is that they are usually
tightly containerized with the components held at specific, well-tested versions. Make that
doubly so for OS development kits like these. Instead of having to constantly juggle
multiple chroots, bin paths, library paths, library version nuances, and build scripts
in your head, commit your working mental model to an "imod" with which you can launch,
with a single call to an "init" function, say, "google_os_custom_bin", a shell environment
within whichever SDK you prefer to work in straight from login after a fresh boot,
along with a set of functions that seemlessly enter the alternate chroot whenever building
or working with that SDK is needed. 

True, you can make a script to do this, but using "imods" allows you to separate logic
that can be shared out of the script so that it can be used elsewhere. For example, you
can take parts of the above-mentioned SDK-oriented "imod", abstract away the SDK bits,
and use the bulk of the code its own "imod", and then make another "imod" that depends on
the aforementioned imod for, say, a project where the native Linux backend
and the Windows app share native code, and you want to build and test the code in a Cygwin
environment periodically while doing all development of said code inside of
Windows Subsystem for Linux (WSL).

Using "imods" also removes having to implemement boilerplate code for proper error
handling, logging features, signal traps, etc., as these are all included in the "imod" API.

Finally, as illustrated above, "interactive mods" can, and often will, depend on other "interactive mods",
allowing for code-sharing to minimize writing boilerplate code.


# Great, more software I have to manually version track.
Actually, it is the developers' intent to make it so that "imods" are
included in your Linux distro's package management repositories. This allows
your package manager to handle version tracking and updates. Additionally,
one of our goals is to develop a helper script that will allow developers
to package their "imods" for Debian/Ubuntu (.dpkg) or for Fedora/RHEL/SUSE/OpenSUSE (.rpm)
format regardless of what Linux distro they use for development.

Please understand that this will not happen until development
on the core features of "bash-interactive-mods" is close to
completion. It is simply an issue of lack of development resources.
