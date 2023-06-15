---
layout: page
title: "Ingredients"
subtitle: "Components"
---

Ingredients for the FAEST:

1. [AES Block Cipher][aes_spec]

	To build the FAEST, we use a One-way function *f* whose output *y=f(x)* on input *x* will serve as the public verification key, while *x* plays the role of the secret signing key. In FAEST-128, one can think of the function *f* the AES-128 block cipher where the key is *x*, while *y* is a plaintext-ciphertext pair *m,c* where the plaintext is encrypted under key *x* (it technically is only a OWF if the plaintext *m* is fixed in advance). For FAEST-192 and FAEST-256 two plaintext/ciphertext pairs for the **same** key are instead used, since AES only encrypts a block of 128 bits also for larger key lengths. A signature is a Zero-Knowledge  (ZK) proof, demonstrating knowledge of the key *x*.

	Using AES as the OWF has been done in previous signature candidates such as [BBQ](https://eprint.iacr.org/2019/781.pdf), [Banquet](https://eprint.iacr.org/2021/068.pdf) and [Limbo](https://eprint.iacr.org/2021/215). Similar to BBQ and follow-ups, FAEST exploits that the only non-linear operation of the AES cipher is the S-Box, which is an inversion over a small field (and can be efficiently proven in ZK). Similar to BBQ and Banquet, FAEST requires that the input of each S-box during key scheduling and encryption is non-zero, a requirement whose security impact has been analyzed in BBQ.

	FAEST can additionally use the Even-Mansour version of AES, where the key of the AES permutation is fixed in advance (to make it an ideal permutation). Then, FAEST-EM proves that it knows a key *x* such that *x XOR m*, encrypted using AES with a fixed publicly known key, yields output *c xor m*. The advantage of FAEST-EM is that the key expansion S-Boxes must not be proven in ZK since their inputs and outputs are public information. This reduces the proof and therefore signature size. For 192 and 256 bit security, FAEST-EM relies on Rijndael-192 and Rijndael-256 due to constrains of AES.

2. [QuickSilver ZK Proof][quicksilver]

	As concrete ZK proof system, FAEST uses [QuickSilver](https://eprint.iacr.org/2021/076). QuickSilver has the advantage that the concrete proof, while linear in the circuit size of AES (proportional to the number of S-Boxes), requires very low concrete communication. Moreover, the computation necessary to generate or verify the proof is very lightweight. QuickSilver requires random Vector Oblivious Linear Evaluation (VOLE) correlations between the prover and the verifier as setup. FAEST uses the observation that the proof remains sound if the prover learns the verifier's share of the VOLE correlation after it sent all QuickSilver proof messages.

3. [VOLE-in-the-Head][vith_crypto]

	<p>
	<img src="/assets/vith.png" alt="A vole in the head of a person" style="float:right;width:20%;">
	QuickSilver (and other VOLE-based ZK proof systems) use an LPN-based preprocessing stage to generate the VOLE correlations between prover and verifier in a preprocessing phase. Unfortunately, it is currently not known how to instantiate these VOLE correlation generators based on LPN such that the prover's share of the VOLE correlations can be generated without a secret state of the verifier. FAEST differs from previous works by using a protocol from the [SoftSpokenVOLE](https://eprint.iacr.org/2022/192) to generate VOLE correlations. SoftSpokenVOLE achieves this using Random Oblivious Transfers (ROTs) as starting point, and FAEST  modifies it such that the generated VOLE correlations have parameters for which the QuickSilver ZK proof has good soundness. Since the resulting proof system bears resemblance with MPC-in-the-Head, we call this approach VOLE-in-the-Head.
	</p> 

4. A pinch of salt

	Until this point, the verifier still keeps a secret state - namely its choice bits to the Oblivious Transfers. Therefore, FAEST replaces the ROTs in SoftSpokenVOLE with [hash-based commitments](https://eprint.iacr.org/2018/983) and applies the Fiat-Shamir transform to turn the ZK proof into a signature scheme. This use of hash-based commitments instead of ROT reveals the verifier's share of the VOLE correlation to the prover when commitments are chosen to be opened. Since at this point all QuickSilver proof messages have been sent this does not affect security. 

{% include_relative references.md %}
