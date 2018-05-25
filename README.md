# ExactpAdics2

Another [Magma](http://magma.maths.usyd.edu.au/magma) package for exact p-adic computation. See [the user manual](https://cjdoris.github.io/ExactpAdics2).

It differs from [the first implementation (`ExactpAdics`)](https://github.com/cjdoris/ExactpAdics) in that we do not track precision dependencies backwards. Instead, we "push" them forwards: if a computation is not to enough precision, we increase the precision of all of its inputs by some large jump and recompute. This has the benefits of making it much easier to code the internals, and the dependency tracking is vastly simpler. A potential downside is that some computations may be done to too much precision. In practice, this implementation is usually quicker.

**Contents**
- [Changelog](#changelog)
- [Developer notes](#developer-notes)

## Changelog

```
! Bug fix (no change to user interface, increment patch version)
~ Improvement (no change to user interface, increment patch version)
+ New feature (backwards-compatible change to user interface, increment minor version)
- Remove (backwards-incompatible change to user interface, increment major version)
```

### Pending release

### v0.2.0
```
~ `RamificationFiltration` now uses linear algebra instead of factorization, which is faster.
~ `BringToEpoch` is reimplemented more simply, and is faster.
+ Adds `CanBringToEpoch`, `UninitializedCopy`, `WithDependencies`, `NumberOfNames`
+ Adds `DefiningPolynomial` for extensions (but only implemented for single-hop extensions)
+ Adds `Safe` parameters to functions which need them to make them safe for `WithDependencies` with the `Fast` option.
```

### v0.1.0
```
Initial release
```

## Developer notes

### Common code

This and the original `ExactpAdics` share some common code from [the `ExactpAdicsCommon` repository](https://github.com/cjdoris/ExactpAdicsCommon). The code there should be periodically copied into the `common` directory (no fancy git merging currently).

### Documentation

Documentation is generated using [magdoc](https://cjdoris.github.io/magdoc) with the following command:

```
magdoc.py -o docs FldPad.mag Ramification.mag HomFldPadExact.mag RngUPol.mag Factorization_new.mag common/Factorization_new.mag RngMPol.mag SetCart.mag ValFldPad.mag ValRngUPol.mag Generics.mag Version.mag State.mag DefaultAssociativeArray.mag Promotion.mag
```

### Potential improvements
- If an output `z` is created from some inputs `x` and `y` say, but not directly so that there are some intermediate variables, then we could provide an intrinsic to make `z` depend directly on `x` and `y`. Such an intrinsic would essentially precompute the tree of dependencies of `z` as far as `x` and `y`, so that computing an approximation of `z` amounts to running through these dependencies in order. Hence this will save the work to compute the dependencies of `z` each time it is updated.
- In the preceding idea, the intermediate variables still exist, and are essentially cached inside `z`. We could provide a stricter intrinsic which forgets the actual dependency variables, and only remembers crucial information such as their `get_approximation` function. Then the `get_approximation` function for `z` simply runs through the dependencies and computes their approximations, without any checking or chacheing which usually occurs. This could save time and memory.
- Precision strategies? The original `ExactpAdics` package had precision strategies, which essentially gave a list of precisions to try computations at. In this package, we currently always try epochs 1, 2, 3, ... forever. We could provide a means to specify the epochs to try, or even specific precisions to try. This could be passed in as a `Strategy` parameter (as in `ExactpAdics`) but this has the disadvantage that one has to be careful that this is propagated out. Or it could be attached as a `precision_strategy` attribute of a p-adic object.
