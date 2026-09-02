---
layout: page
title: "Dishes"
subtitle: "Software"
---


## Optimized C++ Implementation

The [optimized architecture-specific implementation][faest_arch_opt_impl] supports x86-64 and aarch64 and uses ISA
extensions to accelerate AES and other operations.

### x86-64 (with AVX2 and AES-NI)

We measured the performance using a single core of a notebook with an Intel Core Ultra 9 285H
processor of the Arrow Lake family running Linux 7.1.9. We compile with GCC 16.2.1 and pin the
benchmark to a performance core with up to 5.4 GHz.

{% include_relative avx2-perf.md %}

### AArch64 (with AES)

For ARM, we benchmarked on a Macbook Pro with an Apple M1 processor at up to 3.2 GHz.

{% include_relative aarch64-perf.md %}

## Reference C Implementation

The [reference implementation][faest_ref_impl] is slower than the optimized implementation above,
but follows the algorithms given in the specification more closely.


## Old Implementations

- [x86-64 C implementation][faest_avx_impl_v1] with AVX2, AES-NI, and other ISA extensions for the NIST Round 1 submission.
  Superceded by the C++ version above.

- [Initial Rust implementation][vith_crypto_impl] for our Crypto 2023 [paper][vith_crypto].
  Note that this is for an older version of our protocol, which uses different primitives and is incompatible with the specification.

{% include_relative references.md %}
