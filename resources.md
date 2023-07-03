---
layout: page
title: "Recipes"
subtitle: "Documents"
---

### Specification

- [v1.1][spec_1_1] covers the same protocol, but fixes some issues with the document:
  - Corrected performance tables.
    They listed the same times for signature and verification due to a bug in the script; signing time was reported faster (or sometimes slower) than real timings.
  - Corrected author order on front page.
  - Corrected description and security proofs for the one-way functions.
  - Revised security estimates for the one-way functions.
- [v1.0][spec_1_0] was included in our round 1 submission to NIST.

### Submission

NIST round 1 [submission][submission_1] (29.5 MB; includes specification, source code and test vectors).

### Papers

- Our Crypto 2023 [paper][vith_crypto] on VOLE-in-the-head.

{% include_relative references.md %}
