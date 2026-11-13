# OEIS A097160: certified terms a(7)–a(12)

<!-- oeis-status:begin -->
**OEIS status** (lab registry, 14 Nov 2026):

- [A097160](https://oeis.org/A097160), a(7)-a(12) of the greatest prime with exactly n consecutive quadratic residues: **proposed** (2026-11-13: gap closed: guide full rescan of a(11) identical to the certificate). Certificate: complete.

Rules and the full registry: [athanor-oeis](https://github.com/iwasborninbali/athanor-oeis/blob/main/REGISTRY.md).
<!-- oeis-status:end -->

[A097160](https://oeis.org/A097160): a(n) is the greatest prime p such that there are n, but not n+1, consecutive
quadratic residues mod p (the longest run of consecutive nonzero quadratic residues in 1, …, p−1 has length exactly n).

This repository holds everything behind the terms a(7)–a(12): the method, the programs, the certificates and the logs
of two independent full computations. It concerns this sequence only.

| n | a(n) | Status |
|---|---|---|
| 1–6 | 5, 17, 53, 193, 457, 2153 | already in the OEIS; a(6) reproduced here |
| 7 | 4481 | certified (`a7-proof/`), independently audited (`a7-audit/`) |
| 8 | 9857 | certified; two independent full scans |
| 9 | 25793 | certified; two independent full scans |
| 10 | 60961 | certified; two independent full scans (and a third program) |
| 11 | 132113 | certified; two independent full scans |
| 12 | 324673 | certified; two independent full scans (the second finished 12 Nov 2026) |

## Method

Let k = n + 1 and let N_k(p) be the number of x in F_p such that x, x+1, …, x+k−1 are all nonzero quadratic residues.
Weil's bound for character sums of squarefree polynomials gives

  N_k(p) ≥ (p − B_k·√p − C_k) / 2^k,  B_k = (k−2)·2^(k−1) + 1,  C_k = k·2^(k−1),

which is positive for every p ≥ M_k², with M_k = 775, 1795, 4099, 9219, 20483, 45059 for k = 8, …, 13
(`terms-a8-a12/cutoffs.json`; the full derivation is in `a7-proof/result.md`). Every prime above the cutoff therefore has a
run of length k, so a complete scan of the primes below M_k² **determines** a(n); it does not only check a candidate.

## Contents

| Path | What |
|---|---|
| [`a7-proof/`](a7-proof/) | the cutoff derivation (`result.md`) and the certificate system that proves a(7) = 4481 and reproduces a(6) = 2153 |
| [`a7-audit/`](a7-audit/) | an independent audit of the a(7) proof, with its own scanner (`independent_scan.c`) and the endpoint witnesses |
| [`terms-a8-a12/`](terms-a8-a12/) | the primary scanner (`scan.c`), the independent checker (`independent.c`), the Guide's separately written full rescans (`guide_check_qrrun*.c`), certificates `certificates/aN.tsv` (every exceptional prime with its longest run), logs |

Reproduce, for example, a(8) completely (any C compiler, no libraries):

```sh
cd terms-a8-a12
gcc -O3 -std=c11 -Wall -Wextra scan.c -o scan
gcc -O3 -std=c11 -Wall -Wextra independent.c -o independent
./independent 9 3222025 full certificates/a8.tsv logs/check-a8.json certificates/sample-a8.tsv
```

The certificate for a(12) lists all 2,760 primes below 2,030,313,481 whose longest run is shorter than 13, with their longest
runs; the second full rescan (`logs/guide-check-a12.json`) produced exactly the same list.

## History and related work

- The terms 4481, 9857, 25793, 60961, 132113, 324673 were proposed by Don Reble in 2014 as the "most likely continuation"
  ([his notes](https://oeis.org/A097160/a097160.txt)); in 2015 a(7) and a(8) were removed from the entry as unproved,
  and two older values of a(9), a(10) (17041, 23473) as wrong.
- D. A. Buell and R. H. Hudson, *On runs of consecutive quadratic residues and quadratic nonresidues*, BIT 24 (1984),
  243–247, proved via Weil and Burgess that every prime p ≥ 414463 has 9 consecutive residues and computed the longest runs
  for all primes below 420000; that determines a(1)–a(8). Their follow-up (IJMMS 9 (1986), 261–266) says the last exceptional
  primes they found for m ≤ 8 are ≡ 1 (mod 4). We could not see their tables. a(9)–a(12) lie beyond their bound.

## Author, archive, licence

Aleksei Kudriashov (ORCID 0009-0006-8885-5338), Athanor lab, with AI assistance (OpenAI Codex cores; Claude Code as the
lab's guide). Archived as part of Zenodo [10.5281/zenodo.24163515](https://doi.org/10.5281/zenodo.24163515)
(athanor-number-theory v1.1, which also contains unrelated material). Code: MIT; data and text: CC BY 4.0 (see `LICENSE.md`).

[Verification certificate](CERTIFICATE.md) and [prior-art record](PRIOR-ART.md).
