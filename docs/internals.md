# Internals
{:#internals}

In this section, we document the generic internal structure common to all p-adic objects.

**Contents**
* [Overview](#overview)
* [Generic intrinsics](#generic-intrinsics)
* [Overloadable intrinsics](#overloadable-intrinsics)
* [Version](#version)
* [Global ID](#global-id)
* [Warnings](#warnings)


## Overview
{:#overview}


All p-adic objects are a subtype of `AnyPadExact`, which has attributes including:
- `id`: A global id, a unique integer assigned in dependency order.
- `approximation`: A list of approximations of the object, the `n`th entry being the approximation at the `n`th "epoch".
- `dependencies`: A list of the other p-adic object on which this depends.
- `get_approximation`: A function taking a positive integer `n` (an epoch) and the list of approximations of the dependencies at this epoch, and returning an approximation at this epoch.
- `min_epoch`: The lowest epoch for which `get_approximation` should be called. For lower epochs, interpolation is used (see `InterpolateEpochs`).
- `max_epoch`: The highest epoch for which `get_approximation` should be called. For higher epochs, a precision error is raised.
- `internal_data`: Some state which may be freely modified by `get_approximation`.

There are two direct subtypes of `AnyPadExact`: `StrPadExact` representing a structure (or set), and `PadExactElt` representing an element of such a structure. For example, `FldPadExact` represents a p-adic field and is a subtype of `StrPadExact`, and its elements have type `FldPadExactElt` which is a subtype of `PadExactElt`. `PadExactElt` has an additional `parent` attribute, which must be the parent structure to which the element belongs.

## Generic intrinsics
{:#generic-intrinsics}

<a id="BringToEpoch"></a><a id="BringToEpoch--seq-AnyPadExact--etc"></a><a id="BringToEpoch--seq-AnyPadExact--RngIntElt"></a>
> **BringToEpoch** (xs :: [*AnyPadExact*], n :: *RngIntElt*)
{:.intrinsic}

Brings each `x` in `xs` to epoch `n`.


<a id="BringToEpoch-2"></a><a id="BringToEpoch--AnyPadExact--etc"></a><a id="BringToEpoch--AnyPadExact--RngIntElt"></a>
> **BringToEpoch** (x :: *AnyPadExact*, n :: *RngIntElt*)
{:.intrinsic}

Brings `x` to epoch `n`.


<a id="EpochApproximation"></a><a id="EpochApproximation--seq-AnyPadExact--etc"></a><a id="EpochApproximation--seq-AnyPadExact--RngIntElt"></a>
> **EpochApproximation** (xs :: [*AnyPadExact*], n :: *RngIntElt*)
> 
> -> []
> {:.ret}
{:.intrinsic}

Returns sequence of approximations of `xs` at epoch `n`.


<a id="EpochApproximation-2"></a><a id="EpochApproximation--AnyPadExact--etc"></a><a id="EpochApproximation--AnyPadExact--RngIntElt"></a>
> **EpochApproximation** (x :: *AnyPadExact*, n :: *RngIntElt*)
> 
> -> Any
> {:.ret}
{:.intrinsic}

The approximation of `x` at epoch `n`.


<a id="Init_AnyPadExact"></a><a id="Init_AnyPadExact--AnyPadExact"></a><a id="Init_PadExactElt"></a><a id="Init_PadExactElt--PadExactElt"></a><a id="Init"></a><a id="Init--AnyPadExact"></a><a id="Init--PadExactElt"></a>
> **Init_AnyPadExact** (x :: *AnyPadExact*)
> 
> **Init_PadExactElt** (x :: *PadExactElt*)
> 
> **Init** (x :: *AnyPadExact*)
> 
> **Init** (x :: *PadExactElt*)
{:.intrinsic}

Initializes `x`.








<a id="Parent"></a><a id="Parent--PadExactElt"></a>
> **Parent** (x :: *PadExactElt*)
> 
> -> *StrPadExact*
> {:.ret}
{:.intrinsic}

The parent of `x`.


<a id="BestApproximation"></a><a id="BestApproximation--AnyPadExact"></a>
> **BestApproximation** (x :: *AnyPadExact*)
> 
> -> Any
> {:.ret}
{:.intrinsic}

The best approximation to `x`.


<a id="ExistsEpochWith"></a><a id="ExistsEpochWith--AnyPadExact--etc"></a><a id="ExistsEpochWith--AnyPadExact--any"></a>
> **ExistsEpochWith** (x :: *AnyPadExact*, pred)
> 
> -> *BoolElt*, *RngIntElt*
> {:.ret}
{:.intrinsic}

True if there is an epoch of `x` such that `pred(x)` is true. If so, returns it.


<a id="ExistsEpochWithApproximation"></a><a id="ExistsEpochWithApproximation--AnyPadExact--etc"></a><a id="ExistsEpochWithApproximation--AnyPadExact--any"></a>
> **ExistsEpochWithApproximation** (x :: *AnyPadExact*, pred)
> 
> -> *BoolElt*, *RngIntElt*
> {:.ret}
{:.intrinsic}

True if there is an epoch of `x` such that `pred(xx)` is true, where `xx` is the corresponding approximation. If so, returns it.

**Parameters**
- `FromTop`
- `Minimize`

<a id="FirstEpochWithApproximation"></a><a id="FirstEpochWithApproximation--AnyPadExact--etc"></a><a id="FirstEpochWithApproximation--AnyPadExact--any"></a>
> **FirstEpochWithApproximation** (x :: *AnyPadExact*, pred)
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The first epoch whose approximation satisfies the predicate.

**Parameters**
- `FromTop`

<a id="IncreaseEpochUntil"></a><a id="IncreaseEpochUntil--AnyPadExact--etc"></a><a id="IncreaseEpochUntil--AnyPadExact--any"></a>
> **IncreaseEpochUntil** (x :: *AnyPadExact*, pred)
{:.intrinsic}

Increases the epoch of `x` until `pred(x)` is true.


<a id="IncreaseAbsolutePrecision"></a><a id="IncreaseAbsolutePrecision--PadExactElt--etc"></a><a id="IncreaseAbsolutePrecision--PadExactElt--any"></a>
> **IncreaseAbsolutePrecision** (x :: *PadExactElt*, apr)
{:.intrinsic}

Increases the absolute precision of `x` to at least `apr`.


<a id="Approximation"></a><a id="Approximation--PadExactElt--etc"></a><a id="Approximation--PadExactElt--any"></a>
> **Approximation** (x :: *PadExactElt*, apr)
> 
> -> Any
> {:.ret}
{:.intrinsic}

An approximation of `x` with absolute precision at least `apr`.


<a id="InterpolateUpTo"></a><a id="InterpolateUpTo--AnyPadExact--etc"></a><a id="InterpolateUpTo--AnyPadExact--RngIntElt"></a>
> **InterpolateUpTo** (x :: *AnyPadExact*, n :: *RngIntElt*)
{:.intrinsic}

Replaces the approximations of `x` below `n` with their interpolations.


<a id="InterpolateUpToFirstEpochWithApproximation"></a><a id="InterpolateUpToFirstEpochWithApproximation--AnyPadExact--etc"></a><a id="InterpolateUpToFirstEpochWithApproximation--AnyPadExact--any"></a>
> **InterpolateUpToFirstEpochWithApproximation** (x :: *AnyPadExact*, pred)
> 
> -> *RngIntElt*, *RngIntElt*
> {:.ret}
{:.intrinsic}

Replaces the approximations of `x` below n with their interpolations, where n is the first epoch whose approximation satisfies the predicate. Returns the new and old values of n.

**Parameters**
- `FromTop`

<a id="SetApproximation"></a><a id="SetApproximation--AnyPadExact--etc"></a><a id="SetApproximation--AnyPadExact--RngIntElt--any"></a>
> **SetApproximation** (x :: *AnyPadExact*, n :: *RngIntElt*, xx)
{:.intrinsic}

Sets the approximation of `x` at epoch `n` to `xx`.

This is called by [`BringToEpoch`](#BringToEpoch) and [`InterpolateUpTo`](#InterpolateUpTo).

It checks the new approximation is valid by calling [`IsValidApproximation`](#IsValidApproximation), then calls [`SetApproximationHook`](#SetApproximationHook), then calls [`InterpolateEpochs`](#InterpolateEpochs) if necessary to get missing approximations below `n`, and then finally updates the list of approximations.


## Overloadable intrinsics
{:#overloadable-intrinsics}


The following intrinsics are expected to be overloaded for type-specific behaviour.

<a id="InterpolateEpochs"></a><a id="InterpolateEpochs--AnyPadExact--etc"></a><a id="InterpolateEpochs--AnyPadExact--RngIntElt--RngIntElt--any"></a>
> **InterpolateEpochs** (x :: *AnyPadExact*, n1 :: *RngIntElt*, n2 :: *RngIntElt*, xx2)
> 
> -> *List*
> {:.ret}
{:.intrinsic}

Assuming we have an approximation for `x` at epoch `n1`, and `xx2` is the approximation at epoch `n2`, returns approximations for the intermediate epochs `[n1+1..n2-1]`. Usually this will do something simple such as just lowering the precision of `xx2` to match each intermediate epoch.


<a id="GetApproximation"></a><a id="GetApproximation--any--etc"></a><a id="GetApproximation--any--RngIntElt--List"></a>
> **GetApproximation** (get, n :: *RngIntElt*, xds :: *List*)
> 
> -> Any
> {:.ret}
{:.intrinsic}

Given a `get_approximation` value `get`, an epoch `n` and a list of approximations of dependencies at epoch `n`, returns an approximation at epoch `n`.


<a id="GetApproximation-2"></a><a id="GetApproximation--UserProgram--etc"></a><a id="GetApproximation--UserProgram--RngIntElt--List"></a>
> **GetApproximation** (get :: *UserProgram*, n :: *RngIntElt*, xds :: *List*)
> 
> -> Any
> {:.ret}
{:.intrinsic}

Currently, `get_approximation` is always just a function, and so this just calls it.


<a id="SetApproximationHook"></a><a id="SetApproximationHook--AnyPadExact--etc"></a><a id="SetApproximationHook--AnyPadExact--RngIntElt--any"></a>
> **SetApproximationHook** (x :: *AnyPadExact*, n :: *RngIntElt*, ~xx)
{:.intrinsic}

Overload this to perform some action when we are about to set the approximation of `x` at epoch `n` to `xx`.

For example, this is used by `RngUPol_FldPadExact` to ensure all its approximations have the same variable name.


<a id="IsValidApproximation"></a><a id="IsValidApproximation--AnyPadExact--etc"></a><a id="IsValidApproximation--AnyPadExact--RngIntElt--any"></a>
> **IsValidApproximation** (x :: *AnyPadExact*, n :: *RngIntElt*, xx)
> 
> -> *BoolElt*, *MonStgElt*
> {:.ret}
{:.intrinsic}

True if `xx` is a valid approximation of `x` at epoch `n`. If not, also returns an error message.


<a id="IsValidApproximation-2"></a><a id="IsValidApproximation--PadExactElt--etc"></a><a id="IsValidApproximation--PadExactElt--RngIntElt--any"></a>
> **IsValidApproximation** (x :: *PadExactElt*, n :: *RngIntElt*, xx)
> 
> -> *BoolElt*, *MonStgElt*
> {:.ret}
{:.intrinsic}

For p-adic elements, this checks that the approximation is an element of the approximation of the parent, and that it is weakly equal to the current best approximation for `x`.


## Version
{:#version}

<a id="ExactpAdics_Version"></a><a id="ExactpAdics_Version--noargs"></a>
> **ExactpAdics_Version** ()
> 
> -> *RngIntElt*, *RngIntElt*, *RngIntElt*
> {:.ret}
{:.intrinsic}

The version of the ExactpAdics package, as major, minor and patch numbers.


<a id="ExactpAdics_Implementation"></a><a id="ExactpAdics_Implementation--noargs"></a>
> **ExactpAdics_Implementation** ()
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

This returns 2, to distinguish this package from ExactpAdics, for which this returns 1.


## Global ID
{:#global-id}

Each p-adic object (`AnyPadExact`) has a unique `id` attribute, which is ordered according to dependency.

<a id="ExactpAdics_NextId"></a><a id="ExactpAdics_NextId--noargs"></a>
> **ExactpAdics_NextId** ()
> 
> -> *RngIntElt*
> {:.ret}
{:.intrinsic}

The next global id.


## Warnings
{:#warnings}

For controlling the extent to which errors and warning occur in the package.

<a id="ExactpAdics_SetWarningAction"></a><a id="ExactpAdics_SetWarningAction--MonStgElt--etc"></a><a id="ExactpAdics_SetWarningAction--MonStgElt--MonStgElt"></a>
> **ExactpAdics_SetWarningAction** (name :: *MonStgElt*, action :: *MonStgElt*)
{:.intrinsic}

Sets how the warning `name` is displayed. `action` is one of:
- `"Ignore"`: ignores the warning and does nothing
- `"Warn"`: prints the warning to the screen
- `"WarnOnce"`: prints the warning to the screen the first time it occurs
- `"Error"`: raises an error


<a id="ExactpAdics_WarningActionIsDefined"></a><a id="ExactpAdics_WarningActionIsDefined--MonStgElt"></a>
> **ExactpAdics_WarningActionIsDefined** (name :: *MonStgElt*)
> 
> -> *BoolElt*, *MonStgElt*
> {:.ret}
{:.intrinsic}

True if there is a warning action defined for warning `name`. If so, also returns the action.


<a id="ExactpAdics_GetWarningAction"></a><a id="ExactpAdics_GetWarningAction--MonStgElt--etc"></a><a id="ExactpAdics_GetWarningAction--MonStgElt--MonStgElt"></a>
> **ExactpAdics_GetWarningAction** (name :: *MonStgElt*, dflt :: *MonStgElt*)
> 
> -> *MonStgElt*
> {:.ret}
{:.intrinsic}

The warning action set for warning `name`, if set, or else `dflt`.


<a id="ExactpAdics_Warn"></a><a id="ExactpAdics_Warn--MonStgElt--etc"></a><a id="ExactpAdics_Warn--MonStgElt--any"></a>
> **ExactpAdics_Warn** (name :: *MonStgElt*, msg)
{:.intrinsic}

Raises the warning `name` with message `msg`.

**Parameters**
- `DefaultAction`
- `Action`

