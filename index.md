---
layout: home
title: "Come and join the FAEST"
---

FAEST is a digital signature algorithm designed to be secure against quantum computers.
The security of FAEST is based on standard cryptographic hashes and ciphers, specifically [SHA3][sha3_spec] and [AES][aes_spec], which are believed to remain secure against quantum adversaries.

## Design

In FAEST, the secret signing key is an AES key, while the public verification key is a plaintext-ciphertext pair, obtained by encrypting a random message under the signing key. A signature consists of a non-interactive zero-knowledge proof of knowledge of the AES key which maps the message to the ciphertext. This follows the design principle of the [Picnic signature scheme][picnic], except using the well-analyzed AES cipher as a one-way function instead of LowMC.

FAEST's efficiency results from a new zero-knowledge proof technique called VOLE-in-the-head, which improves upon the established MPC-in-the-head paradigm.
VOLE-in-the-head allows for a faster implementation with smaller proofs than previous approaches, while still requiring only symmetric-key primitives like SHA3 and AES.
FAEST does not need stronger cryptographic hardness assumptions like LWE, CSIDH, syndrome decoding, etc.

## Performance

For 128-bit security, our optimized implementation of FAEST can sign or verify in 0.9 milliseconds (for signatures of size 6.5 kilobytes) or 8.1 milliseconds (for signatures of size 5 kilobytes). When using AES in Even-Mansour mode, signature size can be further reduced to 4.6 kilobytes. Here are the benchmarks for our [AVX2](/software.html) implementation.

{% include_relative avx2-perf.md %}

## Contact

If you want to contact us, please send an e-mail to [faest.authors@gmail.com](mailto://faest.authors@gmail.com)

{% include_relative references.md %}
