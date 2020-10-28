Talisman Core staging tree 0.12
===============================

`master:` [![Build Status](https://travis-ci.org/talisman-coin/talisman.svg?branch=master)](https://travis-ci.org/talisman-coin/talisman) `v0.12.0.x:` [![Build Status](https://travis-ci.org/talisman-coin/talisman.svg?branch=v0.12.0.x)](https://travis-ci.org/talisman-coin/talisman/branches) `v0.12.1.x:` [![Build Status](https://travis-ci.org/talisman-coin/talisman.svg?branch=v0.12.1.x)](https://travis-ci.org/talisman-coin/talisman/branches)

https://www.talisman.org

Copyright (c) 2009-2015 Bitcoin Core Developers

Copyright (c) 2014-2015 Talisman Core Developers


What is Talisman?
----------------

Talisman is an experimental new digital currency that enables anonymous, instant
payments to anyone, anywhere in the world. Talisman uses peer-to-peer technology
to operate with no central authority: managing transactions and issuing money
are carried out collectively by the network. Talisman Core is the name of open
source software which enables the use of this currency.

For more information, as well as an immediately useable, binary version of
the Talisman Core software, see https://www.talisman.org/downloads.


License
-------

Talisman Core is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see http://opensource.org/licenses/MIT.

Development Process
-------------------

The `master` branch is meant to be stable. Development is normally done in separate branches.
[Tags](https://github.com/talisman-coin/talisman/tags) are created to indicate new official,
stable release versions of Talisman Core.

The contribution workflow is described in [CONTRIBUTING.md](CONTRIBUTING.md).


Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write unit tests for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run (assuming they weren't disabled in configure) with: `make check`

Every pull request is built for both Windows and Linux on a dedicated server,
and unit and sanity tests are automatically run. The binaries produced may be
used for manual QA testing — a link to them will appear in a comment on the
pull request posted by [TalismanPullTester](https://github.com/talisman-coin/PullTester). See https://github.com/TheBlueMatt/test-scripts
for the build/test scripts. ***TODO***

### Manual Quality Assurance (QA) Testing

Large changes should have a test plan, and should be tested by somebody other
than the developer who wrote the code.
See https://github.com/talisman-coin/QA/ for how to create a test plan. ***TODO***

Translations
------------

Changes to translations as well as new translations can be submitted to
[Bitcoin Core's Transifex page](https://www.transifex.com/projects/p/talisman/).

Translations are periodically pulled from Transifex and merged into the git repository. See the
[translation process](doc/translation_process.md) for details on how this works.

**Important**: We do not accept translation changes as GitHub pull requests because the next
pull from Transifex would automatically overwrite them again.

Translators should also subscribe to the [mailing list](https://groups.google.com/forum/#!forum/talisman-translators). ***TODO***

Development tips and tricks
---------------------------

**compiling for debugging**

Run configure with the --enable-debug option, then make. Or run configure with
CXXFLAGS="-g -ggdb -O0" or whatever debug flags you need.

**debug.log**

If the code is behaving strangely, take a look in the debug.log file in the data directory;
error and debugging messages are written there.

The -debug=... command-line option controls debugging; running with just -debug will turn
on all categories (and give you a very large debug.log file).

The Qt code routes qDebug() output to debug.log under category "qt": run with -debug=qt
to see it.

**testnet and regtest modes**

Run with the -testnet option to run with "play talisman" on the test network, if you
are testing multi-machine code that needs to operate across the internet.

If you are testing something that can run on one machine, run with the -regtest option.
In regression test mode, blocks can be created on-demand; see qa/rpc-tests/ for tests
that run in -regtest mode.

**DEBUG_LOCKORDER**

Talisman Core is a multithreaded application, and deadlocks or other multithreading bugs
can be very difficult to track down. Compiling with -DDEBUG_LOCKORDER (configure
CXXFLAGS="-DDEBUG_LOCKORDER -g") inserts run-time checks to keep track of which locks
are held, and adds warnings to the debug.log file if inconsistencies are detected.
