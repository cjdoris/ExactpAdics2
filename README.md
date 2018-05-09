# ExactpAdics2

Another [Magma](http://magma.maths.usyd.edu.au/magma) package for exact p-adic computation.

It differs from [the first implementation `ExactpAdics`](https://github.com/cjdoris/ExactpAdics) in that we do not track precision dependencies backwards. Instead, we "push" them forwards: if a computation is not to enough precision, we increase the precision of all of its inputs by some large jump and recompute.
