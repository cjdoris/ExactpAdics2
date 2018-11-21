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

### [v0.4.0](https://github.com/cjdoris/ExactpAdics2/releases/tag/v0.4.0)

```
+ Adds `Generator(E,F)` and `DefiningPolynomial(E,F)` for an extension `E/F`.
+ Adds `HasRoot(f)` and `IsIrreducible(f)` for univariate polynomial `f`.
! `RamificationFiltration` now more robust.
! Fixes bugs in `IsCoercible` and univariate factorization.
```

### [v0.3.0](https://github.com/cjdoris/ExactpAdics2/releases/tag/v0.3.0)

```
~ Now licensed under GPL.
~ Homomorphism constructors have been reimplemented.
+ Adds representations for vector spaces, vectors and matrices over p-adic fields.
+ Adds `DiscriminantValuation`, `VectorSpace`, `StandardForm` and `OptimizedRepresentation` for field extensions.
+ Adds `SplittingField`.
! Fixes bugs in `IsCoercible`.
```

### [v0.2.0](https://github.com/cjdoris/ExactpAdics2/releases/tag/v0.2.0)
```
~ `RamificationFiltration` now uses linear algebra instead of factorization, which is faster.
~ `BringToEpoch` is reimplemented more simply, and is faster.
+ Adds `CanBringToEpoch`, `UninitializedCopy`, `WithDependencies`, `NumberOfNames`
+ Adds `DefiningPolynomial` for extensions (but only implemented for single-hop extensions)
+ Adds `Safe` parameters to functions which need them to make them safe for `WithDependencies` with the `Fast` option.
```

### [v0.1.0](https://github.com/cjdoris/ExactpAdics2/releases/tag/v0.1.0)
```
Initial release
```

## Developer notes

### Common code

This and the original `ExactpAdics` share some common code from [the `ExactpAdicsCommon` repository](https://github.com/cjdoris/ExactpAdicsCommon). The code there should be periodically copied into the `common` directory (no fancy git merging currently).

### Documentation

Documentation is generated using [magdoc](https://cjdoris.github.io/magdoc) with the following command:

```
magdoc.py -o docs FldPad.mag Ramification.mag HomFldPadExact.mag RngUPol.mag Factorization_new.mag common/Factorization_new.mag RngMPol.mag ModTupFld.mag ModMatFld.mag SetCart.mag ValFldPad.mag ValRngUPol.mag Generics.mag Version.mag State.mag DefaultAssociativeArray.mag Promotion.mag
```

We don't currently document the `Utils.mag`.

### Potential improvements
- Precision strategies? The original `ExactpAdics` package had precision strategies, which essentially gave a list of precisions to try computations at. In this package, we currently always try epochs 1, 2, 3, ... forever. We could provide a means to specify the epochs to try, or even specific precisions to try. This could be passed in as a `Strategy` parameter (as in `ExactpAdics`) but this has the disadvantage that one has to be careful that this is propagated out. Or it could be attached as a `precision_strategy` attribute of a p-adic object.

## License

Copyright (C) 2018 Christopher Doris

ExactpAdics2 is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

ExactpAdics2 is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with ExactpAdics2.  If not, see http://www.gnu.org/licenses/.
