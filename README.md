# mining-docs

Self-contained HTML reference documents on hashing and Monero mining. Each file is a single
page with no build step, no dependencies and no network calls — open it in a browser, or
double-click it from disk. They work offline.

## Documents

### `mining-a-monero-block.html`

What must occur for an XMR block to be mined, in nine stages: a synced node, the block
template, the coinbase transaction, the ~76-byte hashing blob, RandomX dataset
initialisation, the hash loop, the target comparison, network validation, and the
propagation race. Closes with a comparison of traditional pools and P2Pool.

Four stages carry deeper annexes:

| Annex | Covers |
|---|---|
| 02 | The pre-2022 emission curve, the 0.6 XMR tail, the quadratic block-weight penalty (with the curve plotted), the short/long-term median composite, and why weight ≠ size |
| 05 | The RandomX virtual machine: register file, three-tier scratchpad, the 256-instruction frequency table and what each class forces hardware to have, and the tuning consequences |
| 06 | The 720-block / 60-cut retargeting algorithm, the timewarp defence, and the exponential variance a solo miner actually faces |
| 07 | CLSAG, gamma-distributed decoy selection, key images, Pedersen commitments and Bulletproofs+ — and what a validating node never learns |

Five diagrams are hand-authored inline SVG. Throughout, **ember marks proof of work** (the
expensive half, run billions of times by one machine) and **teal marks verification** (the
cheap half, run once by every machine). That asymmetry is the document's argument.

### `hash-audit-bench.html`

Every arithmetic step of a cryptographic hash, computed live in the browser and laid out to
be checked by hand. No crypto library and no `crypto.subtle` — SHA-256 and Keccak are
written out in the file. Two tabs: Bitcoin SHA-256d and Monero Keccak-256, plus a diagrammed
(not computed) RandomX pipeline, which the page states plainly.

## Verification

The hash implementations in `hash-audit-bench.html` were extracted and run against
independent test vectors — **9/9 pass**:

- SHA-256 for the empty string, `abc`, the 448-bit multi-block case, and the one-million-`a`
  NIST vector
- Keccak-256 with `0x01` padding (Monero) and `0x06` padding (NIST SHA-3), empty and `abc`
- The real Bitcoin block 125552 header hashing to its published block hash

Both pages have been rendered and visually reviewed in light and dark themes and at 400px
width. The canvas-driven regions of `hash-audit-bench.html` remain unreviewed, because the
renderer used does not execute JavaScript.

## Notes

Both pages follow the viewer's light/dark preference. Wide diagrams and tables scroll
horizontally on narrow screens rather than shrinking to illegibility.
