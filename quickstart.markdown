---
layout: page
title: Quickstart
permalink: /quickstart/
nav_order: 2
---

## Installation
### UDon2 from PyPi [currently work in progress]
UDon2 is pre-compiled for Python 3.6+ and available for all Linux distributions and Windows (32 and 64 bit) using pip (see the command below). Mac OS is currently not supported. 
```
pip install udon2
```

### UDon2 from sources
Pre-compiled version of UDon2 is pretty quick, but it could be made even faster by compiling from sources for your own machine specifically. This requires first to install all prerequisites.
#### Prerequisites
- C++ compiler (gcc, g++ for Unix systems or msvc for Windows)
- Boost.Python (tested for 1.71.0+)
    - Ubuntu: `sudo apt-get install libboost-python-dev`
    - Other Linux distributions: take the name of the package [here](https://pkgs.org/search/?q=boost-python) and install it using your favourite package manager **OR** [compile from sources](https://www.boost.org/doc/libs/1_74_0/libs/python/doc/html/building/installing_boost_python_on_your_.html)
    - Windows: download and install a pre-built binary from [here](https://sourceforge.net/projects/boost/files/boost-binaries/) **OR** [compile from sources](https://www.boost.org/doc/libs/1_74_0/libs/python/doc/html/building/installing_boost_python_on_your_.html)

#### Compile & install
1. `python setup.py bdist_wheel`
2. `pip install dist/udon2-<version>-<system_details>.whl`
