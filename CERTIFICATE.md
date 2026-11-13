# Verification certificate

## Claim

- a(7) = 4481.
- a(8) = 9857.
- a(9) = 25793.
- a(10) = 60961.
- a(11) = 132113.
- a(12) = 324673.

## Evidence

| What | Repository path | Author and date | Coverage | Result | Independence / shared code or data |
|---|---|---|---|---|---|
| Producer and witness check | `a7-proof/generate.c`, `a7-proof/check.py`, `a7-proof/certificates/` | Athanor lab, AI assisted, Nov 2026; individual coder not identified | a(7), cutoff, endpoint and finite witnesses | PASS in this replay | Checker consumes producer certificates; analytic argument in `a7-proof/result.md` is human-checkable, not machine-checked |
| Independent check | `a7-audit/independent_scan.c`, `a7-audit/verify.md` | Athanor lab, Nov 2026; individual coder not identified | a(7) audit and endpoint | Audit reports agreement | Separate scanner; same mathematical target; witness data examined |
| Producer | `terms-a8-a12/scan.c`, `terms-a8-a12/certificates/`, `terms-a8-a12/vm-harvest/logs/` | Athanor lab, Nov 2026; individual coder not identified | a(8)..a(12), finite scan below cutoff | Reported endpoints agree with claims | Producer |
| Independent checks | `terms-a8-a12/independent.c`, `terms-a8-a12/vm-harvest/logs/check-a*.json`, `terms-a8-a12/guide_check_qrrun2.c`, `terms-a8-a12/logs/guide-check-a12.json` | Athanor lab; Guide's a(12) rescan completed 12 Nov 2026 | Full a(8), a(9), a(10); sampled a(11), a(12) in independent.c; separate full a(12) rescan reported | a(12) report: 2760 exceptions, endpoint 324673, matches producer | Separate code, compares with producer certificate; shared definition and cutoff |

## Replayed for this repository

Executed on 13 Nov 2026 WITA, locally. Commands use the logged working directory; logs contain the full outputs. Wall times include process startup.

- `python3 -B a7-proof/check.py` — exit 0, 0.917 s; output: PASS a(7)=4481, 48537 finite witnesses; 8 hashes pass. [`logs/certificate-2026-11-13/a7-check.log`](logs/certificate-2026-11-13/a7-check.log) (SHA-256 `b78b32d3aae25a381eccdf3bd6787ab222e9b81afdde011be37ef1f15f80f393`).
- `/tmp/c7-A097160/independent 9 3222025 full /Users/iwasborninbali/projects/science/oeis-A097160/terms-a8-a12/certificates/a8.tsv /tmp/c7-A097160/check-a8.json /tmp/c7-A097160/sample-a8.tsv` — exit 0, 6.592 s; output: full scan PASS; see the JSON result in this log folder. [`logs/certificate-2026-11-13/full-a8.log`](logs/certificate-2026-11-13/full-a8.log) (SHA-256 `8015dec569dc9089808bf960af5669a27585bbe9adbd6fcd3c7ea0a401d89aba`).
- `/tmp/c7-A097160/independent 10 16801801 full /Users/iwasborninbali/projects/science/oeis-A097160/terms-a8-a12/certificates/a9.tsv /tmp/c7-A097160/check-a9.json /tmp/c7-A097160/sample-a9.tsv` — exit 0, 62.386 s; output: full scan PASS; see the JSON result in this log folder. [`logs/certificate-2026-11-13/full-a9.log`](logs/certificate-2026-11-13/full-a9.log) (SHA-256 `5ada24126849f71d8baaba5757fce98b9e23f269a5677253772b65dba3878947`).
- `python3 -B /tmp/c7-A097160/validate.py` — exit 0, 4.358 s; output: PASS: k=2..14 on primes <1000; five corruptions rejected. [`logs/certificate-2026-11-13/validation-temporary.log`](logs/certificate-2026-11-13/validation-temporary.log) (SHA-256 `3507c521e9083c983e0515739459b87aa05f8072f1408dd385c5100d8c99b533`).
- `python3 -B terms-a8-a12/validate.py` — exit 1, 0.091 s; output: FAILED: missing compiled scan binary; see log. A successful temporary-build retry follows. [`logs/certificate-2026-11-13/validation.log`](logs/certificate-2026-11-13/validation.log) (SHA-256 `55ebd289cc5ce36b8c4daa8d75183326654cbdb843996daa56e19ee2e5d2db12`).

Temporary validation used copies of `scan.c`, `independent.c`, `validate.py` and `certificates/a8.tsv` in `/tmp/c7-A097160`; the C programs were compiled there with `cc -O3 -std=c11`. Full extension scans were not replayed because of runtime; the stored full a(12) rescan took about 30 hours.

The full-scan programs wrote their results to temporary JSON files; the captured result files are:

- [`logs/certificate-2026-11-13/check-a8.json`](logs/certificate-2026-11-13/check-a8.json) SHA-256 `647e48accbe75fec6ade1c9d02a1a542bc33ba6bd39f70977bf54d505b913d08`: `{"method":"Euler criterion with multiplicative sequential scan and odd bit sieve","mode":"full","k":9,"upper_exclusive":3222025,"prime_count":231706,"checked_count":231706,"exception_count":217,"sample_count":22,"sample_seed_hex":"a09716020261111","sample_modulus":10000,"endpoint":9857,"Euler_evaluations":35377675,"wall_seconds":6.586758,"cpu_seconds":6.535148,"status":"PASS"}`
- [`logs/certificate-2026-11-13/check-a9.json`](logs/certificate-2026-11-13/check-a9.json) SHA-256 `a42bc9bf7185d54856932db3eb92fb674ce06e0925e88f92c07328611f83811b`: `{"method":"Euler criterion with multiplicative sequential scan and odd bit sieve","mode":"full","k":10,"upper_exclusive":16801801,"prime_count":1079376,"checked_count":1079376,"exception_count":400,"sample_count":91,"sample_seed_hex":"a09716020261111","sample_modulus":10000,"endpoint":25793,"Euler_evaluations":297286716,"wall_seconds":62.380341,"cpu_seconds":62.109710,"status":"PASS"}`

- [`logs/certificate-2026-11-13/sample-a8.tsv`](logs/certificate-2026-11-13/sample-a8.tsv): SHA-256 `f78af2be5dfa77cfabab643989648bc52234077dc8b94788beb350d943b711bf`.
- [`logs/certificate-2026-11-13/sample-a9.tsv`](logs/certificate-2026-11-13/sample-a9.tsv): SHA-256 `5a1142358947ffcacf815485419bbc0cbfa6dbd6bd0583f419b9311d9dc2b657`.

## Not covered

The analytic cutoff relies on Weil’s bound and a human-readable derivation, which has not been independently proved in this replay. Full scans for a(8) and a(9) were replayed; full scans for a(10)..a(12) were not replayed due to runtime; the available `independent.c` a(11) receipt is sample-mode, despite the README claim of two full scans; the a(10) full receipt is `terms-a8-a12/vm-harvest/logs/check-a10-full.json`. The separate full a(12) rescan is a stored report; source-to-execution and complete enumeration were not re-established here. Individual coder attribution is unspecified.

## Guide's independent check

pending

## Verdict

complete (see the addendum below); earlier verdict: partial — The evidence and replay leave the gaps above, and the Guide's independent check is pending.

**Addendum, 13 November 2026 (guide).** The gap noted above for a(11) (independent check only in sample mode) is closed:
the guide's program `terms-a8-a12/guide_check_qrrun2.c` (Jacobi symbols, written separately from the producer) scanned
all 22,322,063 primes below 419,553,289 in two shards and found exactly the 1427 primes without a run of 12 consecutive
residues listed in `terms-a8-a12/certificates/a11.tsv`, with identical longest runs; the largest prime with longest run exactly 11 is
132113 (`terms-a8-a12/logs/guide-check-a11.json`). Together with the guide's earlier full rescan of a(12), every term
a(7)..a(12) now has an independent full scan.
