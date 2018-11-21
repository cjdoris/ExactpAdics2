# Multivariate polynomials
{:#multivariate-polynomials}


**Contents**
* [Creation of rings](#creation-of-rings)
* [Basic operations on rings](#basic-operations-on-rings)
* [Creation of polynomials](#creation-of-polynomials)
  * [Coercion](#coercion)
* [Basic operations on polynomials](#basic-operations-on-polynomials)
  * [Derivative](#derivative)
  * [Evaluate](#evaluate)
* [Hensel lifting](#hensel-lifting)
* [Internals](#internals)
  * [Approximation](#approximation)

## Creation of rings
{:#creation-of-rings}

<a id="PolynomialRing"></a><a id="PolynomialRing--FldPadExact--etc"></a><a id="PolynomialRing--FldPadExact--RngIntElt"></a>
> **PolynomialRing** (F :: *FldPadExact*, k :: *RngIntElt*)
> 
> -> *RngMPol_FldPadExact*
> {:.ret}
{:.intrinsic}

The polynomial ring of rank `k` over `F`.


## Basic operations on rings
{:#basic-operations-on-rings}

<a id="BaseRing"></a><a id="BaseRing--RngMPol_FldPadExact"></a>
> **BaseRing** (R :: *RngMPol_FldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The base ring of `R`.


<a id="Rank"></a><a id="Rank--RngMPol_FldPadExact"></a>
> **Rank** (R :: *RngMPol_FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The rank of `R`.


<a id="Generator"></a><a id="Generator--RngMPol_FldPadExact--etc"></a><a id="Generator--RngMPol_FldPadExact--RngIntElt"></a>
> **Generator** (R :: *RngMPol_FldPadExact*, i :: *RngIntElt*)
> 
> -> *RngMPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The `i`th generator of `R`.


<a id="Generators"></a><a id="Generators--RngMPol_FldPadExact"></a>
> **Generators** (R :: *RngMPol_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The generators of `R`.


## Creation of polynomials
{:#creation-of-polynomials}

### Coercion
{:#coercion}

The following are coercible to a multivariate polynomial in `R`:
- A polynomial in `R`.
- A multivariate polynomial of correct rank whose coefficients are coercible into the base ring of `R`.
- A sequence of tuples, whose first element is a coefficient and whose second element is an exponent vector.
- Anything coercible to the base ring of `R`.

<a id="IsCoercible"></a><a id="IsCoercible--RngMPol_FldPadExact--etc"></a><a id="IsCoercible--RngMPol_FldPadExact--any"></a>
> **IsCoercible** (R :: *RngMPol_FldPadExact*, X)
> 
> -> *BoolElt*, Any
> {:.ret}
{:.intrinsic}

True if `X` is coercible to an element of `R`. If so, also returns the coerced element.


## Basic operations on polynomials
{:#basic-operations-on-polynomials}

<a id="MonomialCoefficient"></a><a id="MonomialCoefficient--RngMPolElt_FldPadExact--etc"></a><a id="MonomialCoefficient--RngMPolElt_FldPadExact--RngMPolElt_FldPadExact"></a>
> **MonomialCoefficient** (f :: *RngMPolElt_FldPadExact*, m :: *RngMPolElt_FldPadExact*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

The coefficient of monomial `m` in `f`.


<a id="ExponentsCoefficient"></a><a id="ExponentsCoefficient--RngMPolElt_FldPadExact--etc"></a><a id="ExponentsCoefficient--RngMPolElt_FldPadExact--seq-RngIntElt"></a>
> **ExponentsCoefficient** (f :: *RngMPolElt_FldPadExact*, e :: [*RngIntElt*])
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

The coefficient of exponent `e` in `f`.


<a id="Monomial"></a><a id="Monomial--RngMPol_FldPadExact--etc"></a><a id="Monomial--RngMPol_FldPadExact--seq-RngIntElt"></a>
> **Monomial** (R :: *RngMPol_FldPadExact*, e :: [*RngIntElt*])
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

The monomial of `R` with exponents `e`.


<a id="IsDefinitelyMonomial"></a><a id="IsDefinitelyMonomial--RngMPolElt_FldPadExact"></a>
> **IsDefinitelyMonomial** (f :: *RngMPolElt_FldPadExact*)
> 
> -> *BoolElt*, []
> {:.ret}
{:.intrinsic}

True if `f` is definitely a monomial (i.e. has one term). If so, also returns its exponents.


<a id="Exponents"></a><a id="Exponents--RngMPolElt_FldPadExact"></a>
> **Exponents** (m :: *RngMPolElt_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The exponents of `m`, which must be a monomial.


<a id="-"></a><a id="---RngMPolElt_FldPadExact"></a><a id="+"></a><a id="+--RngMPolElt_FldPadExact--etc"></a><a id="+--RngMPolElt_FldPadExact--RngMPolElt_FldPadExact"></a><a id="---RngMPolElt_FldPadExact--etc"></a><a id="---RngMPolElt_FldPadExact--RngMPolElt_FldPadExact"></a><a id="*"></a><a id="*--RngMPolElt_FldPadExact--etc"></a><a id="*--RngMPolElt_FldPadExact--RngMPolElt_FldPadExact"></a><a id="/"></a><a id="/--RngMPolElt_FldPadExact--etc"></a><a id="/--RngMPolElt_FldPadExact--FldPadExactElt"></a><a id="&+"></a><a id="&+--seq-RngMPolElt_FldPadExact"></a><a id="&*"></a><a id="&*--seq-RngMPolElt_FldPadExact"></a>
> **\'-\'** (f :: *RngMPolElt_FldPadExact*)
> 
> **\'+\'** (f :: *RngMPolElt_FldPadExact*, g :: *RngMPolElt_FldPadExact*)
> 
> **\'-\'** (f :: *RngMPolElt_FldPadExact*, g :: *RngMPolElt_FldPadExact*)
> 
> **\'\*\'** (f :: *RngMPolElt_FldPadExact*, g :: *RngMPolElt_FldPadExact*)
> 
> **\'/\'** (f :: *RngMPolElt_FldPadExact*, x :: *FldPadExactElt*)
> 
> **\'&+\'** (fs :: [*RngMPolElt_FldPadExact*])
> 
> **\'&\*\'** (fs :: [*RngMPolElt_FldPadExact*])
> 
> -> *RngMPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Negate, add, subtract, multiply, divide by scalar, sum, product.













**Parameters**
- `Safe := false`: When true, this may be used as an intermediate variable in [`WithDependencies`]({{site.baseurl}}/internals#WithDependencies) with the `Fast` option.

### Derivative
{:#derivative}

<a id="Derivative"></a><a id="Derivative--RngMPolElt_FldPadExact--etc"></a><a id="Derivative--RngMPolElt_FldPadExact--RngIntElt--RngIntElt"></a><a id="Derivative--RngMPolElt_FldPadExact--RngIntElt--RngMPolElt_FldPadExact"></a><a id="Derivative--RngMPolElt_FldPadExact--RngIntElt"></a><a id="Derivative--RngMPolElt_FldPadExact--RngMPolElt_FldPadExact"></a>
> **Derivative** (f :: *RngMPolElt_FldPadExact*, m :: *RngIntElt*, v :: *RngIntElt*)
> 
> **Derivative** (f :: *RngMPolElt_FldPadExact*, m :: *RngIntElt*, v :: *RngMPolElt_FldPadExact*)
> 
> **Derivative** (f :: *RngMPolElt_FldPadExact*, v :: *RngIntElt*)
> 
> **Derivative** (f :: *RngMPolElt_FldPadExact*, v :: *RngMPolElt_FldPadExact*)
> 
> -> *RngMPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The `m`th or first derivative of `f` with respect to variable `v`.








### Evaluate
{:#evaluate}

<a id="Evaluate"></a><a id="Evaluate--RngMPolElt_FldPadExact--etc"></a><a id="Evaluate--RngMPolElt_FldPadExact--seq-FldPadExactElt"></a>
> **Evaluate** (f :: *RngMPolElt_FldPadExact*, xs :: [*FldPadExactElt*])
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

Evaluates `f(xs)`.


## Hensel lifting
{:#hensel-lifting}

<a id="IsHenselLiftable"></a><a id="IsHenselLiftable--seq-RngMPolElt_FldPadExact--etc"></a><a id="IsHenselLiftable--seq-RngMPolElt_FldPadExact--seq-FldPadExactElt"></a>
> **IsHenselLiftable** (fs :: [*RngMPolElt_FldPadExact*], xs :: [*FldPadExactElt*])
> 
> -> *BoolElt*, []
> {:.ret}
{:.intrinsic}

True if `xs` are Hensel liftable to a system of roots of `fs`. If so, also returns the system of roots.

`fs` must be a system of `n` equations of rank `n`, and `xs` must be a sequence of `n` p-adic numbers.


**Parameters**
- `Strategy := "default"`: The precision strategy to use.
- `Slopes`: When given, must be a sequence of `n` rationals to slope the equations by. That is, conceptually we multiply the `i`th variable by `pi^Slopes[i]` and `xs[i]` correspondingly by `pi^-Slopes[i]`. When not given, the zero slope is used.
- `Shifts`: When given, must be a sequence of `n` rationals to shift the equations by. That is, conceptually we multiply the `i`th equation by `pi^Shifts[i]`. When not given, the best shifts are chosen.
- `AsTuple := false`: When `true`, the solution is returned as a `Tup_FldPad`, not as a sequence.

## Internals
{:#internals}

### Approximation
{:#approximation}

<a id="WeakMonomials"></a><a id="WeakMonomials--RngMPolElt_FldPadExact"></a>
> **WeakMonomials** (f :: *RngMPolElt_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The monomials of `f`. Some of the corresponding coefficients may be zero.


<a id="WeakCoefficients"></a><a id="WeakCoefficients--RngMPolElt_FldPadExact"></a>
> **WeakCoefficients** (f :: *RngMPolElt_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The coefficients of `f` corresponding to `WeakMonomials(f)`.


<a id="WeakCoefficientsAndMonomials"></a><a id="WeakCoefficientsAndMonomials--RngMPolElt_FldPadExact"></a>
> **WeakCoefficientsAndMonomials** (f :: *RngMPolElt_FldPadExact*)
> 
> -> [], []
> {:.ret}
{:.intrinsic}

The coefficients and monomials of `f`.


