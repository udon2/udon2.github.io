---
layout: page
title: Quickstart
permalink: /quickstart/
nav_order: 2
---

## Installation
### UDon2 from PyPi
Pre-compiled version of UDon2 is available to be installed via pip (see the command below) for the following platforms:
- all Linux distributions (32 and 64 bit) for Python 3.6 - 3.9
- Windows (32 and 64 bit) for Python 3.7 - 3.8

```
pip install udon2
```

MacOS is currently not supported.

### UDon2 from sources
Pre-compiled version of UDon2 is pretty quick, but it could be made even faster by compiling from sources for your own machine specifically. You might also try to compile it on MacOS, but this was not tested, so do it at your own risk.
#### Prerequisites
- C++ compiler (gcc, g++ for Unix systems or msvc for Windows)
- Boost.Python (tested for 1.71+)
    - Ubuntu: `sudo apt-get install libboost-python-dev`
    - Other Linux distributions: take the name of the package [here](https://pkgs.org/search/?q=boost-python) and install it using your favourite package manager **OR** [compile from sources](https://www.boost.org/doc/libs/1_74_0/libs/python/doc/html/building/installing_boost_python_on_your_.html)
    - Windows: download and install a pre-built binary from [here](https://sourceforge.net/projects/boost/files/boost-binaries/) **OR** [compile from sources](https://www.boost.org/doc/libs/1_74_0/libs/python/doc/html/building/installing_boost_python_on_your_.html)

#### Compile & install
1. Specify the environmental variable `BOOST_DIR` wit a directory of your Boost installation (for Linux the directory should contain `include` and `lib` folders, for Windows - `lib<arch>-msvc-*` and `boost` folders, where `<arch>` is your platform architecture).
1. `python setup.py bdist_wheel`
2. `pip install dist/udon2-<version>-<system_details>.whl --user`
