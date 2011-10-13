===============
POWDER Wii Port
===============

Source for the `Wii port`_ of `POWDER`_, a Roguelike designed for the Gameboy
Advance and Nintendo DS, offering accessibility without sacrificing any of
the depth or challenge you'd expect of the genre.

POWDER itself is not open source, but its `source is available`_ under a
`Creative Commons Sampling Plus`_ license, should you wish to build the Wii
version yourself.

Files for the Wii port are provided in the ``port/`` directory.

All other changes made while creating the Wii build are provided in
``non_port_changes.diff``, which can be applied using GNU patch::

   patch -p0 < non_port_changes.diff

.. _`Wii port`: http://wiibrew.org/wiki/Powder
.. _`POWDER`: http://www.zincland.com/powder/
.. _`source is available`: http://www.zincland.com/powder/index.php?pagename=release
.. _`Creative Commons Sampling Plus`: http://creativecommons.org/licenses/sampling+/1.0/

Building
========

Grab the POWDER source (version 116 at the time of typing), copy the Wii
port directory over and apply the patch.

Support Files
-------------

On Windows, I use `Cygwin`_ (with the ``make`` and ``g++`` packages
installed) to build the support files - this should be as simple as changing
to the ``port/linux/`` directory and invoking ``make premake``.

.. _`Cygwin`: http://cygwin.com

Wii Build
---------

The Wii build toolchain is `devkitpro and devkitPPC`_.

Ensure you have `SDL Wii`_ and its dependencies available in your
``libogc`` directory as per its usage instructions.

Change to the ``port/wii/`` directory and invoke ``make``.

To test, start the `Homebrew Channel`_ on your Wii and invoke
``make run``.

.. _`devkitpro and devkitPPC`: http://devkitpro.org/wiki/Getting_Started
.. _`SDL Wii`: http://code.google.com/p/sdl-wii/
.. _`Homebrew Channel`: http://wiibrew.org/wiki/Homebrew_Channel
