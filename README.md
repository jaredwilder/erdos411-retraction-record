# erdos411-retraction-record

**A math program that claimed a closure, then killed its own claim, with both halves published.**

Author: Jared Wilder. First public timestamp: 2026-09-10.

## Start here

`retraction/RETRACTION-EG411-R2-2026-06-09.md`

That document is authoritative and it is the reason this repository exists. Its first line:

> **RETRACTION - "EG#411 r=2 closed" is FALSE. The problem is OPEN.**

It withdraws, by name, every prior claim in the program that Erdos-Graham #411 (r=2) was
"closed", "closed modulo an axiom", `CLOSED_MOD_AXIOMS`, or "unconditionally closed", including
a final-accounting document, a canonical-state document, a file literally called
`WIN-EG411-UNCONDITIONAL`, the receipts that claimed closure, a public research page, a
manifest card, and a memory note.

## Why the closure was false, in the retraction's own words

> The repo's `cambie_depth3_check`-based "closure" does not address the actual problem. Proving
> `cambie_depth3_check p = true` for all primes `p = 7 (mod 8)` - even with zero axioms - would
> resolve **nothing**, because the check is provably `true` at *every* prime the problem asks us
> to rule out.

And on whether this was excessive caution:

> This is not a hedge or a re-opening out of caution. It is a checkable, structural fact,
> confirmed against the primary literature and by direct computation.

A formally verified proof of a statement that is vacuously true at every relevant input. The
kernel was satisfied. The mathematics was not. That failure mode is the whole point of this
repository.

## What is in `archive/`

75 files: the research packets produced along the way, several of them named for victories that
did not happen. `ERDOS_411_R597_ABSOLUTE_KILLSHOT_PACKET.zip`,
`ERDOS_411_R599_FULL_VICTORY_PROOF_FRONTIER.zip`,
`ERDOS_411_R603_COMPLETE_CLOSURE_FORBIDDEN_SIGNATURE_BOARD.zip`.

**They are published deliberately, under their original names, with the retraction that kills
them.** Deleting them would make the record look cleaner than it was. The real result of the
411 program is the bridge, cascade and omega-ladder work, which lives at
github.com/jaredwilder/erdos411 and is unaffected by this retraction.

## Why publish this at all

Every other repository released tonight asks a stranger to trust numbers that came out of a
mostly automated pipeline. The only evidence worth anything for that trust is what happened the
time the pipeline was wrong and nobody outside would have caught it. This is that record, in
full, including the enthusiastic filenames.

Erdos-Graham #411 (r=2) is OPEN.

## License

Apache-2.0.
