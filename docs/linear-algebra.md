# Linear algebra
{:#linear-algebra}


**Contents**
* [Creation of vector spaces](#creation-of-vector-spaces)
* [Creation of vectors](#creation-of-vectors)
  * [Coercion](#coercion)
* [Basic properties of vector spaces](#basic-properties-of-vector-spaces)
* [Vector components](#vector-components)
* [Creation of matrix spaces](#creation-of-matrix-spaces)
* [Creation of matrices](#creation-of-matrices)
  * [From coefficients](#from-coefficients)
  * [Special forms](#special-forms)
  * [Coercion](#coercion-2)
* [Basic properties of matrix spaces](#basic-properties-of-matrix-spaces)
* [Matrix components](#matrix-components)
* [Arithmetic](#arithmetic)
  * [Pointwise](#pointwise)
  * [Scalar](#scalar)
  * [Matrix](#matrix)
* [Transpose, determinant, inverse](#transpose-determinant-inverse)

## Creation of vector spaces
{:#creation-of-vector-spaces}

<a id="VectorSpace"></a><a id="VectorSpace--FldPadExact--etc"></a><a id="VectorSpace--FldPadExact--RngIntElt"></a><a id="KSpace"></a><a id="KSpace--FldPadExact--etc"></a><a id="KSpace--FldPadExact--RngIntElt"></a>
> **VectorSpace** (K :: *FldPadExact*, n :: *RngIntElt*)
> 
> **KSpace** (K :: *FldPadExact*, n :: *RngIntElt*)
> 
> -> *ModTupFld_FldPadExact*
> {:.ret}
{:.intrinsic}

The full vector space over `K` of dimension `n`.




## Creation of vectors
{:#creation-of-vectors}

### Coercion
{:#coercion}


The following can be coerced to a vector in V:
- A vector in V
- A vector whose components are coercible to the base field of V
- A sequence of vector entries, all coercible to the base field

<a id="IsCoercible"></a><a id="IsCoercible--ModTupFld_FldPadExact--etc"></a><a id="IsCoercible--ModTupFld_FldPadExact--any"></a>
> **IsCoercible** (V :: *ModTupFld_FldPadExact*, X)
> 
> -> *BoolElt*, Any
> {:.ret}
{:.intrinsic}

True if `X` is coercible to an element of `V`. If so, also returns the coerced element.


## Basic properties of vector spaces
{:#basic-properties-of-vector-spaces}

<a id="BaseField"></a><a id="BaseField--ModTupFld_FldPadExact"></a>
> **BaseField** (V :: *ModTupFld_FldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The base field of `V`.


<a id="BaseField-2"></a><a id="BaseField--ModTupFldElt_FldPadExact"></a>
> **BaseField** (v :: *ModTupFldElt_FldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The base field of `v`.


<a id="Degree"></a><a id="Degree--ModTupFld_FldPadExact"></a>
> **Degree** (V :: *ModTupFld_FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

If `V` is a subspace of `K^n`, returns `n`. That is, the number of columns in vectors in `V`.


<a id="Generic"></a><a id="Generic--ModTupFld_FldPadExact"></a>
> **Generic** (V :: *ModTupFld_FldPadExact*)
> 
> -> *ModTupFld_FldPadExact*
> {:.ret}
{:.intrinsic}

The generic vector space containing `V`.


<a id="IsGeneric"></a><a id="IsGeneric--ModTupFld_FldPadExact"></a>
> **IsGeneric** (V :: *ModTupFld_FldPadExact*)
> 
> -> *BoolElt*
> {:.ret}
{:.intrinsic}

True if `V` is generic, i.e. it was created as the full-dimensional vector space with default generators.


<a id="Dimension"></a><a id="Dimension--ModTupFld_FldPadExact"></a>
> **Dimension** (V :: *ModTupFld_FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The dimension of `V`.


<a id="Generators"></a><a id="Generators--ModTupFld_FldPadExact"></a>
> **Generators** (V :: *ModTupFld_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The generators of `V`.


## Vector components
{:#vector-components}

<a id="Nrows"></a><a id="Nrows--ModTupFldElt_FldPadExact"></a><a id="Ncols"></a><a id="Ncols--ModTupFldElt_FldPadExact"></a>
> **Nrows** (v :: *ModTupFldElt_FldPadExact*)
> 
> **Ncols** (v :: *ModTupFldElt_FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

Number of rows (always 1) and columns.




<a id="Eltseq"></a><a id="Eltseq--ModTupFldElt_FldPadExact"></a>
> **Eltseq** (v :: *ModTupFldElt_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The components of `v` as a sequence.


<a id="Component"></a><a id="Component--ModTupFldElt_FldPadExact--etc"></a><a id="Component--ModTupFldElt_FldPadExact--RngIntElt"></a><a id="@"></a><a id="@--RngIntElt--etc"></a><a id="@--RngIntElt--ModTupFldElt_FldPadExact"></a>
> **Component** (v :: *ModTupFldElt_FldPadExact*, i :: *RngIntElt*)
> 
> **\'@\'** (i :: *RngIntElt*, v :: *ModTupFldElt_FldPadExact*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

The `i`th component of `v`.




## Creation of matrix spaces
{:#creation-of-matrix-spaces}

<a id="KMatrixSpace"></a><a id="KMatrixSpace--FldPadExact--etc"></a><a id="KMatrixSpace--FldPadExact--RngIntElt--RngIntElt"></a>
> **KMatrixSpace** (K :: *FldPadExact*, m :: *RngIntElt*, n :: *RngIntElt*)
> 
> -> *ModMatFld_FldPadExact*
> {:.ret}
{:.intrinsic}

The space of `m x n` matrices over `K`.


## Creation of matrices
{:#creation-of-matrices}

### From coefficients
{:#from-coefficients}

<a id="Matrix"></a><a id="Matrix--FldPadExactElt--etc"></a><a id="Matrix--FldPadExactElt--RngIntElt--RngIntElt--any"></a>
> **Matrix** (K :: *FldPadExactElt*, nrows :: *RngIntElt*, ncols :: *RngIntElt*, cs)
> 
> -> *ModMatFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The `nrows x ncols` matrix over `K` defined by `cs`.


<a id="Matrix-2"></a><a id="Matrix--RngIntElt--etc"></a><a id="Matrix--RngIntElt--RngIntElt--seq-FldPadExactElt"></a>
> **Matrix** (nrows :: *RngIntElt*, ncols :: *RngIntElt*, cs :: [*FldPadExactElt*])
> 
> -> *ModMatFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The `nrows x ncols` matrix with coefficients `cs`.


<a id="Matrix-3"></a><a id="Matrix--seq-seq-FldPadExactElt"></a><a id="Matrix--seq-ModTupFldElt_FldPadExact"></a>
> **Matrix** (cs :: [[*FldPadExactElt*]])
> 
> **Matrix** (cs :: [*ModTupFldElt_FldPadExact*])
> 
> -> *ModMatFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The matrix whose rows are given by each entry in `cs`.




### Special forms
{:#special-forms}

<a id="Zero"></a><a id="Zero--ModMatFld_FldPadExact"></a><a id="ZeroMatrix"></a><a id="ZeroMatrix--ModMatFld_FldPadExact"></a><a id="ZeroMatrix--FldPadExact--etc"></a><a id="ZeroMatrix--FldPadExact--RngIntElt--RngIntElt"></a>
> **Zero** (M :: *ModMatFld_FldPadExact*)
> 
> **ZeroMatrix** (M :: *ModMatFld_FldPadExact*)
> 
> **ZeroMatrix** (K :: *FldPadExact*, nrows :: *RngIntElt*, ncols :: *RngIntElt*)
> 
> -> *ModMatFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The zero matrix.






<a id="Identity"></a><a id="Identity--ModMatFld_FldPadExact"></a><a id="IdentityMatrix"></a><a id="IdentityMatrix--ModMatFld_FldPadExact"></a><a id="IdentityMatrix--FldPadExact--etc"></a><a id="IdentityMatrix--FldPadExact--RngIntElt"></a>
> **Identity** (M :: *ModMatFld_FldPadExact*)
> 
> **IdentityMatrix** (M :: *ModMatFld_FldPadExact*)
> 
> **IdentityMatrix** (K :: *FldPadExact*, nrows :: *RngIntElt*)
> 
> -> *ModMatFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The identity matrix.






<a id="ScalarMatrix"></a><a id="ScalarMatrix--ModMatFld_FldPadExact--etc"></a><a id="ScalarMatrix--ModMatFld_FldPadExact--any"></a><a id="ScalarMatrix--FldPadExact--etc"></a><a id="ScalarMatrix--FldPadExact--RngIntElt--any"></a><a id="ScalarMatrix--RngIntElt--etc"></a><a id="ScalarMatrix--RngIntElt--FldPadExactElt"></a>
> **ScalarMatrix** (M :: *ModMatFld_FldPadExact*, x)
> 
> **ScalarMatrix** (K :: *FldPadExact*, nrows :: *RngIntElt*, x)
> 
> **ScalarMatrix** (nrows :: *RngIntElt*, x :: *FldPadExactElt*)
> 
> -> *ModMatFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The scalar matrix with `x` on the diagonal and zero elsewhere.






<a id="DiagonalMatrix"></a><a id="DiagonalMatrix--ModMatFld_FldPadExact--etc"></a><a id="DiagonalMatrix--ModMatFld_FldPadExact--seq"></a><a id="DiagonalMatrix--FldPadExact--etc"></a><a id="DiagonalMatrix--FldPadExact--seq"></a><a id="DiagonalMatrix--seq-FldPadExactElt"></a>
> **DiagonalMatrix** (M :: *ModMatFld_FldPadExact*, cs :: [])
> 
> **DiagonalMatrix** (K :: *FldPadExact*, cs :: [])
> 
> **DiagonalMatrix** (cs :: [*FldPadExactElt*])
> 
> -> *ModMatFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The diagonal matrix with diagonal entries given by `cs`.






### Coercion
{:#coercion-2}


The following can be coerced to a matrix in M:
- A matrix in M (or whose components are coercible to the base field)
- A sequence of sequences of components
- A sequence of row vectors
- A sequence of components

<a id="IsCoercible-2"></a><a id="IsCoercible--ModMatFld_FldPadExact--etc"></a><a id="IsCoercible--ModMatFld_FldPadExact--any"></a>
> **IsCoercible** (M :: *ModMatFld_FldPadExact*, X)
> 
> -> *BoolElt*, Any
> {:.ret}
{:.intrinsic}

True if `X` is coercible to an element of `M`. If so, also returns the coerced element.


## Basic properties of matrix spaces
{:#basic-properties-of-matrix-spaces}

<a id="BaseField-3"></a><a id="BaseField--ModMatFld_FldPadExact"></a><a id="BaseField--ModMatFldElt_FldPadExact"></a>
> **BaseField** (M :: *ModMatFld_FldPadExact*)
> 
> **BaseField** (m :: *ModMatFldElt_FldPadExact*)
> 
> -> *FldPadExact*
> {:.ret}
{:.intrinsic}

The base field.




<a id="Nrows-2"></a><a id="Nrows--ModMatFld_FldPadExact"></a><a id="Ncols-2"></a><a id="Ncols--ModMatFld_FldPadExact"></a>
> **Nrows** (M :: *ModMatFld_FldPadExact*)
> 
> **Ncols** (M :: *ModMatFld_FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

Number of rows and columns.




<a id="Degree-2"></a><a id="Degree--ModMatFld_FldPadExact"></a>
> **Degree** (M :: *ModMatFld_FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

Number of components.


<a id="Dimension-2"></a><a id="Dimension--ModMatFld_FldPadExact"></a>
> **Dimension** (M :: *ModMatFld_FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The dimension of `M`.


<a id="Generators-2"></a><a id="Generators--ModMatFld_FldPadExact"></a>
> **Generators** (M :: *ModMatFld_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The generators of `M`.


<a id="RowSpace"></a><a id="RowSpace--ModMatFld_FldPadExact"></a>
> **RowSpace** (M :: *ModMatFld_FldPadExact*)
> 
> -> *ModTupFld_FldPadExact*
> {:.ret}
{:.intrinsic}

The vector space of rows of `M`.


<a id="TransposeSpace"></a><a id="TransposeSpace--ModMatFld_FldPadExact"></a>
> **TransposeSpace** (M :: *ModMatFld_FldPadExact*)
> 
> -> *ModMatFld_FldPadExact*
> {:.ret}
{:.intrinsic}

The space of transposes of elements of `M`.


## Matrix components
{:#matrix-components}

<a id="Nrows-3"></a><a id="Nrows--ModMatFldElt_FldPadExact"></a><a id="Ncols-3"></a><a id="Ncols--ModMatFldElt_FldPadExact"></a>
> **Nrows** (m :: *ModMatFldElt_FldPadExact*)
> 
> **Ncols** (m :: *ModMatFldElt_FldPadExact*)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

Number of rows and columns.




<a id="Eltseq-2"></a><a id="Eltseq--ModMatFldElt_FldPadExact"></a>
> **Eltseq** (m :: *ModMatFldElt_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The components of `m`.


<a id="Component-2"></a><a id="Component--ModMatFldElt_FldPadExact--etc"></a><a id="Component--ModMatFldElt_FldPadExact--RngIntElt--RngIntElt"></a><a id="@-2"></a><a id="@--RngIntElt--etc-2"></a><a id="@--RngIntElt--RngIntElt--ModMatFldElt_FldPadExact"></a>
> **Component** (m :: *ModMatFldElt_FldPadExact*, i :: *RngIntElt*, j :: *RngIntElt*)
> 
> **\'@\'** (i :: *RngIntElt*, j :: *RngIntElt*, m :: *ModMatFldElt_FldPadExact*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

The `j`th component of the `i`th row of `m`.




<a id="Rows"></a><a id="Rows--ModMatFldElt_FldPadExact"></a>
> **Rows** (m :: *ModMatFldElt_FldPadExact*)
> 
> -> []
> {:.ret}
{:.intrinsic}

The rows of `m`.


<a id="Row"></a><a id="Row--ModMatFldElt_FldPadExact--etc"></a><a id="Row--ModMatFldElt_FldPadExact--RngIntElt"></a><a id="@-3"></a><a id="@--RngIntElt--etc-3"></a><a id="@--RngIntElt--ModMatFldElt_FldPadExact"></a>
> **Row** (m :: *ModMatFldElt_FldPadExact*, i :: *RngIntElt*)
> 
> -> *FldPadExactElt*
> {:.ret}
> 
> **\'@\'** (i :: *RngIntElt*, m :: *ModMatFldElt_FldPadExact*)
> 
> -> *ModTupFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

The `i`th row of `m`.




<a id="-"></a><a id="---ModMatFldElt_FldPadExact"></a><a id="+"></a><a id="+--ModMatFldElt_FldPadExact--etc"></a><a id="+--ModMatFldElt_FldPadExact--ModMatFldElt_FldPadExact"></a><a id="---ModMatFldElt_FldPadExact--etc"></a><a id="---ModMatFldElt_FldPadExact--ModMatFldElt_FldPadExact"></a><a id="&+"></a><a id="&+--seq-ModMatFldElt_FldPadExact"></a>
> **\'-\'** (m :: *ModMatFldElt_FldPadExact*)
> 
> **\'+\'** (m :: *ModMatFldElt_FldPadExact*, n :: *ModMatFldElt_FldPadExact*)
> 
> **\'-\'** (m :: *ModMatFldElt_FldPadExact*, n :: *ModMatFldElt_FldPadExact*)
> 
> **\'&+\'** (ms :: [*ModMatFldElt_FldPadExact*])
> 
> -> *ModMatFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Matrices: Negation, addition, subtraction, sum.








<a id="*"></a><a id="*--ModMatFldElt_FldPadExact--etc"></a><a id="*--ModMatFldElt_FldPadExact--FldPadExactElt"></a><a id="*--FldPadExactElt--etc"></a><a id="*--FldPadExactElt--ModMatFldElt_FldPadExact"></a><a id="/"></a><a id="/--ModMatFldElt_FldPadExact--etc"></a><a id="/--ModMatFldElt_FldPadExact--FldPadExactElt"></a>
> **\'\*\'** (m :: *ModMatFldElt_FldPadExact*, x :: *FldPadExactElt*)
> 
> **\'/\'** (m :: *ModMatFldElt_FldPadExact*, x :: *FldPadExactElt*)
> 
> -> *ModMatFldElt_FldPadExact*
> {:.ret}
> 
> **\'\*\'** (x :: *FldPadExactElt*, m :: *ModMatFldElt_FldPadExact*)
> 
> -> Any
> {:.ret}
{:.intrinsic}

Scalar multiplication and division.





**Parameters**
- `Safe`

<a id="*-2"></a><a id="*--ModTupFldElt_FldPadExact--etc"></a><a id="*--ModTupFldElt_FldPadExact--ModMatFldElt_FldPadExact"></a>
> **\'\*\'** (x :: *ModTupFldElt_FldPadExact*, y :: *ModMatFldElt_FldPadExact*)
> 
> -> *ModTupFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Vector-matrix multiplication.


<a id="*-3"></a><a id="*--ModMatFldElt_FldPadExact--etc-2"></a><a id="*--ModMatFldElt_FldPadExact--ModMatFldElt_FldPadExact"></a>
> **\'\*\'** (x :: *ModMatFldElt_FldPadExact*, y :: *ModMatFldElt_FldPadExact*)
> 
> -> *ModMatFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Matrix multiplication.


<a id="^"></a><a id="^--ModMatFldElt_FldPadExact--etc"></a><a id="^--ModMatFldElt_FldPadExact--RngIntElt"></a>
> **\'^\'** (x :: *ModMatFldElt_FldPadExact*, n :: *RngIntElt*)
> 
> -> *ModMatFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Matrix power.


## Arithmetic
{:#arithmetic}

### Pointwise
{:#pointwise}

<a id="--2"></a><a id="---ModTupFldElt_FldPadExact"></a><a id="+-2"></a><a id="+--ModTupFldElt_FldPadExact--etc"></a><a id="+--ModTupFldElt_FldPadExact--ModTupFldElt_FldPadExact"></a><a id="---ModTupFldElt_FldPadExact--etc"></a><a id="---ModTupFldElt_FldPadExact--ModTupFldElt_FldPadExact"></a><a id="&+-2"></a><a id="&+--seq-ModTupFldElt_FldPadExact"></a>
> **\'-\'** (v :: *ModTupFldElt_FldPadExact*)
> 
> **\'+\'** (v :: *ModTupFldElt_FldPadExact*, w :: *ModTupFldElt_FldPadExact*)
> 
> **\'-\'** (v :: *ModTupFldElt_FldPadExact*, w :: *ModTupFldElt_FldPadExact*)
> 
> **\'&+\'** (vs :: [*ModTupFldElt_FldPadExact*])
> 
> -> *ModTupFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Vectors: Negation, addition, subtraction, sum.








### Scalar
{:#scalar}

<a id="*-4"></a><a id="*--ModTupFldElt_FldPadExact--etc-2"></a><a id="*--ModTupFldElt_FldPadExact--FldPadExactElt"></a><a id="*--FldPadExactElt--etc-2"></a><a id="*--FldPadExactElt--ModTupFldElt_FldPadExact"></a><a id="/-2"></a><a id="/--ModTupFldElt_FldPadExact--etc"></a><a id="/--ModTupFldElt_FldPadExact--FldPadExactElt"></a>
> **\'\*\'** (v :: *ModTupFldElt_FldPadExact*, x :: *FldPadExactElt*)
> 
> **\'/\'** (v :: *ModTupFldElt_FldPadExact*, x :: *FldPadExactElt*)
> 
> -> *ModTupFldElt_FldPadExact*
> {:.ret}
> 
> **\'\*\'** (x :: *FldPadExactElt*, v :: *ModTupFldElt_FldPadExact*)
> 
> -> Any
> {:.ret}
{:.intrinsic}

Scalar multiplication and division.





**Parameters**
- `Safe`

### Matrix
{:#matrix}

<a id="InnerProduct"></a><a id="InnerProduct--ModTupFldElt_FldPadExact--etc"></a><a id="InnerProduct--ModTupFldElt_FldPadExact--ModTupFldElt_FldPadExact"></a>
> **InnerProduct** (v :: *ModTupFldElt_FldPadExact*, w :: *ModTupFldElt_FldPadExact*)
> 
> -> *ModTupFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Inner product.


<a id="Norm"></a><a id="Norm--ModTupFldElt_FldPadExact"></a>
> **Norm** (v :: *ModTupFldElt_FldPadExact*)
> 
> -> *ModTupFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Norm.


## Transpose, determinant, inverse
{:#transpose-determinant-inverse}

<a id="Transpose"></a><a id="Transpose--ModMatFldElt_FldPadExact"></a>
> **Transpose** (m :: *ModMatFldElt_FldPadExact*)
> 
> -> *ModMatFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

Transpose.


<a id="Determinant"></a><a id="Determinant--ModMatFldElt_FldPadExact"></a>
> **Determinant** (m :: *ModMatFldElt_FldPadExact*)
> 
> -> *FldPadExactElt*
> {:.ret}
{:.intrinsic}

Determinant.


<a id="IsDefinitelyInvertible"></a><a id="IsDefinitelyInvertible--ModMatFldElt_FldPadExact"></a>
> **IsDefinitelyInvertible** (m :: *ModMatFldElt_FldPadExact*)
> 
> -> *BoolElt*, *ModMatFldElt_FldPadExact*
> {:.ret}
{:.intrinsic}

True if `m` is definitely invertible. If so, also returns the inverse.

**Parameters**
- `Safe`

