# Exact p-adic fields
{:#exact-p-adic-fields}


**Contents**
* [Creation of p-adic fields](#creation-of-p-adic-fields)
  * [Prime fields](#prime-fields)
  * [Extensions](#extensions)
  * [Completions](#completions)
  * [From approximate fields](#from-approximate-fields)
* [Creation of p-adic numbers](#creation-of-p-adic-numbers)
  * [Distinguished elements](#distinguished-elements)
  * [From coefficients](#from-coefficients)
  * [Coercion](#coercion)
  * [Random](#random)
* [Basic operations](#basic-operations)
* [Arithmetic](#arithmetic)
* [Valuation](#valuation)
  * [Comparison to constant](#comparison-to-constant)
  * [Comparison between elements](#comparison-between-elements)
  * [Smallest and closest](#smallest-and-closest)
* [Extensions](#extensions-2)
  * [Basic information](#basic-information)
  * [Invariants](#invariants)
  * [Ramification predicates](#ramification-predicates)
  * [Printing](#printing)
  * [Standard form](#standard-form)
* [Residue class field](#residue-class-field)
* [Ramification polynomials and polygons](#ramification-polynomials-and-polygons)
* [Hasse-Herbrand transition function](#hasse-herbrand-transition-function)
  * [Creation](#creation)
  * [Operations](#operations)
* [Homomorphisms](#homomorphisms)
  * [Creation](#creation-2)
  * [Inspection](#inspection)
  * [Application](#application)
  * [Automorphism group](#automorphism-group)
* [Internals](#internals)
  * [Approximations](#approximations)
  * [ExtFldPadExact](#extfldpadexact)

## Creation of p-adic fields
{:#creation-of-p-adic-fields}

### Prime fields
{:#prime-fields}

<a id="ExactpAdicField"></a><a id="ExactpAdicField--RngIntElt"></a>
> **ExactpAdicField** (p :: *RngIntElt*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The `p`-adic field.


### Extensions
{:#extensions}

<a id="ExtConstructor"></a><a id="ExtConstructor--FldPadExact--etc"></a><a id="ExtConstructor--FldPadExact--Tup"></a>
> **ext** \<F :: *FldPadExact* \| ...>
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

Constructs an extension of `F`.

Its arguments must be either:
- A positive integer: constructs an unramified extension of this degree.
- Coercible to a inertial polynomial over `F`: constructs an unramified extension.
- Coercible to an Eisenstein polynomial over `F`: constructs a totally ramified extension.
- Two `FldPad`s, forming an extension `xE/xF`: constructs an extension `E/F` isomorphic to `xE/xF`.


<a id="UnramifiedExtension"></a><a id="UnramifiedExtension--FldPadExact--etc"></a><a id="UnramifiedExtension--FldPadExact--any"></a>
> **UnramifiedExtension** (F :: *FldPadExact*, f)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

An unramified extension of `F` defined by `f`.


<a id="UnramifiedExtension-2"></a><a id="UnramifiedExtension--RngUPolElt_FldPadExact"></a>
> **UnramifiedExtension** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

An unramified extension defined by `f`.


<a id="UnramifiedExtension-3"></a><a id="UnramifiedExtension--FldPadExact--etc-2"></a><a id="UnramifiedExtension--FldPadExact--RngIntElt"></a>
> **UnramifiedExtension** (F :: *FldPadExact*, d :: *RngIntElt*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

An unramified extension of `F` of degree `d`.


<a id="TotallyRamifiedExtension"></a><a id="TotallyRamifiedExtension--FldPadExact--etc"></a><a id="TotallyRamifiedExtension--FldPadExact--any"></a>
> **TotallyRamifiedExtension** (F :: *FldPadExact*, f)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

A totally ramified extension of `F` defined by `f`.


<a id="TotallyRamifiedExtension-2"></a><a id="TotallyRamifiedExtension--RngUPolElt_FldPadExact"></a>
> **TotallyRamifiedExtension** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

A totally ramified extension defined by `f`.


### Completions
{:#completions}

<a id="ExactCompletion"></a><a id="ExactCompletion--FldRat--etc"></a><a id="ExactCompletion--FldRat--any"></a><a id="ExactCompletion--FldNum--etc"></a><a id="ExactCompletion--FldNum--any"></a>
> **ExactCompletion** (F :: *FldRat*, p)
> 
> **ExactCompletion** (F :: *FldNum*, p)
> 
> -> *FldPadExact*, *Map*
> {:.ret}
{:.intrinsic}

The completion of `F` at `p` as an exact `p`-adic field. Also returns the embedding of `F`. The inverse of the embedding takes a `p`-adic number to its best current approximation, and therefore depends on the current precision of the element.




### From approximate fields
{:#from-approximate-fields}

<a id="ExactpAdicField-2"></a><a id="ExactpAdicField--FldPad"></a>
> **ExactpAdicField** (xF :: *FldPad*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

An exact p-adic field isomorphic to `xF`.

**Parameters**
- `CheckUnique := true`: When `true`, checks that the input is precise enough to determine the field up to isomorphism.

<a id="ExactpAdicField-3"></a><a id="ExactpAdicField--FldPad--etc"></a><a id="ExactpAdicField--FldPad--FldPad--FldPadExact"></a>
> **ExactpAdicField** (xE :: *FldPad*, xF :: *FldPad*, F :: *FldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

Given an extension `xE/xF`, such that `xF` is parallel-coercible to and from any approximation field of `F`, returns E such that `E/F` is isomorphic to `xE/xF`. Note that `ext<F | xE, xF>` is shorthand for this.

**Parameters**
- `CheckUnique := true`: When `true`, checks that the input is precise enough to determine the field up to isomorphism.

## Creation of p-adic numbers
{:#creation-of-p-adic-numbers}

### Distinguished elements
{:#distinguished-elements}

<a id="Zero"></a><a id="Zero--FldPadExact"></a><a id="One"></a><a id="One--FldPadExact"></a>
> **Zero** (F :: *FldPadExact*)
> 
> **One** (F :: *FldPadExact*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

Zero and one.




<a id="Generator"></a><a id="Generator--FldPadExact"></a>
> **Generator** (F :: *FldPadExact*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

A generator of `F`.


<a id="UniformizingElement"></a><a id="UniformizingElement--FldPadExact"></a>
> **UniformizingElement** (F :: *FldPadExact*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

A uniformizing element of `F`.


<a id="ResidueGenerator"></a><a id="ResidueGenerator--FldPadExact"></a>
> **ResidueGenerator** (F :: *FldPadExact*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

A residue generator of `F`. That is, an element whose residue class generates the residue class field over its prime subfield.


<a id="AbsoluteGenerator"></a><a id="AbsoluteGenerator--FldPadExact"></a>
> **AbsoluteGenerator** (F :: *FldPadExact*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

A generator of `F` over its prime subfield.

If `F` is absolutely unramified, this will be a residue generator. If absolutely totally ramified, this will be a uniformizing element. Otherwise, it will be the sum of the two.


### From coefficients
{:#from-coefficients}

*Not implemented.*

### Coercion
{:#coercion}


We can coerce the following to an element of `F`:
- An element of `F`
- An integer or rational
- Anything coercible to the base field of `F`
- Anything coercible to a number field that `F` is a completion of

<a id="IsCoercible"></a><a id="IsCoercible--FldPadExact--etc"></a><a id="IsCoercible--FldPadExact--any"></a>
> **IsCoercible** (F :: *FldPadExact*, X)
> 
> -> *BoolElt*, Any
> {:.ret}
{:.intrinsic}

True if `X` is coercible to `F`. If so, also returns the coerced element.


### Random
{:#random}

*Not implemented.*

## Basic operations
{:#basic-operations}

<a id="Prime"></a><a id="Prime--FldPadExact"></a>
> **Prime** (F :: *FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The prime of `F`.


<a id="DefiningPolynomial"></a><a id="DefiningPolynomial--FldPadExact"></a>
> **DefiningPolynomial** (F :: *FldPadExact*)
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The defining polynomial of `F`.


<a id="DefiningPolynomial-2"></a><a id="DefiningPolynomial--FldPadExact--etc"></a><a id="DefiningPolynomial--FldPadExact--FldPadExact"></a>
> **DefiningPolynomial** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

A defining polynomial for `E`/`F`.


<a id="Valuation"></a><a id="Valuation--FldPadExactElt"></a>
> **Valuation** (x :: *FldPadExactElt*)
> 
> -> *ValFldPadExactElt*
> {:.ret}
{:.intrinsic}

The valuation of `x`. If `x` is zero, this will hang.


<a id="IsDefinitelyNonzero"></a><a id="IsDefinitelyNonzero--FldPadExactElt"></a>
> **IsDefinitelyNonzero** (x :: *FldPadExactElt*)
> 
> -> *BoolElt*, *RngIntElt*
> {:.ret}
{:.intrinsic}

True if `x` is nonzero. If so, returns an epoch in which the approximation is nonzero.

**Parameters**
- `Minimize := false`: When `true`, the returned epoch is minimal.

<a id="Eltseq"></a><a id="Eltseq--FldPadExactElt"></a>
> **Eltseq** (x :: *FldPadExactElt*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The coefficients of `x` as a vector over the base field.


## Arithmetic
{:#arithmetic}

<a id="-"></a><a id="---FldPadExactElt"></a><a id="+"></a><a id="+--FldPadExactElt--etc"></a><a id="+--FldPadExactElt--FldPadExactElt"></a><a id="---FldPadExactElt--etc"></a><a id="---FldPadExactElt--FldPadExactElt"></a><a id="*"></a><a id="*--FldPadExactElt--etc"></a><a id="*--FldPadExactElt--FldPadExactElt"></a><a id="/"></a><a id="/--FldPadExactElt--etc"></a><a id="/--FldPadExactElt--FldPadExactElt"></a><a id="^"></a><a id="^--FldPadExactElt--etc"></a><a id="^--FldPadExactElt--RngIntElt"></a><a id="&+"></a><a id="&+--seq-FldPadExactElt"></a><a id="&*"></a><a id="&*--seq-FldPadExactElt"></a>
> **\'-\'** (x :: *FldPadExactElt*)
> 
> **\'+\'** (x :: *FldPadExactElt*, y :: *FldPadExactElt*)
> 
> **\'-\'** (x :: *FldPadExactElt*, y :: *FldPadExactElt*)
> 
> **\'\*\'** (x :: *FldPadExactElt*, y :: *FldPadExactElt*)
> 
> **\'/\'** (x :: *FldPadExactElt*, y :: *FldPadExactElt*)
> 
> **\'^\'** (x :: *FldPadExactElt*, m :: *RngIntElt*)
> 
> **\'&+\'** (xs :: [*FldPadExactElt*])
> 
> **\'&\*\'** (xs :: [*FldPadExactElt*])
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

Negate, add, subtract, multiply, divide, power, sum and product.















**Parameters**
- `Safe := false`: (Division and powering only.) When true, this may be used as an intermediate variable in [`WithDependencies`](internals#WithDependencies) with the `Fast` option.

<a id="ShiftValuation"></a><a id="ShiftValuation--FldPadExactElt--etc"></a><a id="ShiftValuation--FldPadExactElt--RngIntElt"></a>
> **ShiftValuation** (x :: *FldPadExactElt*, m :: *RngIntElt*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

Multiplies `x` by the `m`th power of the uniformizer.


## Valuation
{:#valuation}

### Comparison to constant
{:#comparison-to-constant}

<a id="ValuationEq"></a><a id="ValuationEq--FldPadExactElt--etc"></a><a id="ValuationEq--FldPadExactElt--any"></a><a id="ValuationNe"></a><a id="ValuationNe--FldPadExactElt--etc"></a><a id="ValuationNe--FldPadExactElt--any"></a><a id="ValuationGe"></a><a id="ValuationGe--FldPadExactElt--etc"></a><a id="ValuationGe--FldPadExactElt--any"></a><a id="ValuationGt"></a><a id="ValuationGt--FldPadExactElt--etc"></a><a id="ValuationGt--FldPadExactElt--any"></a><a id="ValuationLe"></a><a id="ValuationLe--FldPadExactElt--etc"></a><a id="ValuationLe--FldPadExactElt--any"></a><a id="ValuationLt"></a><a id="ValuationLt--FldPadExactElt--etc"></a><a id="ValuationLt--FldPadExactElt--any"></a>
> **ValuationEq** (x :: *FldPadExactElt*, v)
> 
> **ValuationNe** (x :: *FldPadExactElt*, v)
> 
> **ValuationGe** (x :: *FldPadExactElt*, v)
> 
> **ValuationGt** (x :: *FldPadExactElt*, v)
> 
> **ValuationLe** (x :: *FldPadExactElt*, v)
> 
> **ValuationLt** (x :: *FldPadExactElt*, v)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

Compares the valuation of `x` with `v`.












<a id="IsUniformizingElement"></a><a id="IsUniformizingElement--FldPadExactElt"></a>
> **IsUniformizingElement** (x :: *FldPadExactElt*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `x` is a uniformizing element; that is, its valuation is 1.


<a id="IsUnit"></a><a id="IsUnit--FldPadExactElt"></a>
> **IsUnit** (x :: *FldPadExactElt*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `x` is a unit; that is, its valuation is 0.


<a id="IsIntegral"></a><a id="IsIntegral--FldPadExactElt"></a>
> **IsIntegral** (x :: *FldPadExactElt*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `x` is an integer; that is, its valuation is at least 0.


### Comparison between elements
{:#comparison-between-elements}

<a id="ValuationEqValuation"></a><a id="ValuationEqValuation--FldPadExactElt--etc"></a><a id="ValuationEqValuation--FldPadExactElt--FldPadExactElt"></a><a id="ValuationNeValuation"></a><a id="ValuationNeValuation--FldPadExactElt--etc"></a><a id="ValuationNeValuation--FldPadExactElt--FldPadExactElt"></a><a id="ValuationGeValuation"></a><a id="ValuationGeValuation--FldPadExactElt--etc"></a><a id="ValuationGeValuation--FldPadExactElt--FldPadExactElt"></a><a id="ValuationGtValuation"></a><a id="ValuationGtValuation--FldPadExactElt--etc"></a><a id="ValuationGtValuation--FldPadExactElt--FldPadExactElt"></a><a id="ValuationLeValuation"></a><a id="ValuationLeValuation--FldPadExactElt--etc"></a><a id="ValuationLeValuation--FldPadExactElt--FldPadExactElt"></a><a id="ValuationLtValuation"></a><a id="ValuationLtValuation--FldPadExactElt--etc"></a><a id="ValuationLtValuation--FldPadExactElt--FldPadExactElt"></a>
> **ValuationEqValuation** (x :: *FldPadExactElt*, y :: *FldPadExactElt*)
> 
> **ValuationNeValuation** (x :: *FldPadExactElt*, y :: *FldPadExactElt*)
> 
> **ValuationGeValuation** (x :: *FldPadExactElt*, y :: *FldPadExactElt*)
> 
> **ValuationGtValuation** (x :: *FldPadExactElt*, y :: *FldPadExactElt*)
> 
> **ValuationLeValuation** (x :: *FldPadExactElt*, y :: *FldPadExactElt*)
> 
> **ValuationLtValuation** (x :: *FldPadExactElt*, y :: *FldPadExactElt*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

Compares the valuation of `x` with the valuation of `y`.












### Smallest and closest
{:#smallest-and-closest}

*Not implemented.*

## Extensions
{:#extensions-2}

### Basic information
{:#basic-information}

<a id="IsPrimeField"></a><a id="IsPrimeField--FldPadExact"></a>
> **IsPrimeField** (F :: *FldPadExact*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `F` is a prime field.


<a id="BaseField"></a><a id="BaseField--FldPadExact"></a>
> **BaseField** (E :: *FldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The base field of `E`, which must be an extension.


<a id="PrimeField"></a><a id="PrimeField--FldPadExact"></a>
> **PrimeField** (E :: *FldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The prime subfield of `E`.


<a id="IsExtensionOf"></a><a id="IsExtensionOf--FldPadExact--etc"></a><a id="IsExtensionOf--FldPadExact--FldPadExact"></a>
> **IsExtensionOf** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *BoolElt*, *ExtFldPadExact*
> {:.ret}
{:.intrinsic}

True if `E` is an extension of `F`. If so, also returns an [object representing the extension](#extfldpadexact).


### Invariants
{:#invariants}

<a id="Degree"></a><a id="Degree--FldPadExact--etc"></a><a id="Degree--FldPadExact--FldPadExact"></a>
> **Degree** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The degree of `E` over `F`.


<a id="InertiaDegree"></a><a id="InertiaDegree--FldPadExact--etc"></a><a id="InertiaDegree--FldPadExact--FldPadExact"></a>
> **InertiaDegree** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The inertia degree of `E` over `F`.


<a id="RamificationDegree"></a><a id="RamificationDegree--FldPadExact--etc"></a><a id="RamificationDegree--FldPadExact--FldPadExact"></a>
> **RamificationDegree** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The ramification degree of `E` over `F`.


<a id="Degree-2"></a><a id="Degree--FldPadExact"></a>
> **Degree** (F :: *FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The degree of `F` over its base field.


<a id="InertiaDegree-2"></a><a id="InertiaDegree--FldPadExact"></a>
> **InertiaDegree** (F :: *FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The inertia degree of `F` over its base field.


<a id="RamificationDegree-2"></a><a id="RamificationDegree--FldPadExact"></a>
> **RamificationDegree** (F :: *FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The ramification degree of `F` over its base field.


<a id="AbsoluteDegree"></a><a id="AbsoluteDegree--FldPadExact"></a>
> **AbsoluteDegree** (F :: *FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The absolute degree of `F`.


<a id="AbsoluteInertiaDegree"></a><a id="AbsoluteInertiaDegree--FldPadExact"></a>
> **AbsoluteInertiaDegree** (F :: *FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The absolute inertia degree of `F`.


<a id="AbsoluteRamificationDegree"></a><a id="AbsoluteRamificationDegree--FldPadExact"></a>
> **AbsoluteRamificationDegree** (F :: *FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The absolute ramification degree of `F`.


### Ramification predicates
{:#ramification-predicates}

<a id="IsUnramified"></a><a id="IsUnramified--FldPadExact"></a><a id="IsUnramified--FldPadExact--etc"></a><a id="IsUnramified--FldPadExact--FldPadExact"></a>
> **IsUnramified** (E :: *FldPadExact*)
> 
> **IsUnramified** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `E` is unramified over `F` or its base field. That is, the ramification degree is 1.




<a id="IsRamified"></a><a id="IsRamified--FldPadExact"></a><a id="IsRamified--FldPadExact--etc"></a><a id="IsRamified--FldPadExact--FldPadExact"></a>
> **IsRamified** (E :: *FldPadExact*)
> 
> **IsRamified** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `E` is ramified over `F` or its base field. That is, the ramification degree is not 1.




<a id="IsTotallyRamified"></a><a id="IsTotallyRamified--FldPadExact"></a><a id="IsTotallyRamified--FldPadExact--etc"></a><a id="IsTotallyRamified--FldPadExact--FldPadExact"></a>
> **IsTotallyRamified** (E :: *FldPadExact*)
> 
> **IsTotallyRamified** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `E` is totally ramified over `F` or its base field. That is, the inertia degree is 1.




<a id="IsTamelyRamified"></a><a id="IsTamelyRamified--FldPadExact"></a><a id="IsTamelyRamified--FldPadExact--etc"></a><a id="IsTamelyRamified--FldPadExact--FldPadExact"></a>
> **IsTamelyRamified** (E :: *FldPadExact*)
> 
> **IsTamelyRamified** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `E` is tamely ramified over `F` or its base field. That is, the ramification degree is indivisible by `p`.




<a id="IsWildlyRamified"></a><a id="IsWildlyRamified--FldPadExact"></a><a id="IsWildlyRamified--FldPadExact--etc"></a><a id="IsWildlyRamified--FldPadExact--FldPadExact"></a>
> **IsWildlyRamified** (E :: *FldPadExact*)
> 
> **IsWildlyRamified** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `E` is wildly ramified over `F` or its base field. That is, the ramification degree is divisible by `p`.




<a id="IsTotallyWildlyRamified"></a><a id="IsTotallyWildlyRamified--FldPadExact"></a><a id="IsTotallyWildlyRamified--FldPadExact--etc"></a><a id="IsTotallyWildlyRamified--FldPadExact--FldPadExact"></a>
> **IsTotallyWildlyRamified** (E :: *FldPadExact*)
> 
> **IsTotallyWildlyRamified** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `E` is totally wildly ramified over `F` or its base field. That is, the inertia degree is 1 and the ramification degree is a power of `p`.




### Printing
{:#printing}

*Not implemented.*

### Standard form
{:#standard-form}

*Not implemented.*

## Residue class field
{:#residue-class-field}

<a id="ResidueClassField"></a><a id="ResidueClassField--FldPadExact"></a>
> **ResidueClassField** (F :: *FldPadExact*)
> 
> -> *FldFin*, *Map*
> {:.ret}
{:.intrinsic}

The residue class field `FF` of `F`, and the quotient map from `F` to `FF`.

Note that the quotient map has an inverse whose approximations always have absolute precision 1, that is, the precision does not increase with epoch. Use [`WeakApproximation`](#WeakApproximation--FldPadExactElt) to choose a representative to infinite precision.


<a id="ResidueClass"></a><a id="ResidueClass--FldPadExactElt"></a>
> **ResidueClass** (x :: *FldPadExactElt*)
> 
> -> *FldFinElt*
> {:.ret}
{:.intrinsic}

The residue class of `x`.


## Ramification polynomials and polygons
{:#ramification-polynomials-and-polygons}


In this package, if $f(x)$ is an Eisenstein polynomial with a root $\pi$, then we define the *ramification polynomial of $f$* to be $f(x+\pi)$ and the *ramification polygon of $f$* to be the Newton polygon of this. Observe that since $f(\pi)=0$ then the ramification polygon has end vertices at 1 and $\deg f$.

If $L/K$ is totally ramified, then the *ramification polygon of $L/K$* is the ramification polygon of any Eisenstein polynomial defining the extension. If $L/U$ is totally ramified and $U/K$ is unramified then the *ramification polygon of $L/K$* is that of $L/U$ with an additional horizontal face from $((L:U),0)$ to $((L:K),0)$.

The Newton polygon is an invariant of an extension and describes the ramification breaks of the *Galois set* $\Gamma(L/K)$ of embeddings $L \hookrightarrow \bar{K}$. This generalizes ramification theory of Galois extensions, where the Galois set is equal to the Galois group.

See also [the `pAdicExtensions` package](https://cjdoris.github.io/pAdicExtensions) which includes a more specialised, and more general, representation of ramification polygons.

<a id="RamificationResidualPolynomials"></a><a id="RamificationResidualPolynomials--RngUPolElt_FldPadExact"></a>
> **RamificationResidualPolynomials** (f :: *RngUPolElt_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The residual polynomials of the ramification polygon of `f`.


<a id="RamificationResidualPolynomial"></a><a id="RamificationResidualPolynomial--RngUPolElt_FldPadExact--etc"></a><a id="RamificationResidualPolynomial--RngUPolElt_FldPadExact--NwtnPgonFace"></a>
> **RamificationResidualPolynomial** (f :: *RngUPolElt_FldPadExact*, face :: *NwtnPgonFace*)
> 
> -> *RngUPolElt*
> {:.ret}
{:.intrinsic}

The residual polynomial of the given `face` of the ramification polygon of `f`.


<a id="RamificationPolynomial"></a><a id="RamificationPolynomial--FldPadExact"></a>
> **RamificationPolynomial** (L :: *FldPadExact*)
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The ramification polynomial of `L` with respect to its defining polynomial.


<a id="RamificationPolygon"></a><a id="RamificationPolygon--RngUPolElt_FldPadExact"></a>
> **RamificationPolygon** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *NwtnPgon*
> {:.ret}
{:.intrinsic}

The ramification polygon of the extension defined by `f`.


<a id="RamificationPolygon-2"></a><a id="RamificationPolygon--FldPadExact"></a><a id="RamificationPolygon--FldPadExact--etc"></a><a id="RamificationPolygon--FldPadExact--FldPadExact"></a>
> **RamificationPolygon** (E :: *FldPadExact*)
> 
> **RamificationPolygon** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *NwtnPgon*
> {:.ret}
{:.intrinsic}

The ramification polygon of `E` over its base field or `F`.




<a id="RamificationFiltration"></a><a id="RamificationFiltration--FldPadExact--etc"></a><a id="RamificationFiltration--FldPadExact--FldPadExact"></a>
> **RamificationFiltration** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The ramification filtration of `E`/`F`.


## Hasse-Herbrand transition function
{:#hasse-herbrand-transition-function}

### Creation
{:#creation}

<a id="TransitionFunction"></a><a id="TransitionFunction--FldPadExact"></a><a id="TransitionFunction--FldPadExact--etc"></a><a id="TransitionFunction--FldPadExact--FldPadExact"></a><a id="TransitionFunction--FldPad"></a><a id="TransitionFunction--FldPad--etc"></a><a id="TransitionFunction--FldPad--FldPad"></a>
> **TransitionFunction** (E :: *FldPadExact*)
> 
> **TransitionFunction** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> **TransitionFunction** (E :: *FldPad*)
> 
> **TransitionFunction** (E :: *FldPad*, F :: *FldPad*)
> 
> -> *HassHerbTransFunc*
> {:.ret}
{:.intrinsic}

The Hasse-Herbrand transition function of `E` over its base field or `F`.








### Operations
{:#operations}

<a id="Degree-3"></a><a id="Degree--HassHerbTransFunc"></a>
> **Degree** (h :: *HassHerbTransFunc*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The degree of the extension this is the transition function of.


<a id="Vertices"></a><a id="Vertices--HassHerbTransFunc"></a>
> **Vertices** (h :: *HassHerbTransFunc*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The vertices of the function.


<a id="LowerBreaks"></a><a id="LowerBreaks--HassHerbTransFunc"></a>
> **LowerBreaks** (h :: *HassHerbTransFunc*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The lower breaks of `h`.


<a id="UpperBreaks"></a><a id="UpperBreaks--HassHerbTransFunc"></a>
> **UpperBreaks** (h :: *HassHerbTransFunc*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The upper breaks of `h`.


<a id="eq"></a><a id="eq--HassHerbTransFunc--etc"></a><a id="eq--HassHerbTransFunc--HassHerbTransFunc"></a>
> **\'eq\'** (h1 :: *HassHerbTransFunc*, h2 :: *HassHerbTransFunc*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `h1` and `h2` are equal as field invariants, i.e. they define the same function.


<a id="@"></a><a id="@--any--etc"></a><a id="@--any--HassHerbTransFunc"></a>
> **\'@\'** (v, h :: *HassHerbTransFunc*)
> 
> -> Any
> {:.ret}
{:.intrinsic}

Evaluates `h` at `v`.


<a id="@@"></a><a id="@@--any--etc"></a><a id="@@--any--HassHerbTransFunc"></a>
> **\'@@\'** (u, h :: *HassHerbTransFunc*)
> 
> -> Any
> {:.ret}
{:.intrinsic}

The inverse of `h` at `u`.


<a id="RamificationPolygon-3"></a><a id="RamificationPolygon--HassHerbTransFunc"></a>
> **RamificationPolygon** (h :: *HassHerbTransFunc*)
> 
> -> *NwtnPgon*
> {:.ret}
{:.intrinsic}

The ramification polygon of a totally ramified extension with the given transition function.


## Homomorphisms
{:#homomorphisms}

### Creation
{:#creation-2}

<a id="TrivialHomomorphism"></a><a id="TrivialHomomorphism--FldPadExact--etc"></a><a id="TrivialHomomorphism--FldPadExact--FldPadExact"></a>
> **TrivialHomomorphism** (E :: *FldPadExact*, C :: *FldPadExact*)
> 
> -> *HomFldPadExact*
> {:.ret}
{:.intrinsic}

The trivial embedding of `E` into `C`, where `C` is an extension of `E`.


<a id="TrivialIsomorphism"></a><a id="TrivialIsomorphism--FldPadExact"></a>
> **TrivialIsomorphism** (F :: *FldPadExact*)
> 
> -> *HomFldPadExact*
> {:.ret}
{:.intrinsic}

The trivial isomorphism of `F`.


<a id="Homomorphism"></a><a id="Homomorphism--FldPadExact--etc"></a><a id="Homomorphism--FldPadExact--FldPadExactElt"></a>
> **Homomorphism** (E :: *FldPadExact*, g :: *FldPadExactElt*)
> 
> -> *HomFldPadExact*
> {:.ret}
{:.intrinsic}

The homomorphism sending the generator of `E` to `g`.


<a id="Homomorphism-2"></a><a id="Homomorphism--FldPadExact--etc-2"></a><a id="Homomorphism--FldPadExact--seq-FldPadExactElt--FldPadExact"></a>
> **Homomorphism** (E :: *FldPadExact*, gs :: [*FldPadExactElt*], F :: *FldPadExact*)
> 
> -> *HomFldPadExact*
> {:.ret}
{:.intrinsic}

The homomorphism of `E` fixing `F` sending the generators of `E/F` to `gs`.


<a id="Homomorphism-3"></a><a id="Homomorphism--FldPadExact--etc-3"></a><a id="Homomorphism--FldPadExact--HomFldPadExact--seq-FldPadExactElt"></a>
> **Homomorphism** (E :: *FldPadExact*, h0 :: *HomFldPadExact*, gs :: [*FldPadExactElt*])
> 
> -> *HomFldPadExact*
> {:.ret}
{:.intrinsic}

The homomorphism extending `h0`, sending the generators of `E` over the domain of `h0` to `gs`.


<a id="Homomorphisms"></a><a id="Homomorphisms--FldPadExact--etc"></a><a id="Homomorphisms--FldPadExact--FldPadExact--FldPadExact"></a>
> **Homomorphisms** (E :: *FldPadExact*, C :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The homomorphisms of `E` to `C` fixing `F`.

**Parameters**
- `Limit`: Limits the number of homomorphisms returned.

<a id="Isomorphisms"></a><a id="Isomorphisms--FldPadExact--etc"></a><a id="Isomorphisms--FldPadExact--FldPadExact--FldPadExact"></a>
> **Isomorphisms** (E :: *FldPadExact*, C :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The isomorphsisms of `E` to `C` fixing `F`.

**Parameters**
- `Limit`: Limits the number of isomorphisms returned.

<a id="HasIsomorphism"></a><a id="HasIsomorphism--FldPadExact--etc"></a><a id="HasIsomorphism--FldPadExact--FldPadExact--FldPadExact"></a>
> **HasIsomorphism** (E :: *FldPadExact*, C :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *BoolElt*, *HomFldPadExact*
> {:.ret}
{:.intrinsic}

True if there is an isomorphism of `E` to `C` fixing `F`. If so, also returns an isomorphism.


<a id="Automorphisms"></a><a id="Automorphisms--FldPadExact--etc"></a><a id="Automorphisms--FldPadExact--FldPadExact"></a>
> **Automorphisms** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The automorphisms of `E` fixing `F`.


### Inspection
{:#inspection}

<a id="Domain"></a><a id="Domain--HomFldPadExact"></a>
> **Domain** (h :: *HomFldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The domain of `h`.


<a id="Codomain"></a><a id="Codomain--HomFldPadExact"></a>
> **Codomain** (h :: *HomFldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The codomain of `h`.


<a id="BaseField-2"></a><a id="BaseField--HomFldPadExact"></a>
> **BaseField** (h :: *HomFldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The field fixed by `h`.


<a id="HasInverse"></a><a id="HasInverse--HomFldPadExact"></a>
> **HasInverse** (h :: *HomFldPadExact*)
> 
> -> *BoolElt*, *HomFldPadExact*
> {:.ret}
{:.intrinsic}

True if `h` has an inverse defined. If so, also returns the inverse.


<a id="Inverse"></a><a id="Inverse--HomFldPadExact"></a>
> **Inverse** (h :: *HomFldPadExact*)
> 
> -> *HomFldPadExact*
> {:.ret}
{:.intrinsic}

The inverse of `h`.


<a id="GeneratorImages"></a><a id="GeneratorImages--HomFldPadExact"></a>
> **GeneratorImages** (h :: *HomFldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The sequence of images of the generators of the intermediate fields from the base field up to the domain.


### Application
{:#application}

<a id="@-2"></a><a id="@--any--etc-2"></a><a id="@--any--HomFldPadExact"></a>
> **\'@\'** (x, h :: *HomFldPadExact*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

The image of `x` under the homomorphism.


<a id="@@-2"></a><a id="@@--any--etc-2"></a><a id="@@--any--HomFldPadExact"></a>
> **\'@@\'** (x, h :: *HomFldPadExact*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

The image of `x` under the inverse homomorphism.


<a id="*-2"></a><a id="*--HomFldPadExact--etc"></a><a id="*--HomFldPadExact--HomFldPadExact"></a>
> **\'\*\'** (h1 :: *HomFldPadExact*, h2 :: *HomFldPadExact*)
> 
> -> *HomFldPadExact*
> {:.ret}
{:.intrinsic}

Composition, such that `x @ (h1 * h2) = x @ h1 @ h2`.


### Automorphism group
{:#automorphism-group}

<a id="AutomorphismGroup"></a><a id="AutomorphismGroup--FldPadExact--etc"></a><a id="AutomorphismGroup--FldPadExact--FldPadExact"></a>
> **AutomorphismGroup** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *GrpPerm*, *Map*
> {:.ret}
{:.intrinsic}

The automorphism group of `E/F` as a permutation group, and the map from the group to the set of automorphisms.


## Internals
{:#internals}

### Approximations
{:#approximations}

<a id="WeakValuation"></a><a id="WeakValuation--FldPadExactElt"></a>
> **WeakValuation** (x :: *FldPadExactElt*)
> 
> -> *ValFldPadExactElt*
> {:.ret}
{:.intrinsic}

The weak valuation of `x`.


<a id="AbsolutePrecision"></a><a id="AbsolutePrecision--FldPadExactElt"></a>
> **AbsolutePrecision** (x :: *FldPadExactElt*)
> 
> -> *ValFldPadExactElt*
> {:.ret}
{:.intrinsic}

The absolute precision of `x`.


<a id="IsWeaklyZero"></a><a id="IsWeaklyZero--FldPadExactElt"></a>
> **IsWeaklyZero** (x :: *FldPadExactElt*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `x` is weakly zero.


<a id="IsDefinitelyZero"></a><a id="IsDefinitelyZero--FldPadExactElt"></a>
> **IsDefinitelyZero** (x :: *FldPadExactElt*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `x` is definitely zero. That is, it is weakly zero and has infinite absolute precision.


<a id="WeakApproximation"></a><a id="WeakApproximation--FldPadExactElt"></a>
> **WeakApproximation** (x :: *FldPadExactElt*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

An element weakly equal to `x` at its current precision.


<a id="EnsureAllApproximationsNonzero"></a><a id="EnsureAllApproximationsNonzero--FldPadExactElt"></a>
> **EnsureAllApproximationsNonzero** (x :: *FldPadExactElt*)
{:.intrinsic}

Ensures that all approximations of `x` are non-zero.


### ExtFldPadExact
{:#extfldpadexact}


This type represents an extension of p-adic fields. It is the second return value of [`IsExtensionOf`](#IsExtensionOf), and each field caches the extensions of which it is the top field. It can be used to cache information about an extension, such as its degree.

For most intrinsics which take two fields forming an extension, there is an alternative form taking a single extension.

<a id="/-2"></a><a id="/--FldPadExact--etc"></a><a id="/--FldPadExact--FldPadExact"></a>
> **\'/\'** (E :: *FldPadExact*, F :: *FldPadExact*)
> 
> -> *ExtFldPadExact*
> {:.ret}
{:.intrinsic}

The extension `E/F`.


<a id="Description"></a><a id="Description--ExtFldPadExact"></a>
> **Description** (X :: *ExtFldPadExact*)
> 
> -> *MonStgElt*
> {:.ret}
{:.intrinsic}

A string describing the extension.


**Parameters**
- `BaseName`: If given, this is used to describe the base field. Otherwise, the base field is not described.

<a id="TopField"></a><a id="TopField--ExtFldPadExact"></a>
> **TopField** (X :: *ExtFldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The top field of the extension.


<a id="BaseField-3"></a><a id="BaseField--ExtFldPadExact"></a>
> **BaseField** (X :: *ExtFldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The base field of the extension.


<a id="Tower"></a><a id="Tower--ExtFldPadExact"></a>
> **Tower** (X :: *ExtFldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The tower of intermediate fields.

Its length is at least 1. The first entry is the base field, the last entry is the top field, and each entry is the base field of the next.


<a id="Tower0"></a><a id="Tower0--ExtFldPadExact"></a>
> **Tower0** (X :: *ExtFldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

Same as `Tower` but with the first entry (the base field) omitted.


