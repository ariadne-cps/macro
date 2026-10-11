# Ariadne Macro

[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

Ariadne Macro is a header-only support module for Ariadne projects.

It owns the two public headers formerly provided directly by Ariadne Utility:

- `macro/general.hpp`
- `macro/test.hpp`

Downstream projects include these headers as `macro/general.hpp` and `macro/test.hpp`.

## Configure and install

Clone the repository together with its Git submodules:

```bash
git clone --recurse-submodules https://github.com/ariadne-cps/macro.git
cd macro
cmake -S . -B build
cmake --install build --prefix <prefix>
```

There are no compiled sources, tests, or coverage targets in this repository.
