# Erdős–Graham #411 — historical retraction record

This repository preserves the June 9, 2026 retraction of an earlier #411 `r=2` closure argument.

The invalid route was based on `cambie_depth3_check`. That check can be true on every prime in the relevant residue class without excluding the objects required by the actual problem. Formal verification of the check therefore did not establish the intended mathematical conclusion.

## What was retracted

The retraction withdrew the closure claims built on that route, including documents and receipts labelled with terms such as

```text
CLOSED_MOD_AXIOMS
unconditionally closed
full victory
complete closure
```

The underlying issue was semantic rather than kernel-level: the formal proposition being checked was not strong enough to imply the target theorem.

The contemporaneous retraction is preserved at

[`retraction/RETRACTION-EG411-R2-2026-06-09.md`](retraction/RETRACTION-EG411-R2-2026-06-09.md).

## Archive

`archive/` contains the original research packets under their historical filenames. They are retained so the source history is inspectable rather than silently rewritten after the correction.

The useful mathematical work that survived the retraction—bridge, cascade, and omega-ladder material—belongs in the main [`erdos411`](https://github.com/jaredwilder/erdos411) repository.

## Purpose

This repository documents one specific failed proof route and its correction. It is not the current reading surface for Erdős–Graham #411.

Author: Jared Wilder. License: Apache-2.0.
