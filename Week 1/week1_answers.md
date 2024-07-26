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
hashOutput = 4267533774488295900887461483015112262021273608761099826938271132511348470966

### Symmetric vs Asymmetric Encryption (AES, RSA)

What is the primary difference between symmetric and asymmetric encryption?

Key Difference: The Symmetric Encryption uses the same key to encrypt and decrypt data while the Asymmetric Encryption uses a private and a public key to encrypt and decrypt.

Can you briefly explain how AES (Advanced Encryption Standard) works?

Originally known as Rjindael standard, it's a encryption standard made by the USA Government in which the cipher arranges data in a 4x4 grid in which uses substitution, permutation and key addition. It has a block size of 128 bits, but can have different key lenghts as AES-128, AES-192, AES-256. 

What makes RSA a popular choice for public-key encryption? 

It's a secure encryption since it uses a mathematical difficult process of factoring large prime numbers, using two different but linked keys by Asymmetric encryption. It can be easy to compute in one direction but difficult to compute in reverse.

### Hash Functions, Merkle Trees

What is a hash function and what are its primary uses in cryptography?

Hashing function process it to take an input and return a fixed-size string of bytes, it's irreversible so you can't use the hash value to retrieve the original data. SHA-256 and Poseidon are popular cryptographic hash functions.

How does the SHA-256 hashing algorithm function, in simple terms?

Is a cryptographic algorithm where the input data is processed through a mathematical function, resulting in a distinct output hash. It generates a fixed-size 256-bit (32 byte) hash. This algorithm divides the input into blocks of 512 bits, each processed in 64 rounds of operations.

What is the Poseidon hash function and why is it particularly useful in ZKPs?

It's a hash function based in the Hades Strategy [GLR+20], a mixture of full nonlinear and partial nonlinear rounds, made with a sponge hash construction. It's less expensice and are designed to be very efficent as algebraic circuits.

### Merkle Tree

Can you describe the structure of a Merkle tree?

It's a regular binary tree, leafs store hashes of chunks of data and applies a hash function to the right and left leafs then applies it to the parent node ending with a root hash.

How are Merkle trees used within the blockchain context?

A blockchain can potentially have thousands of blocks with thousands of transactions in each block. Memory space and computing power are two challenges, so it would be optimal to use as little data as possible for veryfing transactions. Merkle trees can reduce CPU processing and prove better security.

Why are Merkle trees useful for efficient and secure verification of large data structures?

It makes possible to simplify information when searching specific data inside a hash root, it searches specific nodes instead of large chunks of data or the full hash root.