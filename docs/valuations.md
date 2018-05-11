# Valuations
{:#valuations}



**Contents**
* [Introduction](#introduction)
* [Generic intrinsics](#generic-intrinsics)
* [ValFldPadExactElt](#valfldpadexactelt)
  * [Creation](#creation)
  * [Special values](#special-values)
  * [Other operations](#other-operations)
* [ValRngUPolElt_FldPadExact](#valrngupolelt_fldpadexact)
  * [Creation](#creation-2)
  * [Special values](#special-values-2)
  * [Other operations](#other-operations-2)


## Introduction
{:#introduction}


In this package, we define new types to represent valuations of p-adic numbers and polynomials. These are also used to represent precisions.

The valuation of a p-adic number is represented by the type `ValFldPadExactElt`, whose value is either an integer, or positive or negative infinity. Mathematically its values are in $Z := \ZZ \cup \{\pm\infty\}$. Addition of valuations corresponds to multiplications of p-adics, so we define this. On the other hand, multiplication of two valuations has no natural interpretation, so we do not define this. Taking the minimum of two valuations is defined, since this bounds the valuation of the sum of the corresponding p-adics. Hence $Z$ is more like the *tropical ring of integers* than the usual ring of integers $\ZZ$. Multiplying by an ordinary integer (*scalar multiplication*) is defined because this corresponds to exponentiation of p-adic numbers. They are also totally ordered. For convenience, we extend $Z$ to include the rationals $\QQ$ too.

The valuation of a polynomial is (by definition in the package) a function taking an exponent vector to the valuation of the corresponding coefficient. That is, for polynomials of rank $n$, it is a function $\NN^n \to Z^n$, i.e. an element of $Z^{\NN^n}$. They are represented by the type `Val_RngUPolElt_FldPad` for univariate polynomials and `Val_RngMPolElt_FldPad` for multivariate polynomials over p-adic fields. Since polynomials by definition have only finitely many non-zero coefficients, the function is constant except for finitely many inputs. We can define a partial ordering on these valuations: $v_1 < v_2$ iff for all $n \in \NN$ then $v_1(n) < v_2(n)$. This partial ordering gives us suprema and infema (defined pointwise), and we can also define addition and scalar multiplication pointwise.

## Generic intrinsics
{:#generic-intrinsics}


In this section we document intrinsics common to all valuations. Where there are multiple `Val` inputs, it suffices for only one to be a `Val` and for them all to be coercible to a common `Val` type.

<a id="-"></a><a id="---Val"></a><a id="+"></a><a id="+--Val--etc"></a><a id="+--Val--Val"></a><a id="---Val--etc"></a><a id="---Val--Val"></a>
> **\'-\'** (v :: *Val*)
> 
> **\'+\'** (v :: *Val*, w :: *Val*)
> 
> **\'-\'** (v :: *Val*, w :: *Val*)
> 
> -> *Val*
> {:.ret}
{:.intrinsic}

Negation, addition and subtraction.

This is as normal for `ValFldPadExactElt`, and defined pointwise otherwise. For convenience, we define $\infty-\infty=0$.






<a id="*"></a><a id="*--Val--etc"></a><a id="*--Val--any"></a><a id="*--any--etc"></a><a id="*--any--Val"></a><a id="/"></a><a id="/--Val--etc"></a><a id="/--Val--any"></a>
> **\'\*\'** (v :: *Val*, n)
> 
> **\'\*\'** (n, v :: *Val*)
> 
> **\'/\'** (v :: *Val*, n)
> 
> -> *Val*
> {:.ret}
{:.intrinsic}

Scalar multiplication and division. `n` must be an integer or rational.






<a id="eq"></a><a id="eq--Val--etc"></a><a id="eq--Val--Val"></a><a id="ne"></a><a id="ne--Val--etc"></a><a id="ne--Val--Val"></a><a id="le"></a><a id="le--Val--etc"></a><a id="le--Val--Val"></a><a id="lt"></a><a id="lt--Val--etc"></a><a id="lt--Val--Val"></a><a id="ge"></a><a id="ge--Val--etc"></a><a id="ge--Val--Val"></a><a id="gt"></a><a id="gt--Val--etc"></a><a id="gt--Val--Val"></a>
> **\'eq\'** (v :: *Val*, w :: *Val*)
> 
> **\'ne\'** (v :: *Val*, w :: *Val*)
> 
> **\'le\'** (v :: *Val*, w :: *Val*)
> 
> **\'lt\'** (v :: *Val*, w :: *Val*)
> 
> **\'ge\'** (v :: *Val*, w :: *Val*)
> 
> **\'gt\'** (v :: *Val*, w :: *Val*)
> 
> -> *Val*
> {:.ret}
{:.intrinsic}

Ordering predicates.

This is as normal for `ValFldPadExactElt` (i.e. a total ordering), and defined pointwise otherwise (i.e. a partial ordering).












<a id="join"></a><a id="join--Val--etc"></a><a id="join--Val--Val"></a><a id="meet"></a><a id="meet--Val--etc"></a><a id="meet--Val--Val"></a>
> **\'join\'** (v :: *Val*, w :: *Val*)
> 
> **\'meet\'** (v :: *Val*, w :: *Val*)
> 
> -> *Val*
> {:.ret}
{:.intrinsic}

Supremum and infemum.

This is just maximum and minimum for `ValFldPadExactElt`, and defined pointwise otherwise.




<a id="diff"></a><a id="diff--Val--etc"></a><a id="diff--Val--Val"></a>
> **\'diff\'** (v :: *Val*, w :: *Val*)
> 
> -> *Val*
> {:.ret}
{:.intrinsic}

Diff. For `ValFldPadExactElt`, `v diff w` is defined to be `v` if `v gt w` and otherwise is negative infinity. Otherwise, it is defined pointwise.

If you view the valuation of a compound structure like a multiset, except where the multiplicities on each element are tropical integers instead of normal integers, then `diff` is like set difference defined via a universal property.


<a id="Value"></a><a id="Value--Val"></a>
> **Value** (v :: *Val*)
> 
> -> Any
> {:.ret}
{:.intrinsic}

Retrieves the value of the valuation. For `ValFldPadExactElt` this is an integer, rational or infinite. For compound structures it is the underlying function, e.g. for polynomials it is an `AssocDflt` representing a function which is constant almost everywhere.


<a id="IsValidAbsolutePrecision"></a><a id="IsValidAbsolutePrecision--any--etc"></a><a id="IsValidAbsolutePrecision--any--any"></a>
> **IsValidAbsolutePrecision** (x, v)
> 
> -> *Val*
> {:.ret}
{:.intrinsic}

True if `v` may be coerced to a valuation for `x`. If so, also returns the coerced valuation.


<a id="IsValidAbsolutePrecisionDiff"></a><a id="IsValidAbsolutePrecisionDiff--any--etc"></a><a id="IsValidAbsolutePrecisionDiff--any--any"></a>
> **IsValidAbsolutePrecisionDiff** (x, v)
> 
> -> *Val*
> {:.ret}
{:.intrinsic}

True if `v` may be coerced to a valuation for `x`. If so also returns the coerced valuation. Differs from `IsValidAbsolutePrecision` in that, for example, for polynomials, if the constant value is not implied by `v`, then it is taken to be -infinity instead of infinity.


## ValFldPadExactElt
{:#valfldpadexactelt}

Represents the valuation of a p-adic number.

### Creation
{:#creation}

<a id="ValFldPadExactElt_IsCoercible"></a><a id="ValFldPadExactElt_IsCoercible--any"></a><a id="ValFldPadExactElt_IsCoercible--ValFldPadExactElt"></a><a id="ValFldPadExactElt_IsCoercible--RngIntElt"></a><a id="ValFldPadExactElt_IsCoercible--Infty"></a><a id="ValFldPadExactElt_IsCoercible--ExtReElt"></a><a id="ValFldPadExactElt_IsCoercible--FldRatElt"></a>
> **ValFldPadExactElt_IsCoercible** (v)
> 
> **ValFldPadExactElt_IsCoercible** (v :: *ValFldPadExactElt*)
> 
> **ValFldPadExactElt_IsCoercible** (v :: *RngIntElt*)
> 
> **ValFldPadExactElt_IsCoercible** (v :: *Infty*)
> 
> **ValFldPadExactElt_IsCoercible** (v :: *ExtReElt*)
> 
> **ValFldPadExactElt_IsCoercible** (v :: *FldRatElt*)
> 
> -> *BoolElt*, Any
> {:.ret}
{:.intrinsic}

True if `v` is coercible to a ValFldPadExactElt, and the coerced value.












<a id="IsPromotable"></a><a id="IsPromotable--ValFldPadExactElt--etc"></a><a id="IsPromotable--ValFldPadExactElt--any"></a>
> **IsPromotable** (v :: *ValFldPadExactElt*, w)
> 
> -> *BoolElt*, Any, Any
> {:.ret}
{:.intrinsic}

True if `v` and `w` are promotable to a common type.


<a id="ValFldPadExactElt_Make"></a><a id="ValFldPadExactElt_Make--any"></a>
> **ValFldPadExactElt_Make** (v)
> 
> -> *ValFldPadExactElt*
> {:.ret}
{:.intrinsic}

A ValFldPadExactElt with value `v`.


### Special values
{:#special-values}

<a id="ValFldPadExactElt_Infinity"></a><a id="ValFldPadExactElt_Infinity--noargs"></a>
> **ValFldPadExactElt_Infinity** ()
> 
> -> *ValFldPadExactElt*
> {:.ret}
{:.intrinsic}

The valuation Infinity.


<a id="ValFldPadExactElt_NegInfinity"></a><a id="ValFldPadExactElt_NegInfinity--noargs"></a>
> **ValFldPadExactElt_NegInfinity** ()
> 
> -> *ValFldPadExactElt*
> {:.ret}
{:.intrinsic}

The valuation -Infinity.


<a id="ValFldPadExactElt_Zero"></a><a id="ValFldPadExactElt_Zero--noargs"></a>
> **ValFldPadExactElt_Zero** ()
> 
> -> *ValFldPadExactElt*
> {:.ret}
{:.intrinsic}

The valuation 0.


### Other operations
{:#other-operations}

<a id="IsFinite"></a><a id="IsFinite--ValFldPadExactElt"></a>
> **IsFinite** (v :: *ValFldPadExactElt*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `v` is finite, i.e. an integer or rational.


<a id="IsIntegral"></a><a id="IsIntegral--ValFldPadExactElt"></a>
> **IsIntegral** (v :: *ValFldPadExactElt*)
> 
> -> *BoolElt*, *RngIntElt*
> {:.ret}
{:.intrinsic}

True if `v` has an integer value, and the value if so.


<a id="IntegerValue"></a><a id="IntegerValue--ValFldPadExactElt"></a>
> **IntegerValue** (v :: *ValFldPadExactElt*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The value of `v` coerced to an integer.


<a id="Ceiling"></a><a id="Ceiling--ValFldPadExactElt"></a>
> **Ceiling** (v :: *ValFldPadExactElt*)
> 
> -> *ValFldPadExactElt*
> {:.ret}
{:.intrinsic}

The integer valuation larger than `v`, or just `v` if infinite.


<a id="ExactpAdics_Val"></a><a id="ExactpAdics_Val--FldPadElt"></a>
> **ExactpAdics_Val** (x :: *FldPadElt*)
> 
> -> *ValFldPadExactElt*
> {:.ret}
{:.intrinsic}

The valuation of `x`.


<a id="ExactpAdics_APr"></a><a id="ExactpAdics_APr--FldPadElt"></a>
> **ExactpAdics_APr** (x :: *FldPadElt*)
> 
> -> *ValFldPadExactElt*
> {:.ret}
{:.intrinsic}

The absolute precision of `x`.


## ValRngUPolElt_FldPadExact
{:#valrngupolelt_fldpadexact}

Represents the valuation of a univariate polynomial over a p-adic field.

### Creation
{:#creation-2}

<a id="ValRngUPolElt_FldPadExact_IsCoercible"></a><a id="ValRngUPolElt_FldPadExact_IsCoercible--any"></a><a id="ValRngUPolElt_FldPadExact_IsCoercible--ValRngUPolElt_FldPadExact"></a><a id="ValRngUPolElt_FldPadExact_IsCoercible--AssocDflt"></a>
> **ValRngUPolElt_FldPadExact_IsCoercible** (v)
> 
> **ValRngUPolElt_FldPadExact_IsCoercible** (v :: *ValRngUPolElt_FldPadExact*)
> 
> **ValRngUPolElt_FldPadExact_IsCoercible** (v :: *AssocDflt*)
> 
> -> *BoolElt*, Any
> {:.ret}
{:.intrinsic}

True if `v` is coercible to a ValRngUPolElt_FldPadExact.






<a id="IsPromotable-2"></a><a id="IsPromotable--ValRngUPolElt_FldPadExact--etc"></a><a id="IsPromotable--ValRngUPolElt_FldPadExact--any"></a>
> **IsPromotable** (v :: *ValRngUPolElt_FldPadExact*, w)
> 
> -> *BoolElt*, Any
> {:.ret}
{:.intrinsic}

True if `v` and `w` are promotable to a common type.


<a id="ValRngUPolElt_FldPadExact_IsCoercible-2"></a><a id="ValRngUPolElt_FldPadExact_IsCoercible--any--etc"></a><a id="ValRngUPolElt_FldPadExact_IsCoercible--any--any"></a><a id="ValRngUPolElt_FldPadExact_IsCoercible--ValFldPadExactElt--etc"></a><a id="ValRngUPolElt_FldPadExact_IsCoercible--ValFldPadExactElt--any"></a>
> **ValRngUPolElt_FldPadExact_IsCoercible** (dflt, v)
> 
> **ValRngUPolElt_FldPadExact_IsCoercible** (dflt :: *ValFldPadExactElt*, v)
> 
> -> *BoolElt*, Any
> {:.ret}
{:.intrinsic}

True if `v` is coercible to a ValRngUPolElt_FldPadExact with given default.




<a id="ValRngUPolElt_FldPadExact_Make"></a><a id="ValRngUPolElt_FldPadExact_Make--any"></a>
> **ValRngUPolElt_FldPadExact_Make** (v)
> 
> -> *ValRngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

A ValRngUPolElt_FldPadExact with value `v`.


<a id="ValRngUPolElt_FldPadExact_Make-2"></a><a id="ValRngUPolElt_FldPadExact_Make--any--etc"></a><a id="ValRngUPolElt_FldPadExact_Make--any--any"></a>
> **ValRngUPolElt_FldPadExact_Make** (x, y)
> 
> -> *ValRngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Same as ValRngUPolElt_FldPadExact_Make(DefaultAssociativeArray(`x`,`y`)).


<a id="ValRngUPolElt_FldPadExact_Make-3"></a><a id="ValRngUPolElt_FldPadExact_Make--any--etc-2"></a><a id="ValRngUPolElt_FldPadExact_Make--any--any--any"></a>
> **ValRngUPolElt_FldPadExact_Make** (x, y, z)
> 
> -> *ValRngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Same as ValRngUPolElt_FldPadExact_Make(DefaultAssociativeArray(`x`,`y`,`z`)).


### Special values
{:#special-values-2}

<a id="ValRngUPolElt_FldPadExact_Infinity"></a><a id="ValRngUPolElt_FldPadExact_Infinity--noargs"></a>
> **ValRngUPolElt_FldPadExact_Infinity** ()
> 
> -> *ValRngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The valuation Infinity.


<a id="ValRngUPolElt_FldPadExact_NegInfinity"></a><a id="ValRngUPolElt_FldPadExact_NegInfinity--noargs"></a>
> **ValRngUPolElt_FldPadExact_NegInfinity** ()
> 
> -> *ValRngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The valuation -Infinity.


<a id="ValRngUPolElt_FldPadExact_Zero"></a><a id="ValRngUPolElt_FldPadExact_Zero--noargs"></a>
> **ValRngUPolElt_FldPadExact_Zero** ()
> 
> -> *ValRngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The valuation 0.


### Other operations
{:#other-operations-2}

<a id="Value-2"></a><a id="Value--ValRngUPolElt_FldPadExact"></a>
> **Value** (v :: *ValRngUPolElt_FldPadExact*)
> 
> -> *AssocDflt*
> {:.ret}
{:.intrinsic}

The underlying associative array of values.


<a id="Ceiling-2"></a><a id="Ceiling--ValRngUPolElt_FldPadExact"></a>
> **Ceiling** (v :: *ValRngUPolElt_FldPadExact*)
> 
> -> *ValRngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The integer valuation larger than `v`, or just `v` if infinite.


<a id="&join"></a><a id="&join--ValRngUPolElt_FldPadExact"></a>
> **\'&join\'** (v :: *ValRngUPolElt_FldPadExact*)
> 
> -> *ValFldPadExactElt*
> {:.ret}
{:.intrinsic}

The join of the valuations at each coefficient. Equivalent to "&join Image(Value(`v`))".


<a id="&meet"></a><a id="&meet--ValRngUPolElt_FldPadExact"></a>
> **\'&meet\'** (v :: *ValRngUPolElt_FldPadExact*)
> 
> -> *ValFldPadExactElt*
> {:.ret}
{:.intrinsic}

The meet of the valuations at each coefficient. Equivalent to "&meet Image(Value(`v`))".


<a id="@"></a><a id="@--RngIntElt--etc"></a><a id="@--RngIntElt--ValRngUPolElt_FldPadExact"></a>
> **\'@\'** (i :: *RngIntElt*, v :: *ValRngUPolElt_FldPadExact*)
> 
> -> *ValFldPadExactElt*
> {:.ret}
{:.intrinsic}

The valuation of coefficient `i`.


<a id="ShiftSlope"></a><a id="ShiftSlope--ValRngUPolElt_FldPadExact--etc"></a><a id="ShiftSlope--ValRngUPolElt_FldPadExact--any"></a>
> **ShiftSlope** (v :: *ValRngUPolElt_FldPadExact*, s)
> 
> -> *ValRngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Adds i*`s` onto `v`(i).


<a id="ExactpAdics_Val-2"></a><a id="ExactpAdics_Val--RngUPolElt-FldPad"></a>
> **ExactpAdics_Val** (f :: *RngUPolElt*[*FldPad*])
> 
> -> *ValRngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The valuation of `f`.


<a id="ExactpAdics_APr-2"></a><a id="ExactpAdics_APr--RngUPolElt-FldPad"></a>
> **ExactpAdics_APr** (f :: *RngUPolElt*[*FldPad*])
> 
> -> *ValRngUPolElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The absolute precision of `f`.


