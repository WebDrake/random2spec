Draft std.random2 spec
===========

Phobos' std.random module has a number of flaws which cannot readily be fixed
in a backwards-compatible way -- the most glaring being the choice to implement
random number generators as value rather than reference types.

This spec is an attempt to define: (i) a concrete API for std.random's successor,
and (ii) a set of design principles that can be used when developing new
functionality within the module.

## General aims

  1. *Statistical safety.*  The obvious/easy use of random number functionality
     should result in statistically reliable results within the limits of the
     generators used, i.e. no unexpected correlations or repetitions of random
     sequences.  "The right thing to do should be the easy thing to do."

  2. *Quality and efficiency.* Default algorithms should represent the state of
     the art in terms of balancing statistical quality against performance.

  3. *Flexibility.* The module should provide support for the widest variety of
     potential use-cases, from the most rigorous statistical quality requirements
     (e.g. crypto) through quality/speed tradeoffs (e.g. scientific simulation),
     to primarily speed-focused applications (games?).

  4. *Modularity.* With [DIP37](http://wiki.dlang.org/DIP37) approved and
     [merged](https://github.com/D-Programming-Language/dmd/pull/2139), the
     successor to std.random should be implemented as a package, not a single
     module.


## Specific aims

  1. A D-ified (Deified?:-) version of the API defined in the [C++11 standard for
     random number generation](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2011/n3242.pdf)

  2. RNG-based algorithms including random shuffle, random cover and random sample

  3. High-quality thread-safe unpredictable seed


## Broad roadmap

  1. Precise spec for uniform random number generators, RNG adaptors, random number
     distributions, and other features of the package

  2. Re-implement functionality currently available in std.random.

  3. Submit for inclusion in Phobos.

  4. Implement additional functionality defined in specific aims, but not implemented
     in std.random.


## Package modules

The package std.random2 should contain the following submodules:

  * `std.random2.generators` -- random number engines (e.g. Mersenne Twister,
    Linear Congruential), including non-deterministic engines, seed sequence and
    unpredictable seed.

  * `std.random2.adaptors` -- e.g. discard block, independent bits

  * `std.random2.distributions` -- e.g. uniform, normal, exponential, ...

  * `std.random2.algorithms` -- e.g. randomShuffle, randomCover, randomSample

Spec for these modules is contained respectively in the files `generators.md`,
`adaptors.md`, `distributions.md` and `algorithms.md`.
