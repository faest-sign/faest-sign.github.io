---
layout: home
title: "Come and join the FAEST"
---

FAEST is a digital signature algorithm designed to be secure against quantum computers.
The security of FAEST is based on standard cryptographic hashes and ciphers, specifically [SHA3][sha3_spec] and [AES][aes_spec], which are believed to remain secure against quantum adversaries.

## Design

In FAEST, the secret signing key is an AES key, while the public verification key is a plaintext-ciphertext pair, obtained by encrypting a random message under the signing key. A signature consists of a non-interactive zero-knowledge proof of knowledge of an AES key which maps the message to the ciphertext. This follows the design principle of the [Picnic signature scheme][picnic], except using the well-analyzed AES cipher as a one-way function instead of LowMC. FAEST also uses a new zero-knowledge proof technique called VOLE-in-the-head, which improves upon the established MPC-in-the-head paradigm.

## Variants

There are several parameters controlling the instantiation of FAEST, giving differing tradoffs between security, speed, and compactness.
First there's the security parameter, which determines the overall security level of the scheme, and also affects performance.
FAEST offers 3 different security levels, corresponding roughly to AES-128, AES-192 or AES-256.

Second, we have an Even-Mansour variant, where a block cipher is used as an ideal permutation by publishing its key, run on a secret input.
This simplifies proving the key schedule in zero-knowledge, since it is public, but when the security parameter is 192 or 256 it requires using [Rijndael][rijndael-spec] with larger block sizes, as only the 128-bit block size was standardized as AES.

Third, our zero-knoweldge proof admits a communication–computation tradeoff, since it is built using [SoftSpokenVOLE][ssot].
This is controlled by a parameter *𝜏*, with communication being roughly proportional to *𝜏*.
FAEST has two settings for *𝜏* for each security level: a "**s**low and short" setting, and a "**f**ast but long" setting.

## Performance

For 128-bit security, our optimized implementation of FAEST can sign or verify in 0.9 milliseconds (for signatures of size 6.5 kilobytes) or 8.1 milliseconds (for signatures of size 5 kilobytes). When using AES in Even–Mansour mode, signature size can be further reduced to 4.6 kilobytes. Here are the benchmarks for our [AVX2 implementation](/software.html).

{% include_relative avx2-perf.md %}

## Contact

If you want to contact us, please send an email to [team@faest.info](mailto:team@faest.info).

{% include_relative references.md %}
