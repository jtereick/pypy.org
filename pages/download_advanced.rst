.. title: Download (advanced)
.. slug: download_advanced
.. date: 2020-11-21 16:14:02 UTC
.. tags:
.. category:
.. link:
.. description:

.. contents::
    :depth: 2

We provide pre-compiled binaries for many platforms and OSes:

* the Python2.7 compatible release — **PyPy2.7 v7.3.6**

* the Python3.7 compatible release — **PyPy3.7 v7.3.7**

* the Python3.8 compatible release — **PyPy3.8 v7.3.7**

.. note::

  Our `nightly binary builds`_ have the most recent bugfixes and performance
  improvements, though they can be less stable than the official releases. See
  this link for `older versions`_.

.. _`nightly binary builds`: https://buildbot.pypy.org/nightly/
.. _`older versions`: https://downloads.python.org/pypy/

..
  table start

..
  Anonymous tags work, this kind of tag doesn't ``Download <linux64-pypy3.7>``

.. list-table:: `PyPy latest`_
   :widths: 20 15 15 15 35
   :header-rows: 1

   * - OS
     - PyPy3.8
     - PyPy3.7
     - PyPy2.7
     - Notes

   * - **Linux x86 64 bit**
     - Download__
     - Download__
     - Download__
     - compatible with CentOS6 and later

   * - **Windows 64 bit**
     - Download__
     - Download__
     - Download__
     - compatible with any windows 64-bit

       you might need the VC runtime library installer `vcredist.x64.exe`_

   * - **MacOS**

     - Download__
     - Download__
     - Download__
     - High Sierra >= 10.13, not for Sierra and below. Not signed, for signed
       packages use Homebrew_.

   * - **Linux ARM64**

     - Download__
     - Download__
     - Download__
     - compatible with CentOS7 and later

.. __: https://downloads.python.org/pypy/pypy3.8-v7.3.7-linux64.tar.bz2
.. __: https://downloads.python.org/pypy/pypy3.7-v7.3.7-linux64.tar.bz2
.. __: https://downloads.python.org/pypy/pypy2.7-v7.3.6-linux64.tar.bz2

.. __: https://downloads.python.org/pypy/pypy3.8-v7.3.7-win64.zip
.. __: https://downloads.python.org/pypy/pypy3.7-v7.3.7-win64.zip
.. __: https://downloads.python.org/pypy/pypy2.7-v7.3.6-win64.zip

.. __: https://downloads.python.org/pypy/pypy3.8-v7.3.7-osx64.tar.bz2
.. __: https://downloads.python.org/pypy/pypy3.7-v7.3.7-osx64.tar.bz2
.. __: https://downloads.python.org/pypy/pypy2.7-v7.3.6-osx64.tar.bz2

.. __: https://downloads.python.org/pypy/pypy3.8-v7.3.7-aarch64.tar.bz2
.. __: https://downloads.python.org/pypy/pypy3.7-v7.3.7-aarch64.tar.bz2
.. __: https://downloads.python.org/pypy/pypy2.7-v7.3.6-aarch64.tar.bz2

.. _`PyPy latest`: https://doc.pypy.org/en/latest/release-v7.3.7.html
.. _`vcredist.x64.exe`: https://www.microsoft.com/en-us/download/details.aspx?id=52685

..
  table finish


.. list-table:: Other Platfoms
   :widths: 20 15 15 15 35
   :header-rows: 1

   * - OS
     - PyPy3.8
     - PyPy3.7
     - PyPy2.7
     - Notes

   * - **Linux x86 32 bit**

     - Download__
     - Download__
     - Download__
     - compatible with CentOS6 and later

   * - **PowerPC PPC64**

     - n/a
     - n/a
     - 7.3.1__
     - 64bit big-endian, Fedora 20 [1]_

   * - **PowerPC PPC64le**

     - n/a
     - n/a
     - 7.3.1__
     - 64bit little-endian, Fedora 21 [1]_

   * - **S390x**

     - Download__
     - Download__
     - Download__
     - built on Redhat Linux 7.2 [1]_


.. __: https://downloads.python.org/pypy/pypy3.8-v7.3.7-linux32.tar.bz2
.. __: https://downloads.python.org/pypy/pypy3.7-v7.3.7-linux32.tar.bz2
.. __: https://downloads.python.org/pypy/pypy2.7-v7.3.6-linux32.tar.bz2

.. __: https://downloads.python.org/pypy/pypy2.7-v7.3.1-ppc64.tar.bz2

.. __: https://downloads.python.org/pypy/pypy2.7-v7.3.1-ppc64le.tar.bz2

.. __: https://downloads.python.org/pypy/pypy3.8-v7.3.7-s390x.tar.bz2
.. __: https://downloads.python.org/pypy/pypy3.7-v7.3.7-s390x.tar.bz2
.. __: https://downloads.python.org/pypy/pypy2.7-v7.3.6-s390x.tar.bz2

.. [1]
  Linux binaries are provided for the
  distributions listed here.  **If your distribution is not exactly this
  one, it won't work,** you will probably see:
  ``pypy: error while loading shared libraries: ...``.

.. _`Default (with a JIT Compiler)`:

"JIT Compiler" version
-------------------------------

The binaries above include a Just-in-Time compiler. On x86-32, they only work on
CPUs that have the SSE2 instruction set (most of them do, nowadays).. They also
contain `stackless`_ extensions, like `greenlets`_.

Linux binaries and common distributions
---------------------------------------

Since version 7.3, the linux x86 binaries ship with versions
of OpenSSL, SQLite3, libffi, expat, and TCL/TK binary libraries linked in. This
make the binaries "portable" so that they should run on any current glibc-based
linux platform. The ideas were adopted from the `portable-pypy`_ package.

This solution to the portability problem means that the versions of the
packaged libraries are frozen to the version shipped, so updating your system
libraries will not affect this installation of PyPy. Also see the note about
SSL certificates below.

For s390x, and ppc64, the binaries target a specific operating system.
These binaries are dynamically linked, and thus might not be usable due to the
sad story of linux binary compatibility.  This means that **Linux binaries are
only usable on the distributions written next to them** unless you're ready to
hack your system by adding symlinks to the libraries it tries to open.  There
are better solutions:

* download PyPy from your release vendor (usually an outdated
  version): `Ubuntu`_ (`PPA`_), `Debian`_, `Homebrew`_, MacPorts,
  `Fedora`_, `Gentoo`_ and `Arch`_ are known to package PyPy, with various
  degrees of being up-to-date. FreshPorts_ packages for FreeBSD.

* use conda_, (for MacOS) which will also enable installing binary-compiled
  packages.

* `recompile the CFFI-based`_ TCL/TK, OpenSSL, or sqlite3 modules, using system
  libraries and the scripts in ``pypy/lib_pypy/pypy_tools``. This solution will
  not solve compatibility issues with libffi, since that is baked into PyPy.

* or translate_ your own PyPy.

..
  notes_and_links start

.. note::

    SSL Certificates

    While the linux binaries ship an OpenSSL library, they do not ship a
    certificate store for SSL certificates. If you wish to use SSL module,
    you will need a valid certificate store. You can use the `certifi`_ package
    and set ``SSL_CERT_FILE`` to ``certifi.where()`` or install your platform
    certificates which should be discovered by the ``_ssl`` module.


.. _`Ubuntu`: https://packages.ubuntu.com/search?keywords=pypy&searchon=names
.. _`PPA`: https://launchpad.net/~pypy/+archive/ppa
.. _`Debian`: https://packages.debian.org/sid/pypy
.. _`Fedora`: https://fedoraproject.org/wiki/Features/PyPyStack
.. _`Gentoo`: https://packages.gentoo.org/package/dev-python/pypy
.. _`Homebrew`: https://github.com/Homebrew/homebrew-core/blob/master/Formula/pypy.rb
.. _`Arch`: https://wiki.archlinux.org/index.php/PyPy
.. _`portable-pypy`: https://github.com/squeaky-pl/portable-pypy#portable-pypy-distribution-for-linux
.. _`recompile the CFFI-based`: https://doc.pypy.org/en/latest/build.html#build-cffi-import-libraries-for-the-stdlib
.. _`certifi`: https://pypi.org/project/certifi/
.. _conda: https://conda-forge.org/blog/posts/2020-03-10-pypy/

..
  notes_and_links finish


Previous version can be downloaded from here__, or directly from the buildbot's
mirror_.

.. __: https://downloads.python.org/pypy/
.. _mirror: https://buildbot.pypy.org/mirror/
.. _FreshPorts: https://www.freshports.org/lang/pypy


If your CPU is really, really old, it may be a x86-32 without SSE2.
There is untested support for manually translating PyPy's JIT without
SSE2 (``--jit-backend=x86-without-sse2``) but note that your machine
is probably low-spec enough that running CPython on it is a better
idea in the first place.

PyPy-STM 2.5.1
--------------

This is a special version of PyPy!  See the `Software Transactional
Memory`_ (STM) documentation.

* `PyPy-STM Linux x86-64 binary (64bit, tar.bz2 built on Ubuntu 12.04 - 16.04)`__

.. _`Software Transactional Memory`: https://doc.pypy.org/en/latest/stm.html
.. __: https://downloads.python.org/pypy/pypy-stm-2.5.1-linux64.tar.bz2


.. _`Other versions (without a JIT)`:

Other versions
--------------

The other versions of PyPy are:

* Try the most up-to-date `nightly binary builds`_ , if the official
  release is too old for what you want to do.

* Reverse debugger: This version enables debugging your Python
  programs by going forward and backward in time.  See the `RevDB
  documentation`__.

.. __: https://foss.heptapod.net/pypy/revdb/

* Old-style sandboxing: A special safe version.
  *This is NOT the version announced in-development during 2019!*
  Read the docs about sandboxing_.
  This version is **not supported** and not actively maintained.  You
  will likely have to fix some issues yourself, or checkout an old
  version, or otherwise play around on your own.  We provide this
  documentation only for historical reasons.  Please do not use in
  production.  For reference, there are some very old, unmaintained
  binaries for Linux (32bit__, 64bit__).

.. __: https://downloads.python.org/pypy/pypy-1.8-sandbox-linux64.tar.bz2
.. __: https://downloads.python.org/pypy/pypy-1.8-sandbox-linux.tar.bz2
.. _`sandbox docs`: https://doc.pypy.org/en/latest/sandbox.html

.. _`nightly binary builds`: https://buildbot.pypy.org/nightly/

Installing
----------

All binary versions are packaged in a ``tar.bz2`` or ``zip`` file.  When
uncompressed, they run in-place.  You can uncompress them
either somewhere in your home directory or, say, in ``/opt``.
If you want, put a symlink from somewhere like
``/usr/local/bin/pypy`` to ``/path/to/pypy_expanded/bin/pypy``.  Do
not move or copy the executable ``pypy`` outside the tree --- put
a symlink to it, otherwise it will not find its libraries.


Installing more modules
-----------------------

There are as yet few distribution-ready packages. `conda`_ is one easy
way to get packages with a minimum of compilation.
We recommend installing ``pip``, which is the standard package
manager of Python.  It works like it does on CPython as explained in the
`installation documentation`_.

If you use your distribution's PyPy package we recommend you install packages
into a virtualenv. If you try to build a module and the build process complains
about "missing Python.h", you may need to install the pypy-dev package.

.. _installation documentation: https://doc.pypy.org/en/latest/install.html

.. _translate:

Building from source
--------------------

(see more build instructions_)


1. Get the source code.  The preferred way is to checkout the current
   trunk using Mercurial_.  The trunk usually works and is of course
   more up-to-date:

   .. code-block:: bash

     hg clone https://foss.heptapod.net/pypy/pypy

   The trunk contains PyPy 2.  For PyPy 3, switch to the correct branch:

   .. code-block:: bash

     # switch to the branch that implements Python 3.7
     hg update py3.7

   Alternatively, get one of the following smaller packages for the source at
   the same revision as the above binaries:

   * `pypy2.7-v7.3.6-src.tar.bz2`__ (sources, PyPy 2.7 only)
   * `pypy3.7-v7.3.7-src.tar.bz2`__ (sources, PyPy 3.7 only)
   * `pypy3.8-v7.3.7-src.tar.bz2`__ (sources, PyPy 3.8 only)

   .. __: https://downloads.python.org/pypy/pypy2.7-v7.3.6-src.tar.bz2
   .. __: https://downloads.python.org/pypy/pypy3.7-v7.3.7-src.tar.bz2
   .. __: https://downloads.python.org/pypy/pypy3.8-v7.3.7-src.tar.bz2


2. Make sure you **installed the dependencies.**  See the list here__.

   .. __: https://pypy.readthedocs.org/en/latest/build.html#install-build-time-dependencies

3. Enter the ``goal`` directory:

   .. code-block:: bash

     cd pypy/pypy/goal

4. Run the ``rpython`` script.  Here are the common combinations
   of options (works also with ``python`` instead of ``pypy``;
   requires CPython 2.7 or PyPy 2, even to build PyPy 3):

   .. code-block:: bash

     # get the JIT version
     pypy ../../rpython/bin/rpython -Ojit targetpypystandalone
     # get the no-jit version
     pypy ../../rpython/bin/rpython -O2 targetpypystandalone
     # get the sandbox version
     pypy ../../rpython/bin/rpython -O2 --sandbox targetpypystandalone

5. Enjoy Mandelbrot ``:-)``  It takes on the order of half an hour to
   finish the translation, and about 3GB of RAM on a 32-bit system
   and about 5GB on 64-bit systems.  (Do not start a translation on a
   machine with insufficient RAM!  It will just swap forever.  See
   notes below in that case.)

6. If you want to install this PyPy as root, please read the next section,
   Packaging_.

Notes:

* It is recommended to use PyPy to do translations, instead of using CPython,
  because it is twice as fast.  You should just start by downloading an
  official release of PyPy (with the JIT).  If you really have to use CPython
  then note that we are talking about CPython 2.7 here, not CPython 3.x.
  (Older versions like 2.6 are out.)

* On some 32-bit systems, the address space limit of 2 or 3 GB of RAM
  can be an issue.  More generally you may be just a little bit low of
  RAM.  First note that 2 GB is really not enough nowadays; on Windows
  you first need to refer to the `Windows build instructions`_.  More
  precisely, translation on 32-bit takes at this point 2.7 GB if PyPy is
  used and 2.9 GB if CPython is used.  There are two workarounds:

  1. use PyPy, not CPython.  If you don't have any PyPy so far, not even
  an older version, then you need to build one first, with some parts
  removed.  So, first translate with:

  .. code-block:: shell

     cpython2 rpython -Ojit targetpypystandalone \
     --withoutmod-micronumpy --withoutmod-cpyext

  then copy ``pypy-c`` and ``libpypy_c.so`` somewhere else, and finally
  call it with ``...pypy-c ../../rpython/bin/rpython -Ojit``.

  2. if even using PyPy instead of CPython is not enough, try to tweak
  some internal parameters.  Example (slower but saves around 400MB):

  .. code-block:: bash

    PYPY_DONT_RUN_SUBPROCESS=1 PYPY_GC_MAX_DELTA=200MB \
    pypy --jit loop_longevity=300 ../../rpython/bin/rpython \
    -Ojit --source
    # then read the next point about --source

* You can run translations with ``--source``, which only builds the C
  source files (and prints at the end where).  Then you can ``cd`` there
  and execute ``make``.  This is another way to reduce memory usage.
  Note that afterwards, you have to run manually ``pypy-c
  .../pypy/tool/build_cffi_imports.py`` if you want to be able to import
  the cffi-based modules.

* Like other JITs, PyPy doesn't work out of the box on some Linux
  distributions that trade full POSIX compliance for extra security
  features.  E.g. with PAX, you have to run PyPy with ``paxctl -cm``.
  This also applies to translation (unless you use CPython to run the
  translation and you specify ``--source``).

.. _instructions: https://pypy.readthedocs.org/en/latest/build.html
.. _`x86 (IA-32)`: https://en.wikipedia.org/wiki/IA-32
.. _`x86-64`: https://en.wikipedia.org/wiki/X86-64
.. _SSE2: https://en.wikipedia.org/wiki/SSE2
.. _`contact us`: contact.html
.. _`sandboxing`: features.html#sandboxing
.. _`stackless`: https://www.stackless.com/
.. _`greenlets`: https://pypy.readthedocs.org/en/latest/stackless.html#greenlets
.. _`Windows build instructions`: https://doc.pypy.org/en/latest/windows.html#preparing-windows-for-the-large-build
.. _`shadow stack`: https://pypy.readthedocs.org/en/latest/config/translation.gcrootfinder.html
.. _Mercurial: https://www.mercurial-scm.org/

Packaging
---------

Once PyPy is translated from source, a binary package similar to those
provided in the section `Default (with a JIT Compiler)`_ above can be
created with the ``package.py`` script:

.. code-block:: bash

    cd ./pypy/pypy/tool/release/
    python package.py --help  # for information
    python package.py --archive-name pypy-my-own-package-name

It is recommended to use package.py because custom scripts will
invariably become out-of-date.  If you want to write custom scripts
anyway, note an easy-to-miss point: some modules are written with CFFI,
and require some compilation.  If you install PyPy as root without
pre-compiling them, normal users will get errors:

* PyPy 2.5.1 or earlier: normal users would see permission errors.
  Installers need to run ``pypy -c "import gdbm"`` and other similar
  commands at install time; the exact list is in `package.py`_.  Users
  seeing a broken installation of PyPy can fix it after-the-fact if they
  have sudo rights, by running once e.g. ``sudo pypy -c "import gdbm``.

* PyPy 2.6 and later: anyone would get ``ImportError: no module named
  _gdbm_cffi``.  Installers need to run ``pypy _gdbm_build.py`` in the
  ``lib_pypy`` directory during the installation process (plus others;
  see the exact list in `package.py`_).  Users seeing a broken
  installation of PyPy can fix it after-the-fact, by running ``pypy
  /path/to/lib_pypy/_gdbm_build.py``.  This command produces a file
  called ``_gdbm_cffi.pypy-41.so`` locally, which is a C extension
  module for PyPy.  You can move it at any place where modules are
  normally found: e.g. in your project's main directory, or in a
  directory that you add to the env var ``PYTHONPATH``.

.. _`package.py`: https://foss.heptapod.net/pypy/pypy/-/blob/release-pypy3.7-v7.3.7/pypy/tool/release/package.py

Checksums
---------
Checksums for the downloads are :doc:`here <checksums>`

