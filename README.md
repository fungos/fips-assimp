fips-assimp
=========

[![Build Status](https://travis-ci.org/fungos/fips-assimp.svg?branch=travis-ci)](https://travis-ci.org/fungos/fips-assimp)

fipsified assimp (https://github.com/assimp/assimp)

fips build system: https://github.com/floooh/fips

To use assimp you need just to add it to your `fips.yml`:

```cmake
imports:
     fips-assimp:
         git: https://github.com/fungos/fips-assimp.git
```

And them add a dependency to your project using `fips_deps(assimp)`.
