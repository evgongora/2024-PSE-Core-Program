## Circom Exercises

### Multiplication of Two numbers

```rust

pragma circom 2.1.6;

template AdditionProof() {
    // declaration of signals
    signal input a;
    signal input b;
    signal output mult;


    // constraint
    mult <== a * b;
}

component main = AdditionProof();


/* INPUT = {
    "a": 3,
    "b": 5
} */

```

### Multiplication of three numbers.

```rust

pragma circom 2.1.6;

template AdditionProof() {
    // declaration of signals
    signal input a;
    signal input b;
    signal input c;
    signal output y;
    signal output mult;

    // constraint
    y <== a * b;
    mult <== y * c;
}

component main = AdditionProof();

/* INPUT = {
    "a": 3,
    "b": 5,
    "c": 9
} */

```

### Prove input to hash

```rust
pragma circom 2.1.6;

include "circomlib/poseidon.circom";

template HashProof() {
    signal input preimage;
    signal input hash;
    signal output hashOutput;

    //constraints
    component hasher = Poseidon(1);
    hasher.inputs[0] <== preimage;
    hashOutput <== hasher.out;
    hash === hashOutput;
}

component main = HashProof();

/* INPUT = {
    "preimage": "12345",
    "hash": "4267533774488295900887461483015112262021273608761099826938271132511348470966"
} */

```