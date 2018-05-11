---
---

# Overview

Magma's built-in types for p-adic computation (`FldPad`, `RngPad`, `RngPadRes`, etc) are all *approximate* in the sense that their elements are computed immediately to some precision, and therefore an element really corresponds to an equivalence class of genuine p-adic elements.

In this package, we provide a new representation of p-adics which is *exact* in the sense that a p-adic number is represented to infinite precision. This is achieved by having the representation be *lazy* in the sense that in addition to each element being represented by a finite-precision approximation, it carries around a function which allows it to update its approximation arbitrarily high.

Advantages of this approach are:

* The user is freed from the burden of choosing a precision at the beginning of a computation; often this precision will be insufficient and the user must increase it manually until no precision errors occur.
* All computations are performed to the minimal precision necessary to compute an output, sometimes giving a gain in speed.

Disadvantages are:

* Dependency tracking overhead: Elements now depend on each other, and tracking these dependencies can be computationally expensive.
* Memory overhead: Every (exact) intermediate value in a computation which the answer depends on will be kept in memory, so more memory is required.

Therefore the main use-cases of this package are:

* Performing computations interactively in Magma; the overheads will be unnoticed.
* Implementing high-level algorithms in Magma; that is, ones where the main operations are themselves expensive enough that the overheads are comparatively small.

