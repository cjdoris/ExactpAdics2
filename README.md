# ExactpAdics2

Another [Magma](http://magma.maths.usyd.edu.au/magma) package for exact p-adic computation.

It differs from [the first implementation `ExactpAdics`](https://github.com/cjdoris/ExactpAdics) in that we do not track precision dependencies backwards. Instead, we "push" them forwards: if a computation is not to enough precision, we increase the precision of all of its inputs by some large jump and recompute. This has the benefits of making it much easier to code the internals, and the dependency tracking is vastly simpler. A potential downside is that some computations may be done to too much precision. In practice, this implementation is usually quicker.
