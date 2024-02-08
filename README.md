# sil0259-Homomorphic-Hash-Encryption [Proposal]

> **Initial Date:** 7 February 2024 | **Author:** Silene0259 (Joe T)

> Made especially for **Slinky**

## Notice

This was written in a few hours and is incomplete and needs extensive work. It will be updated. You are free to create a pull request with a seperate file/folder like so: `[username]-HHE-Usage.md` or `[username]-HHE-Pseudocode.md`. This file remains untouched and will be updated overtime. Currently, I do not have much time on my hands so apologizes this is not more in-depth.

Some of this information may be incorrect as it is still being worked on. I will be sure to add pseudocode in the future and some examples in Rust.

---

## About

A new method of homomorphically encrypting data by **adding together two hash digests homomorphically** and then being delivered to the client. It only requires **Partially Homomorphic Encryption** which is faster than other schemes as **addition** is the only thing that is required.

Requires using large primitive types like u256, u384, and u512. **Fully-Homomorphic-Encryption (FHE)** is much slower then using addition of large primitives but can be used to expand on this.


## What It Is Used For

- Privacy

- Data Integrity Checking (to see whether two nodes have the same data without revealing what the data is)

- Shorter Signatures

- Randomness Between Multiple Nodes

- Verifying a chain of trust through traversal


## Usage (Note: Needs Improvements)

### One-Time Signatures

Generating hash of Lamport Signature (or other OTS), homomorphically encrypting it, then sending to server for it to generate its own one-time signature and adding it homomorphically. Finally, it is sent to back to the client. There exists multiple use cases for this and will be extended on.

### Data Integrity Check Between Two Nodes To Check Whether They Have The Same Data Without Revealing The Hash Digest or Data

Data Integrity between two nodes can be checked between a client and server by first having the hash digest of some given data (like an image) converted to a large unsigned integer (u256) and encrypted using the clients secret key. This is then sent to the server and the server then generates a hash digest of their data (like the same image) and homomorphically adds it to the initial digest (thus the server knows its own hash digest in cleartext). This is then sent back to the client encrypted.

The client decrypts it and subtracts their original hash digest they sent to the server with the decrypted message. If the hash digest matches then they both have the same input. If it is different then they have different input data (and thus hash digests).

This simple method is powerful because the server never learns what the client has nor the hash digest unless they have matching inputs (like the same image or key).

In some ways, this can be compared to a zero-knowledge proof because the server never learns anything about the data unless it already has that data. This means it is either true or false.

### Verify Password With Server or Node

**Notice:** Currently untrusted due to security issues with TFHE but possibly useful in the future.

A client can verify a server or node knows their password without revealing it. The only knowledge the server needs to know is the hash digest of the password. The same method above can be used to check whether the password is known.

### Asymetric Keypair Verification

- Verify Asymetric Key pair (such as RSA or ED25519) by hashing public key

## Outline

### Definitions

1. Client: The client that has the initial hash digest and encrypts it using their secret key.

2. Server: The server that performs addition or multiplication on the encrypted data and can send it back to the client or to some other node for further processing/verification.

### Basic Usage

#### Step 1: Generation of Hash Digest

Client generates a **Hash Digest** (256 bits for simplicity) using a **chosen hash function** (SHA256,BLAKE2b,SHA3) with some given **input**. This input could be a keypair, signature, image, text, video, or other data. This data should be converted to an unsigned integer of u256 for addition. It is possible that a larger number like u384 may need to be used for certain functions.

#### Step 2: Generation of Client Secret Key For Homomorphic Encryption

The client then generates its own **secret key** for homomorphically encrypting the hash digest.

## Pseudocode In Python

```python

```

## Example Code Using TFHE

Assumes TFHE supports, or will support, u256/u384/u512 which is found in the [primitive-types](https://crates.io/crates/primitive-types) crate.

```rust

```

## Implementations of Homomorphic Encryption

[Rust] [Concrete](

[Rust] [TFHE-rs](https://github.com/zama-ai/tfhe-rs)
> Faster than other implementations and only allows TFHE (addition and multiplication)

## Extensions

**Zero-Knowledge Proofs (ZKPs)** can be used to **prove the preimage of the hash** in many instances and need to be expanded on. There are a multitude of instances where this can be used extensively and with power. Poseidon comes to mind when thinking about this scheme.

# Resources

[1: TFHE: Fast Fully Homomorphic Encryption
over the Torus](https://eprint.iacr.org/2018/421.pdf)

[2: HomomorphicEncryption.org](https://homomorphicencryption.org/)
