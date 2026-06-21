# tree-sitter-dart

[![PyPI](https://img.shields.io/pypi/v/tree-sitter-dart.svg)](https://pypi.org/project/tree-sitter-dart/)
[![Python versions](https://img.shields.io/pypi/pyversions/tree-sitter-dart.svg)](https://pypi.org/project/tree-sitter-dart/)
[![CI](https://github.com/efrenbl/tree-sitter-dart/actions/workflows/ci.yaml/badge.svg)](https://github.com/efrenbl/tree-sitter-dart/actions/workflows/ci.yaml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A [tree-sitter](https://tree-sitter.github.io/) grammar for the Dart programming
language — which also covers **Flutter** (Flutter widgets are ordinary Dart
classes; there is no separate Flutter syntax).

This is a fork of [UserNobody14/tree-sitter-dart](https://github.com/UserNobody14/tree-sitter-dart)
(MIT) packaged and published as a **Python distribution with pre-compiled
wheels** (Linux/macOS/Windows), since no `tree-sitter-dart` existed on PyPI
compatible with `tree-sitter>=0.23`.

## Python usage

```bash
pip install tree-sitter-dart  # ships pre-compiled wheels; no C compiler needed
```

```python
import tree_sitter_dart
from tree_sitter import Language, Parser

parser = Parser(Language(tree_sitter_dart.language()))
tree = parser.parse(b"class MyWidget extends StatelessWidget { Widget build(c) {} }")
print(tree.root_node.type)  # -> program
```

`language()` returns a `tree_sitter.Language` PyCapsule, the standard
py-tree-sitter interface. Wheels are abi3 (CPython 3.8+).

## Grammar development (Node / tree-sitter CLI)

This is a tree-sitter grammar written for the dart programming language. We attempt to adhere as closely as possible to the dart language spec. Initially it was started with a copy of the tree-sitter Java grammar which is why there may be a few relics included in here. For the sake of simplifying the syntax tree, many items were made inlined with tree-sitter's "underscore" method of writing rules.

### Getting started
- Go to the project directory
- run `npm install` (first time)
- run `npm run build_init` (first time) `npm run build` (subsequent times)
- run `npm run test`

### To test a single highlight file
- run `tree-sitter highlight test/highlight/types.dart`

### To test a single test file
- run `tree-sitter test -f 'testcasefilter'`
- for example `tree-sitter test -f 'dart string literals'`

### To show the output of a parse for a sample file (for example while debugging highlight issues)
- run `tree-sitter parse path/to/file.dart`

## Credits

Grammar by [UserNobody14](https://github.com/UserNobody14/tree-sitter-dart) and
contributors (MIT). This fork adds Python packaging, a modernized PyCapsule
binding, and pre-compiled wheels.