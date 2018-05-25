# Univariate polynomials
{:#univariate-polynomials}


**Contents**
* [Creation of rings](#creation-of-rings)
* [Ring basics](#ring-basics)
* [Creation of polynomials](#creation-of-polynomials)
  * [Special values](#special-values)
  * [From coefficients](#from-coefficients)
  * [Coercion](#coercion)
* [Polynomial basics](#polynomial-basics)
  * [Degree](#degree)
  * [Coefficients](#coefficients)
  * [Arithmetic](#arithmetic)
  * [Derivative](#derivative)
  * [Evaluate](#evaluate)
  * [Special forms](#special-forms)
* [Discriminant and resultant](#discriminant-and-resultant)
* [Newton polygon](#newton-polygon)
* [Hensel lifting](#hensel-lifting)
* [Root-finding and factorization](#root-finding-and-factorization)
* [Internals](#internals)
  * [Approximation](#approximation)

## Creation of rings
{:#creation-of-rings}

<a id="PolynomialRing"></a><a id="PolynomialRing--FldPadExact"></a>
> **PolynomialRing** (F :: *FldPadExact*)
> 
> -> *RngUPol_FldPadExact*
> {:.ret}
{:.intrinsic}

The univariate polynomial ring over `F`.


## Ring basics
{:#ring-basics}

<a id="BaseRing"></a><a id="BaseRing--RngUPol_FldPadExact"></a>
> **BaseRing** (R :: *RngUPol_FldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The base ring of `R`.


## Creation of polynomials
{:#creation-of-polynomials}

### Special values
{:#special-values}

<a id="Generator"></a><a id="Generator--RngUPol_FldPadExact"></a>
> **Generator** (R :: *RngUPol_FldPadExact*)
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The generator of `R`.


<a id="Zero"></a><a id="Zero--RngUPol_FldPadExact"></a>
> **Zero** (R :: *RngUPol_FldPadExact*)
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Zero and one.


### From coefficients
{:#from-coefficients}

<a id="Polynomial"></a><a id="Polynomial--seq-FldPadExactElt"></a>
> **Polynomial** (cs :: [*FldPadExactElt*])
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The polynomial with coefficients `cs`.


<a id="Polynomial-2"></a><a id="Polynomial--FldPadExact--etc"></a><a id="Polynomial--FldPadExact--seq"></a>
> **Polynomial** (F :: *FldPadExact*, cs :: [])
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The polynomial over `F` with coefficients `cs`.


### Coercion
{:#coercion}


We can coerce the following to a polynomial in `R`:
- A polynomial in `R`
- A polynomial whose coefficients are coercible to the base ring of `R`
- A sequence of anything coercible to the base ring of `R`
- Anything coercible to the base ring of `R`

<a id="IsCoercible"></a><a id="IsCoercible--RngUPol_FldPadExact--etc"></a><a id="IsCoercible--RngUPol_FldPadExact--any"></a>
> **IsCoercible** (R :: *RngUPol_FldPadExact*, X)
> 
> -> *BoolElt*, Any
> {:.ret}
{:.intrinsic}

True if `X` is coercible to `R`.


<a id="ChangeRing"></a><a id="ChangeRing--RngUPolElt_FldPadExact--etc"></a><a id="ChangeRing--RngUPolElt_FldPadExact--FldPadExact"></a><a id="ChangeRing--RngUPolElt--etc"></a><a id="ChangeRing--RngUPolElt--FldPadExact"></a>
> **ChangeRing** (f :: *RngUPolElt_FldPadExact*, F :: *FldPadExact*)
> 
> **ChangeRing** (f :: *RngUPolElt*, F :: *FldPadExact*)
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Changes the base ring of `f` to `F`.




## Polynomial basics
{:#polynomial-basics}

### Degree
{:#degree}

<a id="Degree"></a><a id="Degree--RngUPolElt_FldPadExact"></a>
> **Degree** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The degree of `f`.


### Coefficients
{:#coefficients}

<a id="Coefficient"></a><a id="Coefficient--RngUPolElt_FldPadExact--etc"></a><a id="Coefficient--RngUPolElt_FldPadExact--RngIntElt"></a>
> **Coefficient** (f :: *RngUPolElt_FldPadExact*, i :: *RngIntElt*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The `i`th coefficient of `f`.


<a id="Coefficients"></a><a id="Coefficients--RngUPolElt_FldPadExact"></a>
> **Coefficients** (f :: *RngUPolElt_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The coefficients of `f`.


<a id="LeadingCoefficient"></a><a id="LeadingCoefficient--RngUPolElt_FldPadExact"></a>
> **LeadingCoefficient** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

The leading coefficient of `f`.


### Arithmetic
{:#arithmetic}

<a id="-"></a><a id="---RngUPolElt_FldPadExact"></a><a id="+"></a><a id="+--RngUPolElt_FldPadExact--etc"></a><a id="+--RngUPolElt_FldPadExact--RngUPolElt_FldPadExact"></a><a id="---RngUPolElt_FldPadExact--etc"></a><a id="---RngUPolElt_FldPadExact--RngUPolElt_FldPadExact"></a><a id="*"></a><a id="*--RngUPolElt_FldPadExact--etc"></a><a id="*--RngUPolElt_FldPadExact--RngUPolElt_FldPadExact"></a><a id="/"></a><a id="/--RngUPolElt_FldPadExact--etc"></a><a id="/--RngUPolElt_FldPadExact--FldPadExactElt"></a><a id="^"></a><a id="^--RngUPolElt_FldPadExact--etc"></a><a id="^--RngUPolElt_FldPadExact--RngIntElt"></a><a id="&+"></a><a id="&+--seq-RngUPolElt_FldPadExact"></a><a id="&*"></a><a id="&*--seq-RngUPolElt_FldPadExact"></a>
> **\'-\'** (f :: *RngUPolElt_FldPadExact*)
> 
> **\'+\'** (f :: *RngUPolElt_FldPadExact*, g :: *RngUPolElt_FldPadExact*)
> 
> **\'-\'** (f :: *RngUPolElt_FldPadExact*, g :: *RngUPolElt_FldPadExact*)
> 
> **\'\*\'** (f :: *RngUPolElt_FldPadExact*, g :: *RngUPolElt_FldPadExact*)
> 
> **\'/\'** (f :: *RngUPolElt_FldPadExact*, x :: *FldPadExactElt*)
> 
> **\'^\'** (f :: *RngUPolElt_FldPadExact*, m :: *RngIntElt*)
> 
> **\'&+\'** (fs :: [*RngUPolElt_FldPadExact*])
> 
> **\'&\*\'** (fs :: [*RngUPolElt_FldPadExact*])
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Negate, add, subtract, multiply, divide by scalar, power, sum, product.















**Parameters**
- `Safe := false`: When true, this may be used as an intermediate variable in [`WithDependencies`]({{site.baseurl}}/internals#WithDependencies) with the `Fast` option.

<a id="div"></a><a id="div--RngUPolElt_FldPadExact--etc"></a><a id="div--RngUPolElt_FldPadExact--RngUPolElt_FldPadExact"></a><a id="mod"></a><a id="mod--RngUPolElt_FldPadExact--etc"></a><a id="mod--RngUPolElt_FldPadExact--RngUPolElt_FldPadExact"></a>
> **\'div\'** (f :: *RngUPolElt_FldPadExact*, g :: *RngUPolElt_FldPadExact*)
> 
> **\'mod\'** (f :: *RngUPolElt_FldPadExact*, g :: *RngUPolElt_FldPadExact*)
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Division and remainder.



**Parameters**
- `Safe := false`: When true, this may be used as an intermediate variable in [`WithDependencies`]({{site.baseurl}}/internals#WithDependencies) with the `Fast` option.

### Derivative
{:#derivative}

<a id="Derivative"></a><a id="Derivative--RngUPolElt_FldPadExact--etc"></a><a id="Derivative--RngUPolElt_FldPadExact--RngIntElt"></a>
> **Derivative** (f :: *RngUPolElt_FldPadExact*, m :: *RngIntElt*)
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The `m`th or first derivative of `f`.


<a id="Derivative-2"></a><a id="Derivative--RngUPolElt_FldPadExact"></a>
> **Derivative** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The derivative of `f`.


### Evaluate
{:#evaluate}

<a id="Evaluate"></a><a id="Evaluate--RngUPolElt_FldPadExact--etc"></a><a id="Evaluate--RngUPolElt_FldPadExact--FldPadExactElt"></a>
> **Evaluate** (f :: *RngUPolElt_FldPadExact*, x :: *FldPadExactElt*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

Evaluates `f(x)`.


<a id="Evaluate-2"></a><a id="Evaluate--RngUPolElt_FldPadExact--etc-2"></a><a id="Evaluate--RngUPolElt_FldPadExact--RngUPolElt_FldPadExact"></a>
> **Evaluate** (f :: *RngUPolElt_FldPadExact*, g :: *RngUPolElt_FldPadExact*)
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Evaluates `f(g)`.


### Special forms
{:#special-forms}

<a id="IsEisenstein"></a><a id="IsEisenstein--RngUPolElt_FldPadExact"></a>
> **IsEisenstein** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `f` is Eisenstein. That is, the leading coefficient has valuation 0, the constant coefficient has valuation 1, and the other coefficients have valuation at least 1. Eisenstein polynomials define totally ramified extensions.


<a id="IsInertial"></a><a id="IsInertial--RngUPolElt_FldPadExact"></a>
> **IsInertial** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `f` is inertial. That is, it is integral, the leading coefficient has valuation 0, and it is irreducible over the residue class field. Inertial polynomials define unramified extensions.


## Discriminant and resultant
{:#discriminant-and-resultant}

<a id="Discriminant"></a><a id="Discriminant--RngUPolElt_FldPadExact"></a>
> **Discriminant** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The discriminant of `f`.

**Parameters**
- `Safe := false`: When true, this may be used as an intermediate variable in [`WithDependencies`]({{site.baseurl}}/internals#WithDependencies) with the `Fast` option.

<a id="Resultant"></a><a id="Resultant--RngUPolElt_FldPadExact--etc"></a><a id="Resultant--RngUPolElt_FldPadExact--RngUPolElt_FldPadExact"></a>
> **Resultant** (f :: *RngUPolElt_FldPadExact*, g :: *RngUPolElt_FldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The resultant of `f` and `g`.

**Parameters**
- `Safe := false`: When true, this may be used as an intermediate variable in [`WithDependencies`]({{site.baseurl}}/internals#WithDependencies) with the `Fast` option.

## Newton polygon
{:#newton-polygon}

<a id="NewtonPolygon"></a><a id="NewtonPolygon--RngUPolElt_FldPadExact"></a>
> **NewtonPolygon** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *NwtnPgon*
> {:.ret}
{:.intrinsic}

The Newton polygon of `f`.

If some of the coefficients of `f` are weakly zero, it can sometimes be quicker to find just part of the polygon. The `Support` parameter controls how much of the Newton polygon is required, and is one of:
- A single integer or rational, which must be in the support.
- A sequence or tuple of two integers or rationals, which specify an interval which must be in the support.
- A function accepting a Newton polygon and returning true if its support is valid.


**Parameters**
- `Support`: Specifies a lower bound on the support of the returned polygon.

## Hensel lifting
{:#hensel-lifting}

<a id="IsHenselLiftable"></a><a id="IsHenselLiftable--RngUPolElt_FldPadExact--etc"></a><a id="IsHenselLiftable--RngUPolElt_FldPadExact--FldPadExactElt"></a>
> **IsHenselLiftable** (f :: *RngUPolElt_FldPadExact*, x :: *FldPadExactElt*)
> 
> -> *BoolElt*, *FldPadExactElt*
> {:.ret}
{:.intrinsic}

True if `x` is Hensel-liftable to a root of `f`. If so, also returns the root.

This uses a generalized statement of Hensel's lemma which does not require the inputs to be integral, namely:

**Hensel's lemma.** *If $f(x) \in K[x]$ and $x \in K$ such that $x$ is closer to one root of $f$ than any other, then iterating $x \mapsto x - f(x)/f'(x)$ converges to that root.*


<a id="IsHenselLiftable-2"></a><a id="IsHenselLiftable--RngUPolElt_FldPadExact--etc-2"></a><a id="IsHenselLiftable--RngUPolElt_FldPadExact--RngUPolElt_FldPadExact"></a>
> **IsHenselLiftable** (f :: *RngUPolElt_FldPadExact*, g :: *RngUPolElt_FldPadExact*)
> 
> -> *BoolElt*, *RngUPolElt_FldPadExact*, *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

True if `g` is Hensel-liftable to a factor of `f`. If so, also returns the factor (with the same leading coefficient as `g`) and its cofactor.

**Future.** Optionally choose `Slope`, `fShift` and `gShift` automagically.


**Parameters**
- `Slope := 0`: A rational number, deslope the polynomials by this amount before applying Hensel's lemma; usually Slope will be a slope of the Newton polygon of `g`.
- `fShift := 0`: A rational number, subtract this from the valuation of `f` after applying `Slope`.
- `gShift := 0`: A rational number, subtract this from the valuation of `g` after applying `Slope`.

## Root-finding and factorization
{:#root-finding-and-factorization}

<a id="Roots"></a><a id="Roots--RngUPolElt_FldPadExact"></a>
> **Roots** (f :: *RngUPolElt_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The roots of `f` over its base ring, as a sequence of `<root,multiplicity>` pairs. Aside from some (exactly) zero roots, which are handled separately, `f` must be squarefree.


<a id="Factorization"></a><a id="Factorization--RngUPolElt_FldPadExact"></a>
> **Factorization** (f :: *RngUPolElt_FldPadExact*)
> 
> -> [], *FldPadExactElt*, []
> {:.ret}
{:.intrinsic}

The factorization of `f` over its base ring, as a sequence of `<factor,multiplicty>` pairs. Aside from some (exactly) zero roots, which are handled separately, `f` must be squarefree. Also returns the leading coefficient of `f`.

Internally, this calls `ExactpAdics_Factorization`, which has more parameters.


**Parameters**
- `Certificates := false`: When `true`, also returns a sequence of certificates corresponding to the factors.
- `Extensions := false`: When `true`, implies `Certificates:=true`, and the certificates also include the extension defined by the factor.

<a id="NewtonPolygonFactorization"></a><a id="NewtonPolygonFactorization--RngUPolElt_FldPadExact"></a>
> **NewtonPolygonFactorization** (f :: *RngUPolElt_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The factorization of `f` according to its Newton polygon, as a sequence of factors. The factors are ordered by slope, from lowest (most negative) to highest.


**Parameters**
- `Residual := false`: When `true` then further factorizes according to the factorization of each residual polynomial into powers of irreducibles.

<a id="ExactpAdics_Factorization"></a><a id="ExactpAdics_Factorization--RngUPolElt_FldPadExact"></a>
> **ExactpAdics_Factorization** (f :: *RngUPolElt_FldPadExact*)
> 
> -> [], *FldPadExactElt*, []
> {:.ret}
{:.intrinsic}

Called internally by `Factorization`.


**Parameters**
- `Proof := true`: When true, the output is proven.
- `Certificates := false`: When true, implies `Proof:=true` and returns certificates.
- `Extensions := false`: When true, implies `Certificates:=true` and certificates include extensions.
- `InternalData := false`: When true, implies `Certificates:=true` and certificates include the state of the branch leading to this factor.
- `SimpleLift := false`: When true, uses "single factor lifting" just enough to use simple Hensel lifting on the factors. Probably slower, but possibly more reliable.
- `DegreeMle := 0`: Only returns factors whose degree divides this, i.e. the degree is "multiplicatively less than" this.
- `DegreeGe := 1`: Only returns factors whose degree is at least this.
- `Limit`: A bound on the number of factors returned.

<a id="ExactpAdics_Roots"></a><a id="ExactpAdics_Roots--RngUPolElt_FldPadExact"></a>
> **ExactpAdics_Roots** (f :: *RngUPolElt_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

Called internally by `Roots`.

**Parameters**
- `Limit`

<a id="ExactpAdics_Factorization-2"></a><a id="ExactpAdics_Factorization--RngUPolElt-FldPad"></a>
> **ExactpAdics_Factorization** (f :: *RngUPolElt*[*FldPad*])
> 
> -> [], *FldPadElt*, []
> {:.ret}
{:.intrinsic}

Our implementation of an OM factorization algorithm for Magma's builtin p-adics.


**Parameters**
- `Proof := true`: When true, the output is proven.
- `Certificates := false`: When true, implies `Proof:=true` and also outputs certificates.
- `Extensions := false`: When true, implies `Certificates:=true` and certificates include extensions.
- `InternalData := false`: When true, implies `Certificates:=true` and certificates include the state of the branch leading to this factor.
- `Lift := true`: When false, does not lift the result to full precision. Hence faster, but gives less precise results.
- `DegreeMle := 0`: Only returns factors whose degree divides this, i.e. the degree is "multiplicatively less than" this.
- `DegreeGe := 1`: Only returns factors whose degree is at least this.
- `Limit`: A bound on the number of factors returned.

<a id="ExactpAdics_Roots-2"></a><a id="ExactpAdics_Roots--RngUPolElt-FldPad"></a>
> **ExactpAdics_Roots** (f :: *RngUPolElt*[*FldPad*])
> 
> -> []
> {:.ret}
{:.intrinsic}

Our implementation of an OM factorization algorithm, specialised to root-finding, for Magma's builtin p-adics.


**Parameters**
- `Lift := true`: When false, does not lift the result to full precision. Hence faster, but gives less precise results.

## Internals
{:#internals}

### Approximation
{:#approximation}

<a id="WeakValuation"></a><a id="WeakValuation--RngUPolElt_FldPadExact"></a>
> **WeakValuation** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *ValRngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The weak valuation of `f`.


<a id="AbsolutePrecision"></a><a id="AbsolutePrecision--RngUPolElt_FldPadExact"></a>
> **AbsolutePrecision** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *ValRngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The weak valuation of `f`.


<a id="WeakDegree"></a><a id="WeakDegree--RngUPolElt_FldPadExact"></a>
> **WeakDegree** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The weak degree of `f`, an upper bound on the actual degree.


<a id="WeakApproximation"></a><a id="WeakApproximation--RngUPolElt_FldPadExact"></a>
> **WeakApproximation** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *RngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

A polynomial weakly equal to `f` at its current precision.


<a id="IsDefinitelyFullDegree"></a><a id="IsDefinitelyFullDegree--RngUPolElt_FldPadExact"></a>
> **IsDefinitelyFullDegree** (f :: *RngUPolElt_FldPadExact*)
> 
> -> *BoolElt*, *RngIntElt*
> {:.ret}
{:.intrinsic}

True if `f` is definitely full degree.

**Parameters**
- `Minimize`

<a id="EnsureAllApproximationsFullDegree"></a><a id="EnsureAllApproximationsFullDegree--RngUPolElt_FldPadExact"></a>
> **EnsureAllApproximationsFullDegree** (f :: *RngUPolElt_FldPadExact*)
{:.intrinsic}

Ensures that all approximations of `f` are full-degree.


