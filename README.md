Percona TokuBackup
======

Percona TokuBackup is a C library that allows users to make consistent
copies of a directory of files, even while the respective files are
being edited, removed, added, and/or renamed.

This repository contains the library and associated unit and
integration tests.

Building
--------

This library requires cmake 2.8.8 or greater to create a build
environment on your target machine.  To create this environment, from
the top of the repository:

```
cd backup
mkdir build-valgrind
cd build-valgrind
CXX=g++ cmake -D CMAKE_BUILD_TYPE=Debug -D USE_VALGRIND=ON ..
```

To build you then simply have to type:

make

Testing
--------

To run a combined suite of unit tests and integration tests, run the
following command after building:

ctest

This will show the progress of the tests and run valgrind memory and
thread checks for each test.


Testing with the address sanitizer
---------------------------------

```
cd backup
mkdir build-address
cd build-address
CXX=clang++ CXXFLAGS="-fsanitize=address" cmake -D CMAKE_BUILD_TYPE=Debug -D USE_VALGRIND=OFF ..
make
ctest
```

Testing with the thread sanitizer
---------------------------------

```
cd backup
mkdir build-thread
cd build-thread
CXX=clang++ CXXFLAGS="-fsanitize=thread" cmake -D CMAKE_BUILD_TYPE=Debug -D USE_VALGRIND=OFF ..
make
TSAN_OPTIONS=suppressions=../tsan.suppressions ctest
```
