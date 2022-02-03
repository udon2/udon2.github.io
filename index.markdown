---
layout: home
title: Overview
nav_order: 1
---

# UDon2 - A Package for Manipulating Universal Dependencies Trees
UDon2 provides the possibility to manipulate Universal Dependencies trees. Written in C++ with Python bindings via Boost.Python, UDon2 combines efficiency and flexibility in one package.

UDon2 is geared towards downstream NLP applications and thus makes the following sacrifices of generality in favor of efficiency:
- not reading and storing comments in CoNLL-U files, as those are typically not provided by existing dependency parsers;
- not supporting UDs [enhanced syntax](https://universaldependencies.org/u/overview/enhanced-syntax.html) (for the same reason as the previous point);
- not supporting CoNLL-U Plus format.

In exchange UDon2 offers:
- an efficient Python package (see [benchmarks](/benchmarks)) requiring [minimal efforts to setup](/quickstart);
- advanced operations on dependency trees, such as various transformations or computing convolution tree kernels;
- a visualization module capable of producing SVG and PDF files;
- a possibility to be used as a C++ library;
- a user-friendly and well-documented API.



