# Ariadne Macro

[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

Ariadne Macro is a header-only support module for Ariadne projects.

It owns the two public headers formerly provided directly by Ariadne Utility:

- `utility/macros.hpp`
- `utility/test.hpp`

The `utility/` include path is intentionally preserved so downstream code does not need to change its includes when Utility starts depending on this module.

## Configure and install

Clone the repository together with its Git submodules:

```bash
git clone --recurse-submodules https://github.com/ariadne-cps/macro.git
cd macro
cmake -S . -B build
cmake --install build --prefix <prefix>
```

There are no compiled sources, tests, or coverage targets in this repository.
