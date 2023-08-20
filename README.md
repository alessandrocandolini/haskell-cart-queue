[![CI](https://github.com/alessandrocandolini/haskell-cart-queue/actions/workflows/ci.yml/badge.svg)](https://github.com/alessandrocandolini/haskell-cart-queue/actions/workflows/ci.yml) [![codecov](https://codecov.io/gh/alessandrocandolini/haskell-cart-queue/graph/badge.svg?token=DMz0c9rmYq)](https://codecov.io/gh/alessandrocandolini/haskell-cart-queue)


# haskell-cart-queue

Illustration of how to use Haskell type system and concurrency abstractions to model intriguing, non-trivial challenges that arise in connection with the "Add to bug" functionality in a e-commerce frontend, when we allow buyers to increment, decrement, edit or clear quantity in a non-blocking way (ie, optimistically update the UI first, manage in background the requests, and deliver unexpected failures to the UI later)

Ideas to explore: 
* **compactification**: minimise pending operations to execute. This is seems premature optimisation, but can be very useful: if I click "+" 24 times to add 24 items, it would be great to not slowly executing 24 network requests  
* **concurrent topic consumption**: operations for different products can happen concurrently. Operations for the same product cannot happen concurrently, as they lack commutativity property (eg, Clear and then increment is different than increment and then clear. Clear and edit are the operations that break commutativity here) 
* **acknowlegment machanism (ack/nack)**: two step process to consume from the queue, so we can fail to consume (nack) if something goes wrong, and we can redeliver the operation from the queue. downside of this approach is that we need to ensure that the consumer always calls either ack or nack exactly ones. (Linear types might help here)
* **retries**: for general purpose strategies, we can absorbe that responsibility into the queue itself, alternatively we can push that responsibility to the consumer of the queue if the logic involves inspecting the content of the operation ]

Data integrity is obviously a key requirement here (we dont want to end up with incorrect quantity for mistake) and proving this requirement is one of the main challenges

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
