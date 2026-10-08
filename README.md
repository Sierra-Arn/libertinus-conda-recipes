<!-- 
    ================================================================================================
    
    Copyright (c) 2026 Ilya Snegov

    Permission to use, copy, modify, and/or distribute this software for
    any purpose with or without fee is hereby granted.

    THE SOFTWARE IS PROVIDED “AS IS” AND THE AUTHOR DISCLAIMS ALL
    WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES
    OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE
    FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY
    DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN
    AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT
    OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

    ================================================================================================
    README.md
    ================================================================================================
-->

# Libertinus Conda Recipes

*Conda recipes for the Libertinus font family, plus the pixi configurations to build and install them straight from git.*

## Project Structure

```
conda-recipe-libertinus/
├── otf/                    # Conda recipe for the static OpenType fonts of the
│   │                       # Libertinus family. Installs the `.otf` files into
│   │                       # `share/fonts/otf/` of the target environment.
│   │
│   ├── pixi.toml           # Pixi package manifest declaring the
│   │                       # `pixi-build-rattler-build` backend, so pixi can
│   │                       # build this recipe from a git dependency.
│   │
│   └── recipe.yaml         # Recipe in the v1 format: upstream release
│                           # source with checksum, install script, and
│                           # package metadata.
│
├── ttf/                    # Conda recipe for the static TrueType fonts.
│   │                       # Mirrors `otf/` and installs the `.ttf` files into
│   │                       # `share/fonts/ttf/`.
│   │
│   ├── pixi.toml
│   └── recipe.yaml
│
└── woff2/                  # Conda recipe for the static WOFF2 web fonts.
    │                       # Mirrors `otf/` and installs the `.woff2` files into
    │                       # `share/fonts/woff2/`.
    │
    ├── pixi.toml
    └── recipe.yaml
```

## Installation

<!-- =========================================================================================== -->

### I. Prerequisites

| Component            | Requirement                       |
| :------------------- | :-------------------------------- |
| **Package Manager**  | [`Pixi`](https://pixi.sh/latest/) with `pixi-build` support |
| **Operating System** | Unix-like system [^1]    |
| **Architecture**     | Any                       |
| **Network**          | Internet access to fetch the font archive from the official upstream repository |

[^1]: The build scripts use POSIX shell, so Windows is not supported.

<!-- =========================================================================================== -->

### II. Enable `pixi-build`

Add the `pixi-build` preview feature to the `[workspace]` section of your `pixi.toml`:

```toml
[workspace]
preview = ["pixi-build"]
```

> **Note:**  
> As of Pixi 0.81.0, `pixi-build` is still a preview feature, so it has to be enabled explicitly. Once it is stabilized, this step may become unnecessary and the syntax may change.

<!-- =========================================================================================== -->

### III. Installation

Add the font format you need. Pixi will fetch the recipe from this repository, build the package, and install it into your environment:

```bash
# OpenType
pixi add --git https://github.com/Sierra-Arn/libertinus-conda-recipes --rev <commit> --subdir otf libertinus-otf

# TrueType
pixi add --git https://github.com/Sierra-Arn/libertinus-conda-recipes --rev <commit> --subdir ttf libertinus-ttf

# WOFF2
pixi add --git https://github.com/Sierra-Arn/libertinus-conda-recipes --rev <commit> --subdir woff2 libertinus-woff2
```

The fonts are installed into `$CONDA_PREFIX/share/fonts/<format>/` of the environment.

<!-- =========================================================================================== -->

## License

Every file in this repository is licensed under the [Zero-Clause BSD](LICENSE.txt).

<!-- =========================================================================================== -->
