# PkgSkeleton.jl

![Lifecycle](https://img.shields.io/badge/lifecycle-experimental-orange.svg)<!--
![Lifecycle](https://img.shields.io/badge/lifecycle-maturing-blue.svg)
![Lifecycle](https://img.shields.io/badge/lifecycle-stable-green.svg)
![Lifecycle](https://img.shields.io/badge/lifecycle-retired-orange.svg)
![Lifecycle](https://img.shields.io/badge/lifecycle-archived-red.svg)
![Lifecycle](https://img.shields.io/badge/lifecycle-dormant-blue.svg) -->
[![Build Status](https://travis-ci.com/tpapp/PkgSkeleton.jl.svg?branch=master)](https://travis-ci.com/tpapp/PkgSkeleton.jl)
[![codecov.io](http://codecov.io/github/tpapp/PkgSkeleton.jl/coverage.svg?branch=master)](http://codecov.io/github/tpapp/PkgSkeleton.jl?branch=master)

Julia package for creating new packages quickly. This is the successor of [skeleton.jl](https://github.com/tpapp/skeleton.jl).

## Installation

This is a clone of registered package
[PkgSkeleton.jl](github.com/tpapp/PkgSkeleton.jl). In order to install this
specific variant (and the template which goes with it), please run

```julia
pkg> add https://github.com/triscale-innov/PkgSkeleton.jl
```

Here is a list of the few modifications that this version brings, which are not
(yet?) in the official, registered package:

- fix a small issue with test cases  (see
  [PR#10](https://github.com/tpapp/PkgSkeleton.jl/pull/10))
- automatically instantiate the `docs/` sub-project during project generation  (see
  [PR#11](https://github.com/tpapp/PkgSkeleton.jl/pull/11))
- interactive way to validate and provide package parameters in case default
  ones (coming from `git config`) are missing (see
  [PR#12](https://github.com/tpapp/PkgSkeleton.jl/pull/12))
- default template sets [Retest](https://github.com/triscale-innov/Retest.jl) up

## Usage

```julia
import PkgSkeleton
PkgSkeleton.generate("destination/directory") # uses default template
```

Then

1. files in template will be copied recursively, with various substitutions (as described below).

2. A git repo is initialized.

If the destination directory exists, the script aborts.

After this, you probably want to `pkg> dev destination/directory` in Julia, and add your Github repository as a remote.

See `?PkgSkeleton.generate` for details.

### “Updating” existing packages

Best practices and recommended setups change with time. The recommended workflow for updating *existing* packages using templates from this package is the following.

1. Make sure that this package is of the latest version, eg with `pkg> up`.

2. Make sure that *everything* is committed in version control. This is very important: when files are overwritten, work may be lost.

3. Run either
    ```julia
    PkgSkeleton.generate("/path/to/pkg"; skip_existing_dir = false)
    ```
    or
    ```julia
    PkgSkeleton.generate("/path/to/pkg"; skip_existing_dir = false, skip_existing_files = true)
    ```
    Only the second one will update existing files.

4. Use your favorite git interface for reviewing the change. Pick and commit what you like, reset the rest.

## Prerequisites

For the default template, you need to set the `git` configuration variables `user.name`, `user.email`, and `github.user`.

## Substitutions

Design follows [KISS](https://en.wikipedia.org/wiki/KISS_principle): do nothing more than substitute strings into templates. For me, this covers 99% of the use cases; the rest I edit manually.

Templates replace the following in files *and filenames*:

| string        | replacement                             |
|---------------|-----------------------------------------|
| `{PKGNAME}`   | name of the package                     |
| `{UUID}`      | an UUID (METADATA-compatible or random) |
| `{GHUSER}`    | `git config --get github.user`          |
| `{USERNAME}`  | `git config --get user.name`            |
| `{USEREMAIL}` | `git config --get user.email`           |
| `{YEAR}`      | the current year                        |
