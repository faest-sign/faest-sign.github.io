---
layout: page
title: "Dishes"
subtitle: "Software"
---

## C

The benchmark numbers below were collected on a consumer notebook with an AMD Ryzen 7 5800H processor, with a base clock speed of 3.2 GHz and 16 GB memory.
Simultaneous Multi-Threading and Precision Boost were enabled.
The computer was running Linux 6.1.30, and the implementations were compiled with GCC 12.2.1.

Reference [implementation][faest_ref_impl]:

{% include_relative ref-perf.html %}

x86-64 [implementation][faest_avx_impl] with AVX2, AES-NI, and other ISA extensions:

{% include_relative avx2-perf.html %}

## Rust

- [Implementation][vith_crypto_impl] for our Crypto 2023 [paper][vith_crypto].
  Note that this is for an older version of our protocol, which uses different primitives and is incompatible with the specification.

{% include_relative references.md %}
