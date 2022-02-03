---
layout: page
title: Benchmarks
permalink: /benchmarks/
nav_order: 6
---

# Comparison to other available Python packages
We have benchmarked our code on [cs-ud-train-l.conllu](https://github.com/UniversalDependencies/UD_Czech-PDT/raw/r1.2/cs-ud-train-l.conllu) from UDv1.2 (68 MiB, 41k sentences, 800k words) and compared it with the other available libraries providing a Python API. All benchmarks were run 30 times on Ubuntu 20.04 (64-bit Python) and Windows 10 (32-bit Python) installed on the machine equipped with Intel(R) Core(TM) i7-8750H CPU @ 2.20GHz. 

| Package     | OS          | Memory, MiB | Load, s             | Save, s            | Read, s            | Write, s            | Text, s            | Relchain, s        |
| ----------- | ----------- | ----------- | ------------------- | ------------------ | ------------------ | ------------------- | ------------------ | ------------------ |
| pyconll     | Ubuntu      | 1683.1      | 12.88 &plusmn; 1.07 | 6.32 &plusmn; 0.25 | 0.34 &plusmn; 0.02 | 0.23 &plusmn; 0.01  | NA                 | 0.47 &plusmn; 0.02 |
|             | Windows     | 876.4       | 10.97 &plusmn; 0.63 | 6.23 &plusmn; 0.11 | 0.38 &plusmn; 0.03 | 0.23 &plusmn; 0.02  | NA                 | 0.54 &plusmn; 0.04 |
| ----------- | ----------- | ----------- | ------------------- | ------------------ | ------------------ | ------------------- | ------------------ | ------------------ |
| conllu      | Ubuntu      | 1208.7      | 16.83 &plusmn; 0.3  | 4.28 &plusmn; 0.06 | 0.19 &plusmn; 0.0  | 0.1 &plusmn; 0.0    | NA                 | 0.25 &plusmn; 0.02 |
|             | Windows     | 707.2       | 19.11 &plusmn; 3.32 | 5.23 &plusmn; 1.1  | 0.22 &plusmn; 0.04 | 0.09 &plusmn; 0.01  | NA                 | 0.3 &plusmn; 0.06  |
| ----------- | ----------- | ----------- | ------------------- | ------------------ | ------------------ | ------------------- | ------------------ | ------------------ |
| Udapi-Python| Ubuntu      | 756.0       | 19.88 &plusmn; 1.05 | 6.86 &plusmn; 0.12 | 0.19 &plusmn; 0.01 | 0.14 &plusmn; 0.01  | 0.94 &plusmn; 0.03 | 0.16 &plusmn; 0.01 |
|             | Windows     | 421.6       | 19.09 &plusmn; 1.08 | 8.51 &plusmn; 1.36 | 0.2 &plusmn; 0.02  | 0.11 &plusmn; 0.01  | 1.01 &plusmn; 0.1  | 0.15 &plusmn; 0.01 |
| ----------- | ----------- | ----------- | ------------------- | ------------------ | ------------------ | ------------------- | ------------------ | ------------------ |
| UDon2       | Ubuntu      | 772.0       | 3.27 &plusmn; 0.07  | 3.34 &plusmn; 0.03 | 0.75 &plusmn; 0.0  | 0.42 &plusmn; 0.0   | 0.24 &plusmn; 0.0  | 0.14 &plusmn; 0.0  |
|             | Windows     | 439.7       | 4.44 &plusmn; 0.32  | 5.53 &plusmn; 0.64 | 0.83 &plusmn; 0.07 | 0.42 &plusmn; 0.04  | 0.41 &plusmn; 0.34 | 0.15 &plusmn; 0.01 |


More detailed descriptions of each benchmark:
- **Load** refers to loading from CoNLL-U file;
- **Save** - to storing to the CoNLL-U file;
- **Read** - getting a form and a lemma for every node of every tree;
- **Write** - changing a deprel for every node of every tree;
- **Text** - computing a textual representation of a subtree induced by every root node of every tree;
- **Relchain** - finding nodes at the end of a relchain for every tree.

For more details, please refer to the benchmark code available [here](https://github.com/udon2/udon2/tree/master/benchmarks).

Important
{: .label .label-red .mb-0 .ml-0 .mt-5}

UDon2 performs worse on **Read** and **Write** benchmarks due to them using Python's for-loops with C++ objects. This is known to result in slow performance (e.g. also in Numpy), which is why it is recommended to use the pre-defined methods for querying. Optimizing these benchmarks is currently work in progress.


Note
{: .label .label-blue .mb-0 .ml-0 .mt-5}

UDon2 compiled for a specific Linux machine performs significantly better than the one available via PyPi, since the wheel for PyPi was created with `manylinux2010` tag (to ensure compatibility with many Linux distributions). So if you need performance boost on a Linux, machine-specific compilation will most probably solve your problems. To give an idea of the kind of performance boost, we present results of the same benchmarks on the same machine, but with a machine-specific version of UDon2.

| Package     | OS          | Memory, MiB | Load, s             | Save, s            | Read, s            | Write, s            | Text, s            | Relchain, s        |
| ----------- | ----------- | ----------- | ------------------- | ------------------ | ------------------ | ------------------- | ------------------ | ------------------ |
| UDon2*       | Ubuntu      | 549.9       | 1.79 &plusmn; 0.11  | 2.42 &plusmn; 0.12 | 0.75 &plusmn; 0.03  | 0.36 &plusmn; 0.02   | 0.2 &plusmn; 0.01  | 0.1 &plusmn; 0.0  |

**Observe**, that machine-specific compilation for Windows will not give any performance benefits, since wheels were built with regular `win32` and `win_amd64` tags.
