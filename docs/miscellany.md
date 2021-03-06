# Miscellany
{:#miscellany}

Bits and bobs not belonging to the main features of the package, but needed by the package and useful nonetheless.

**Contents**
* [Default associative arrays](#default-associative-arrays)
* [Promotion](#promotion)

## Default associative arrays
{:#default-associative-arrays}

The new type `AssocDflt` is an associative array with a default value. Hence it may be used to describe a function which is constant save for finitely many exceptions.

<a id="IsCoercible_DefaultAssociativeArray"></a><a id="IsCoercible_DefaultAssociativeArray--any"></a>
> **IsCoercible_DefaultAssociativeArray** (x)
> 
> -> *BoolElt*, *AssocDflt*
> {:.ret}
{:.intrinsic}

True if we can create a default associative array with default `x`.


<a id="IsCoercible_DefaultAssociativeArray-2"></a><a id="IsCoercible_DefaultAssociativeArray--any--etc"></a><a id="IsCoercible_DefaultAssociativeArray--any--any--any"></a>
> **IsCoercible_DefaultAssociativeArray** (x, keys, values)
> 
> -> *BoolElt*, *AssocDflt*
> {:.ret}
{:.intrinsic}

True if we can create a default associative array with default `x` and given `keys` and `values`.


<a id="IsCoercible_DefaultAssociativeArray-3"></a><a id="IsCoercible_DefaultAssociativeArray--any--etc-2"></a><a id="IsCoercible_DefaultAssociativeArray--any--any"></a><a id="IsCoercible_DefaultAssociativeArray--any--Assoc"></a><a id="IsCoercible_DefaultAssociativeArray--any--seq-Tup"></a>
> **IsCoercible_DefaultAssociativeArray** (x, y)
> 
> **IsCoercible_DefaultAssociativeArray** (x, y :: *Assoc*)
> 
> **IsCoercible_DefaultAssociativeArray** (x, y :: [*Tup*])
> 
> -> *BoolElt*, *AssocDflt*
> {:.ret}
{:.intrinsic}

True if we can create a default associative array with default `x` and values `y`.






<a id="DefaultAssociativeArray"></a><a id="DefaultAssociativeArray--any"></a>
> **DefaultAssociativeArray** (x)
> 
> -> *AssocDflt*
> {:.ret}
{:.intrinsic}

The default associative array with default value `x`.


<a id="DefaultAssociativeArray-2"></a><a id="DefaultAssociativeArray--any--etc"></a><a id="DefaultAssociativeArray--any--any"></a>
> **DefaultAssociativeArray** (x, ys)
> 
> -> *AssocDflt*
> {:.ret}
{:.intrinsic}

The default associative array with default value `x` and keys and values specified by `ys` (an associative array or sequence of <key,value> pairs).


<a id="DefaultAssociativeArray-3"></a><a id="DefaultAssociativeArray--any--etc-2"></a><a id="DefaultAssociativeArray--any--any--any"></a>
> **DefaultAssociativeArray** (x, keys, values)
> 
> -> *AssocDflt*
> {:.ret}
{:.intrinsic}

The default associative array with default value `x`, and given `keys` and `values`.


<a id="Print"></a><a id="Print--AssocDflt--etc"></a><a id="Print--AssocDflt--MonStgElt"></a>
> **Print** (x :: *AssocDflt*, lvl :: *MonStgElt*)
{:.intrinsic}

Print.


<a id="@"></a><a id="@--any--etc"></a><a id="@--any--AssocDflt"></a>
> **\'@\'** (i, x :: *AssocDflt*)
> 
> -> Any
> {:.ret}
{:.intrinsic}

The value at index `i` of `x`.


<a id="ApplyPointwise"></a><a id="ApplyPointwise--any--etc"></a><a id="ApplyPointwise--any--AssocDflt--AssocDflt"></a>
> **ApplyPointwise** (f, x :: *AssocDflt*, y :: *AssocDflt*)
> 
> -> *AssocDflt*
> {:.ret}
{:.intrinsic}

Applies the function `f` pointwise to values of `x` and `y`.


<a id="ApplyPointwise-2"></a><a id="ApplyPointwise--any--etc-2"></a><a id="ApplyPointwise--any--AssocDflt"></a>
> **ApplyPointwise** (f, x :: *AssocDflt*)
> 
> -> *AssocDflt*
> {:.ret}
{:.intrinsic}

Applies the function `f` pointwise to values of `x`.


<a id="Image"></a><a id="Image--AssocDflt"></a>
> **Image** (x :: *AssocDflt*)
> 
> -> {}
> {:.ret}
{:.intrinsic}

The set of possible output values.


<a id="DefaultValue"></a><a id="DefaultValue--AssocDflt"></a>
> **DefaultValue** (x :: *AssocDflt*)
> 
> -> Any
> {:.ret}
{:.intrinsic}

The default value of `x`.


<a id="SpecialAssociativeArray"></a><a id="SpecialAssociativeArray--AssocDflt"></a>
> **SpecialAssociativeArray** (x :: *AssocDflt*)
> 
> -> *Assoc*
> {:.ret}
{:.intrinsic}

The associative array of the special values of `x`.


<a id="SpecialKeys"></a><a id="SpecialKeys--AssocDflt"></a>
> **SpecialKeys** (x :: *AssocDflt*)
> 
> -> *Assoc*
> {:.ret}
{:.intrinsic}

The keys of special values of `x`.


<a id="Zip"></a><a id="Zip--seq-AssocDflt"></a>
> **Zip** (xs :: [*AssocDflt*])
> 
> -> *AssocDflt*
> {:.ret}
{:.intrinsic}

The array [i] -> [x(i) : x in `xs`]. The inputs must have compatible indices.


<a id="ZipApplyPointwise"></a><a id="ZipApplyPointwise--any--etc"></a><a id="ZipApplyPointwise--any--seq-AssocDflt"></a>
> **ZipApplyPointwise** (f, xs :: [*AssocDflt*])
> 
> -> *AssocDflt*
> {:.ret}
{:.intrinsic}

The array [i] -> `f`([x(i) : x in `xs`]). Equivalent to ApplyPointwise(`f`,Zip(`xs`)).


<a id="ForAll"></a><a id="ForAll--AssocDflt--etc"></a><a id="ForAll--AssocDflt--any"></a>
> **ForAll** (x :: *AssocDflt*, f)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `f`(`x`(i)) is true for all i.


<a id="ForAll-2"></a><a id="ForAll--AssocDflt--etc-2"></a><a id="ForAll--AssocDflt--AssocDflt--any"></a>
> **ForAll** (x :: *AssocDflt*, y :: *AssocDflt*, f)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `f`(`x`(i),`y`(i)) is true for all i.


## Promotion
{:#promotion}

A basic scheme for promoting values in different structures to a common strucure.

<a id="IsPromotable"></a><a id="IsPromotable--any--etc"></a><a id="IsPromotable--any--any"></a>
> **IsPromotable** (x, y)
> 
> -> *BoolElt*, Any, Any
> {:.ret}
{:.intrinsic}

True if `x` and `y` are promotable to the same parent.


<a id="Promote"></a><a id="Promote--any--etc"></a><a id="Promote--any--any"></a>
> **Promote** (x, y)
> 
> -> Any, Any
> {:.ret}
{:.intrinsic}

Promotes `x` and `y` to a common type.


