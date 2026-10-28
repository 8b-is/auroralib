# Ternary Codec, Parallel Scheduler Tick & Diamond-Property Exhaustive Reducer

**Mechachleopteryx**  
*Verification Log · October 27, 2026 (`19:53:08 – 19:54:21`)*  
*Archived in `8b-is/auroralib` & `pocoo.vaked.dev/demos/book/`*

---

## 1. Chronological Verification Transcript

- **`[10/27/26, 7:53:08 PM] Mechachleopteryx`**:
  > The ternary codec is ported and mutation-tested, with stricter decoding than the original. I'm now writing the visualization mapping, using integer values and driven from real traces, then the capability graph and the parallel tick.
- **`[10/27/26, 7:53:25 PM] Mechachleopteryx`**:
  > Parallel scheduler tick is done: logs are byte-identical to the sequential tick across 150 random worlds with yields and rearms, and it passes under the race detector. Next is the capability graph and batch reducer, then the reducer shortcuts, which I'll validate against the exhaustive searches before deciding whether to keep them.
- **`[10/27/26, 7:53:38 PM] Mechachleopteryx`**:
  > The reducer shortcuts (cached structural flags, allocation-free hashing and path buffer) match the old search on 143,190 enumerated terms and 3,000 random larger ones, under every mode and strategy. I'm fixing one failing new term test and then running the full searches and the Python cross-check on the modified reducer before I call it done.
- **`[10/27/26, 7:53:51 PM] Mechachleopteryx`**:
  > The Go-to-Python cross-check on the modified reducer matches the earlier run exactly: 300 cases, no disagreements, same step counts by rule. The big searches are running in the background, and I'm adding a worker option to the sim command so the Python verifier can check logs produced by the parallel tick.
- **`[10/27/26, 7:54:21 PM] Mechachleopteryx`**:
  > The diamond-property search results on the modified reducer match the earlier record on all three term sets, with no failures and no capped terms for settled absorption with settled scope: `6,664,432`, `31,696,480` and `28,639,888` pairs, and `2,979,568`, `20,851,984` and `7,657,808` with absorption off. The known failures for the safe forms also appear as before.

---

## 2. Quantitative Verification Matrix

| Subsystem | Verification Scope | Invariant / Result |
|---|---|---|
| **Ternary Codec** | Mutation-tested with stricter decoding | Integer-only trace visualization mapping (zero floats) |
| **Parallel Scheduler Tick** | `150` random worlds with yields & rearms | Byte-identical logs to sequential tick; passes Go `-race` detector |
| **Reducer Shortcuts** | `143,190` enumerated terms + `3,000` random larger terms | Cached structural flags + allocation-free hashing & path buffer match under every mode & strategy |
| **Go-to-Python Cross-Check** | `300` differential cases + `--workers` CLI flag | `0` disagreements; identical step counts by reduction rule |
| **Diamond Property (Settled Absorption + Scope)** | `6,664,432` · `31,696,480` · `28,639,888` pairs (`67,000,800` total) | `0` failures, `0` capped terms |
| **Diamond Property (Absorption Off)** | `2,979,568` · `20,851,984` · `7,657,808` pairs (`31,489,360` total) | Exact match with reference reducer record |
