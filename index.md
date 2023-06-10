---
layout: home
title: "Come and join the FAEST"
---

FAEST is a digital signature algorithm designed to be secure against quantum computers.
The security of FAEST is based on standard cryptographic hash functions (SHA3) and the AES cipher. 

## Design philosophy

In FAEST, the secret signing key is a key of the AES block cipher. Meanwhile, the verification key of a signature is a pair of a plaintext and ciphertext (obtained by encrypting under the secret signing key). The signature is then a Non-Interactive Zero-Knowledge proof of knowledge of the AES key. This follows the design principle of the Picnic signature scheme, although using AES as a One-Way Function instead of LowMC.

The Zero-Knowledge proof system used for FAEST is based on a new design called VOLE-in-the-head, which is developed from the established MPC-in-the-head paradigm. VOLE-in-the-head allows for a faster implementation with smaller proofs than previous approaches. Since the security of the proof system itself also only relies on the security of symmetric key cryptography such as hash functions and the AES cipher, no other cryptographic hardness assumption (LWE, CSIDH, Syndrome Decoding, ...) has to be made.

## Performance

For 128 bit security, our optimized implementation of FAEST can sign or verify in 0.9 milliseconds (for signatures of size 6.5 kilobytes) or 8.1 milliseconds (for signatures of size 5 kilobytes). When using AES in Even-Mansour mode, signature size can be further reduced to 4.6 kilobytes.

## Contact

If you want to contact us, please send an e-mail to [faest.authors@gmail.com](mailto://faest.authors@gmail.com)