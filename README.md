libcuckoo
=========

libcuckoo provides a high-performance, compact hash table that allows
multiple concurrent reader and writer threads.

The Doxygen-generated documentation is available at the
[project page](http://efficient.github.io/libcuckoo/).

Authors: Manu Goyal, Bin Fan, Xiaozhou Li, David G. Andersen, and Michael Kaminsky

For details about this algorithm and citations, please refer to
[our paper in NSDI 2013][1]. Some of the details of the hashing
algorithm have been improved since that work (e.g., the previous algorithm
in [1] serializes all writer threads, while our current
implementation supports multiple concurrent writers), however, and this source
code is now the definitive reference.

   [1]: http://www.cs.cmu.edu/~dga/papers/memc3-nsdi2013.pdf "MemC3: Compact and Concurrent Memcache with Dumber Caching and Smarter Hashing"

Requirements
================

This library has been tested on Mac OSX >= 10.8 and Ubuntu >= 12.04.

It compiles with clang++ >= 3.1 and g++ >= 4.6.3, however we strongly
suggest using the latest versions of both compilers, as they have
greatly improved support for atomic operations. Building the library
requires the autotools.

Building
==========

    $ autoreconf -fis
    $ ./configure
    $ make
    $ make install

Usage
==========

To build a program with the hash table, include
``libcuckoo/cuckoohash_map.hh`` into your source file. If you want to
use CityHash, which we recommend, we have provided a wrapper
compatible with the ``std::hash`` type around it in the
``libcuckoo/city_hasher.hh`` file. If compiling with CityHash, add the
``-lcityhash`` flag. You must also enable C++11 features on your
compiler. Compiling the file ``examples/count_freq.cpp`` with g++
might look like this:

    $ g++ -std=c++11 examples/count_freq.cpp -lcityhash

The
[examples directory](https://github.com/efficient/libcuckoo/tree/master/examples)
contains some simple demonstrations of some of the basic features of
the hash table.

**Note**: While the STL supports ``operator[]`` for accessing keys in
  the map, we instead have a ``cuckoohash_map::find`` method, which
  resembles the ``unordered_map::at`` method. Consult
  [the documentation](http://efficient.github.io/libcuckoo/classcuckoohash__map.html#addc0721a99193e0af53b34e2170fd6b5)
  for more information.

Tests
==========

The
[tests directory](https://github.com/efficient/libcuckoo/tree/master/tests)
directory contains a number of tests and benchmarks of the hash table,
which also serve as useful examples of how to use the table's various
features. The entire test suite can be run with the ``make check``
command, and the test executables, which have the suffix ``.out``, can
be run individually as well.

Issue Report
============

To let us know your questions or issues, we recommend you
[report an issue](https://github.com/efficient/libcuckoo/issues) on
github. You can also email us at
[libcuckoo-dev@googlegroups.com](mailto:libcuckoo-dev@googlegroups.com).

Licence
===========
Copyright (C) 2013, Carnegie Mellon University and Intel Corporation

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

     http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

---------------------------

CityHash (lib/city.h, lib/city.cc) is Copyright (c) Google, Inc. and
has its own license, as detailed in the source files.
