---
layout: page
title: "Dishes"
subtitle: "Software"
---


## Optimized C++ Implementation

The [optimized x86-64 implementation][faest_avx_impl] uses AVX2, AES-NI, and other ISA extensions.

We measured the performance using a single core of a workstation running a AMD Zen 3 Ryzen 9 5950X
processor at 3.4 GHz (with clock boosting disabled) and 128 GiB memory. The system was otherwise
idle (load average 0.01), so while Simultaneous Multi-Threading was enabled it likely did not affect
the results significantly. Each individual test can be run with memory usage below 19 MiB.  The
computer was running Linux 6.6.40, and the implementations were built with GCC 14.1.1.

{% include_relative avx2-perf.md %}

## Reference C Implementation

The [reference implementation][faest_ref_impl] is slower than the optimized implementation above,
but follows the algorithms given in the specification more closely.


## Old Implementations

- [x86-64 C implementation][faest_avx_impl_v1] with AVX2, AES-NI, and other ISA extensions for the NIST Round 1 submission.
  Superceded by the C++ version above.

- [Initial Rust implementation][vith_crypto_impl] for our Crypto 2023 [paper][vith_crypto].
  Note that this is for an older version of our protocol, which uses different primitives and is incompatible with the specification.

{% include_relative references.md %}
