# Why 18 fails in the 547/727 prime race

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24410788.svg)](https://doi.org/10.5281/zenodo.24410788)

This result is now maintained in [theta-host-split-inert-race](https://github.com/leecrossley/theta-host-split-inert-race/tree/main/results/theta-race-factor-18). This repository is archived and keeps its releases and DOI.

From every real starting height $`1\le H\le1{,}000{,}000{,}000`$, a gain and a loss of more than $`1.9735\log2`$ both finish by $`18H`$. The sieve proves this finite statement unconditionally. Assume the generalised Riemann hypothesis (GRH) for the primitive Dirichlet $L$-functions in the 547/727 race and its base field, including the Riemann zeta function. **At arbitrarily large heights, $`18H`$ misses the loss. At other arbitrarily large heights, it misses the gain.** Even the slightly larger factor $`2e^{11/5}=18.0500\ldots`$ fails. [Theorem and proof](PROOF.md)

Each move is a doubling $`S(y)\to S(2y)`$ with $`y\gt H`$. The score measures weighted inert prime ideals minus weighted split prime ideals on the 547/727 theta-lift host, with both the width and the move fixed at two. The allowed starts lie in $`(H,CH/2]`$ when both endpoints must finish by $`CH`$. [Prime convention and weight](PROOF.md#two-statements-about-the-same-race)

## What the direct count shows

From one million through one billion, both moves actually finish by **$`7H`$**. The sieve covers norms through 32,467,011,360. It certifies the slopes at 625 integer starts. Checking the next strictly later witness at each breakpoint covers every real starting height in the range. At $`H=1{,}000{,}000{,}000`$ the two verified moves are

| Move | Start | End | Change divided by $`\log2`$ |
|---|---:|---:|---:|
| Gain | 1,016,187,975 | 2,032,375,950 | $`[33.1637,33.1639]`$ |
| Loss | 1,714,594,397 | 3,429,188,794 | $`[-2.7357,-2.7356]`$ |

The finite result uses direct prime-ideal arithmetic. [All slope enclosures](evidence/windows.tsv) · [Coverage verifier](finite.py)

## Why the pattern eventually breaks

At large heights the normalized change approaches a uniformly convergent sum over zeros. On one closed log interval of length $`2.2`$, that sum stays above $`-1.8`$ everywhere. Two computations certify the entire interval, including the point where the kernel crosses the origin. Its shape recurs arbitrarily far out. A factor of 18 gives potential doubling starts only $`\log 9=2.19722\ldots`$ units of log height, so a whole search interval can fit inside a recurring stretch with no qualifying loss. Reflection yields stretches with no qualifying gain. The index of the first numerical failure remains open. [Recurrence argument](PROOF.md#transfer-the-entire-interval) · [Verification output](evidence/check.txt)

The recurrence proof uses Alpöge's announced primitive Dirichlet GRH theorem, independently matched to its formal statement by Sutherland's checks. The local Lean lemmas take the late-translate estimate as an input. The analytic recurrence and its application to gains and losses are written out in the proof. [External verification](https://math.mit.edu/~drew/grh/) [Prior work](PRIOR-WORK.md)

The companion result proves that $`e^{175}`$ works at every height. [Fixed-factor proof](https://github.com/leecrossley/theta-race-fixed-factor/releases/tag/v1.0.1)

## Replay

Use Python 3.10 or newer inside a virtual environment and a C++17 compiler. Run

```sh
python -m pip install -r requirements.txt
python profile.py
python profile_series.py
python finite.py
c++ -std=c++17 -O3 sieve.cpp -o /tmp/theta-factor-18-sieve
python finite.py /tmp/theta-factor-18-sieve
python check_source.py
```

The first `finite.py` command checks coverage from the stored table. The second regenerates every enclosure. For the full x86-64 Linux replay with Git, curl, tar and zstd, use `bash verify-release.sh`. With Lean 4.33.1 on PATH and a built Mathlib at commit `0df444a360eaa60ab8c11dca51a86af692955474`, use `bash verify-release.sh /path/to/mathlib4`. An optional second argument supplies local copies of the five published source and audit files. The release replay also compiles the Lean implications, rechecks the module with the kernel and compares the full output against the receipt. [Lean deductions](FactorObstruction.lean) · [File hashes](SHA256SUMS)
