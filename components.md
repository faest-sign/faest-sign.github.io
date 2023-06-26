---
layout: page
title: "Ingredients"
subtitle: "Components"
---

Ingredients for the FAEST:

1. [AES Block Cipher][aes_spec]

	To build FAEST, we use a one-way function defined using a block cipher.
	A public verification key consists of a plaintext-ciphertext pair *(x, y)*, while the private signing key is the corresponding key *k* (together with the plaintext *x*).
	In FAEST-128, the ciphertext is defined using the AES-128 block cipher as *y = AES-128(x, k)*.
	FAEST-192 and FAEST-256 are similar, except that two plaintext/ciphertext pairs are generated for the **same** key, since AES has a block size of 128 bits even when the key is larger.
	A signature is a zero-knowledge  (ZK) proof, demonstrating knowledge of the key *k*.

	Using AES as the OWF has been done in previous signature candidates such as [BBQ][bbq], [Banquet][banquet] and [Limbo][limbo].
	Similar to BBQ and follow-ups, FAEST exploits that the only non-linear operation of the AES cipher is the S-Box, which is an inversion over a small field (and can be efficiently proven in ZK).
	To avoid dividing by zero, we require that the input of each S-box during key scheduling and encryption is non-zero.
	This restricts us to a subset of all possible keys, but the analysis in BBQ showed that this has only a very minor impact on security.

	FAEST can additionally use AES in Even-Mansour (EM) mode, where AES is used as an ideal permutation, by revealing the AES key as part of the public key.
	FAEST-EM proves that it knows a key *k* such that *k*, encrypted using AES with a fixed publicly known key *x*, yields output *k ⊕ y*.
	That is, *y = k ⊕ AES-128(k, x)*.
	The advantage of FAEST-EM is that the key expansion need not be proven in ZK since the AES key *x* is public information.
	This reduces the proof and therefore signature size.
	Using EM requires the block size to match the key size, so for 192 and 256 bit security FAEST-EM uses on Rijndael-192 and Rijndael-256, the 192 and 256 bit block size versions of Rijndael.
	(Only the 128 bit block size version of Rijndael was standardized as AES.)

2. [QuickSilver Zero-Knowledge Proof][quicksilver]

	The concrete ZK proof system in FAEST is based on [QuickSilver][quicksilver].
	QuickSilver requires a setup where a vector oblivious linear evaluation (VOLE) correlation has been distributed between the prover and the verifier, which allows the prover to homomorphically commit to its witness.
	After committing to the witness using VOLE, the prover in QuickSilver can prove arbitrary low-degree constraints about the witness, with communication complexity independent of the number of constraints.
	Moreover, the computation needed to generate or verify the proof is very lightweight.
	FAEST relies on the observation that the proof remains sound if the prover learns the verifier's portion of the VOLE correlation after the prover sent all QuickSilver proof messages.

3. [VOLE-in-the-Head][vith_crypto]

	<img src="/assets/vith.png" alt="A vole in the head of a person" style="float:right;width:20%;">
	QuickSilver (like other VOLE-based ZK proof systems) has the disadvantage of only supporting a single, designated verifier, since it requires an interactive protocol to generate the VOLE correlation, and the soundness of the proof requires the verifier's VOLE output to be secret.
	With VOLE-in-the-Head, a VOLE-like correlation can instead be generated from a public-coin protocol based on [SoftSpokenVOLE][ssot], with its base oblivious transfers replaced by [hash-based commitments][commit_extend].
	Using commitments instead of oblivious transfers requires the verifier's part of the VOLE correlation to be revealed to the prover when the commitments are later opened.
	Since this is only done after the QuickSilver proof messages have been sent, this does not affect soundness of the proof.
	The resulting, publicly verifiable proof system bears a resemblance to MPC-in-the-Head, so we call this approach VOLE-in-the-Head.

4. A pinch of salt


{% include_relative references.md %}
