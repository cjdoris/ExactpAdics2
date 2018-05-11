# Aggregates
{:#aggregates}


**Contents**
* [Tuples](#tuples)
  * [Creation of cartesian products](#creation-of-cartesian-products)
  * [Creation of tuples](#creation-of-tuples)
  * [Basic operations](#basic-operations)

## Tuples
{:#tuples}

### Creation of cartesian products
{:#creation-of-cartesian-products}

<a id="ExactpAdics_CartesianProduct"></a><a id="ExactpAdics_CartesianProduct--Tup"></a>
> **ExactpAdics_CartesianProduct** (components :: *Tup*)
> 
> -> *SetCart_PadExact*
> {:.ret}
{:.intrinsic}

The cartesian product of the `components`.


<a id="CartesianPower"></a><a id="CartesianPower--StrPadExact--etc"></a><a id="CartesianPower--StrPadExact--RngIntElt"></a>
> **CartesianPower** (S :: *StrPadExact*, n :: *RngIntElt*)
> 
> -> *SetCart_PadExact*
> {:.ret}
{:.intrinsic}

The `n`th cartesian power of `S`.


### Creation of tuples
{:#creation-of-tuples}

<a id="IsCoercible"></a><a id="IsCoercible--SetCart_PadExact--etc"></a><a id="IsCoercible--SetCart_PadExact--any"></a><a id="IsCoercible--SetCart_PadExact--Tup_PadExact"></a><a id="IsCoercible--SetCart_PadExact--Tup"></a>
> **IsCoercible** (C :: *SetCart_PadExact*, X)
> 
> **IsCoercible** (C :: *SetCart_PadExact*, X :: *Tup_PadExact*)
> 
> **IsCoercible** (C :: *SetCart_PadExact*, X :: *Tup*)
> 
> -> *BoolElt*, Any
> {:.ret}
{:.intrinsic}

We can coerce the following to an exact tuple:
- A tuple or exact tuple whose entries are coercible to the components of the cartesian product.






### Basic operations
{:#basic-operations}

<a id="NumberOfComponents"></a><a id="NumberOfComponents--SetCart_PadExact"></a>
> **NumberOfComponents** (C :: *SetCart_PadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The number of components of `C`.


<a id="@"></a><a id="@--RngIntElt--etc"></a><a id="@--RngIntElt--SetCart_PadExact"></a>
> **\'@\'** (i :: *RngIntElt*, C :: *SetCart_PadExact*)
> 
> -> *StrPadExact*
> {:.ret}
{:.intrinsic}

The `i`th component of `C`.


<a id="Components"></a><a id="Components--SetCart_PadExact"></a>
> **Components** (C :: *SetCart_PadExact*)
> 
> -> *Tup*
> {:.ret}
{:.intrinsic}

The components of `C`.


<a id="#"></a><a id="#--Tup_PadExact"></a>
> **\'#\'** (T :: *Tup_PadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The number of elements of `T`.


<a id="@-2"></a><a id="@--RngIntElt--etc-2"></a><a id="@--RngIntElt--Tup_PadExact"></a>
> **\'@\'** (i :: *RngIntElt*, T :: *Tup_PadExact*)
> 
> -> *PadExactElt*
> {:.ret}
{:.intrinsic}

The `i`th element of `T`.


<a id="ToTuple"></a><a id="ToTuple--Tup_PadExact"></a>
> **ToTuple** (T :: *Tup_PadExact*)
> 
> -> *Tup*
> {:.ret}
{:.intrinsic}

Converts `T` to a regular tuple.


<a id="ToSequence"></a><a id="ToSequence--Tup_PadExact"></a>
> **ToSequence** (T :: *Tup_PadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

Converts `T` to a sequence.


