# Governance and confidence policy

## Status vocabulary

- `draft`: incomplete or awaiting review.
- `verified`: sources and automated checks passed.
- `approved`: an accountable human accepted the artifact for its stated use.
- `deprecated`: retained for traceability but not valid for new decisions.

## Source precedence

When sources conflict, use this order for the claim being made:

1. Current law, regulation, regulator order or official government record
2. Homologation/certification record and signed manufacturer filing
3. Manufacturer owner manual, safety report or release note
4. Independently reproducible test evidence
5. Curated dataset with a clear license and collection protocol
6. Peer-reviewed research
7. Reputable secondary reporting
8. Marketing, aggregator or community material

Higher precedence does not guarantee broader applicability. Every source must
also match the date, geography, model/configuration, software version and ODD.

## Confidence classes

| Class | Range | Meaning |
|---|---:|---|
| C0 | 0-49% | Insufficient basis; do not act |
| C1 | 50-79% | Preliminary analytical indication |
| C2 | 80-94% | Supported, but material uncertainty remains |
| C3 | 95-98% | Strong, corroborated and scope-bounded evidence |
| C4 | 99% | Exceptional: all 99% gates pass |

Never output 100% for an empirical safety, legal, performance or future-state
claim.

## Mandatory gates for 99%

All gates must pass:

1. The claim is narrow, testable and explicitly scoped.
2. At least one current primary source directly supports the claim.
3. At least one independent corroborating source or independent verification
   supports it, unless it is a simple quotation of an authoritative record.
4. Sources agree on all material facts.
5. Manufacturer, model/configuration, software version, ODD, jurisdiction and
   as-of date are known or demonstrably irrelevant.
6. Applicable automated validation and regression tests pass.
7. No unresolved high-severity risk affects the conclusion.
8. Remaining uncertainty is immaterial to the narrow claim.
9. A human approver signs safety-critical, legal or deployment conclusions.

If a gate fails, cap confidence below 99 and explain why.

## Rule resolution

Rules are resolved at query time in this order:

1. Authorized person controlling traffic
2. Temporary traffic control and active incident restrictions
3. Traffic signals
4. Regulatory signs and road markings
5. Jurisdiction statute/regulation
6. Municipal or road-authority by-law
7. Core safety policy

This ordering is a configurable reasoning policy, not a universal statement of
law. The Driving Rules Agent must verify the controlling jurisdiction and the
applicable legal hierarchy.

## Change control

Every material artifact requires an owner, version, status, last-reviewed date,
source lineage and change note. A change to laws, software, sensors, dynamics,
ODD, calculation parameters or confidence policy invalidates dependent evidence
until impact analysis is complete.

## Human authority

Agents may summarize evidence, calculate metrics and recommend action. They may
not autonomously:

- certify a vehicle or ADS;
- approve deployment or expansion of an ODD;
- provide a final legal interpretation;
- suppress a safety event;
- modify vehicle control software; or
- operate steering, propulsion or braking.
