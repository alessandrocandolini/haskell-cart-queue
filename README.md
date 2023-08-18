# haskell-cart-queue

Illustration of how to use Haskell type system and concurrency abstractions to model intriguing, non-trivial challenges that arise in connection with the "Add to bug" functionality in a e-commerce frontend, when we allow buyers to increment, decrement, edit or clear quantity in a non-blocking way (ie, optimistically update the UI first, manage in background the requests, and deliver unexpected failures to the UI later) 

## How to build and run locally

The project uses the [Haskell tool stack](https://docs.haskellstack.org/en/stable/README/).

Assuming `stack` is installed in the system, the project can be build by running
```
stack build
```
To build and also run the tests, run
```
stack test
```
which is equivalent to
```
stack build --test
```
To run with test coverage
```
stack test --coverage
```
which generates a textual and HTML report.

To run the executable,
```
stack exec haskell-cart-queue-exe
```
or passing arguments
```
stack exec haskell-cart-queue-exe -- -v doctor
```

For faster feedback loop,
```
stack test --fast --file-watch
```
To run `ghci` (with a version compatible with the resolver) run
```
stack ghci
```
For more information, refer to the `stack` official docs.
