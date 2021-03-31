# compile-documentation-for-packages

This GitHub action runs compiles the manual of a GAP package.

## Usage

The action `compile-documentation-for-packages` has to be called by the workflow of a GAP
package `gap-package`.
By default it compiles the manual of a GAP package.

Its behaviour can be customized via the inputs below.

### Inputs

All of the following inputs are optional.

- use-latex:
  - if `true`, then install and use latex
  - default: `false`
- use-makedoc-shell-script:
  - if true, call `doc/make_doc` instead of `makedoc.g`
  - default: `false`

### Examples

See below for
- a minimal example to run this action, and
- an example how to compile the manual into a pdf and upload it as an
  artifact

#### Minimal example
```yaml
name: CI

# Trigger the workflow on push or pull request
on:
  push:
    branches:
      - master # change this to 'main' if necessary!
  pull_request:

jobs:
  # The documentation job
  manual:
    name: Build manuals
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - uses: gap-actions/setup-gap-for-packages@v1
      - uses: gap-actions/compile-documentation-for-packages@v1
```

#### Uploading the manual as an artifact
```yaml
name: CI

# Trigger the workflow on push or pull request
on:
  push:
    branches:
      - master # change this to 'main' if necessary!
  pull_request:

jobs:
  # The documentation job
  manual:
    name: Build manuals
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - uses: gap-actions/setup-gap-for-packages@v1
      - uses: gap-actions/compile-documentation-for-packages@v1
        with:
          use-latex: 'true'
      - name: 'Upload documentation'
        uses: actions/upload-artifact@v1
        with:
          name: manual
          path: ./doc/manual.pdf
```

## Contact
Please submit bug reports, suggestions for improvements and patches via
the [issue tracker](https://github.com/gap-actions/compile-documentation-for-packages/issues)
or via email to
[Sergio Siccha](mailto:siccha@mathematik.uni-kl.de).

## License
The action `compile-documentation-for-packages` is free software; you can redistribute
and/or modify it under the terms of the GNU General Public License as published
by the Free Software Foundation; either version 2 of the License, or (at your
opinion) any later version. For details, see the file `LICENSE` distributed
with this action or the FSF's own site.
