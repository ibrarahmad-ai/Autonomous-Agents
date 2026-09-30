# SOL Autonomy Agent Assurance Repository

This directory defines a manufacturer-neutral, model-neutral agent system for
autonomous-driving analysis. It is an assurance and decision-support system. It
does **not** control a vehicle and does not certify a vehicle as safe.

## Design boundary

The shared agent capabilities apply across manufacturers. Differences are kept
in versioned profiles:

- `profiles/manufacturers/` identifies organizations and authoritative sources.
- `profiles/vehicles/` records physical dimensions, dynamics, sensors and
  feature availability for a specific model/configuration/software version.
- `rules/jurisdictions/` records jurisdiction-specific traffic rules and dates.
- `catalog/calculations.json` defines formulas while profiles supply parameters.
- `catalog/sources.json` separates official, manufacturer, dataset and research
  evidence and records licensing and coverage limitations.

There is no reliable public dataset containing every worldwide vehicle's
current automated-driving capability. Coverage is therefore explicit and
auditable: unknown fields remain `null` or `unknown`; they are never inferred
from marketing language, vehicle make, or VIN metadata.

## Agents

The system contains one orchestrator and ten specialists:

1. Orchestrator
2. Source Verification
3. Perception and Sensors
4. Localization and Mapping
5. Prediction and Planning
6. Vehicle Systems and Control
7. Driving Rules
8. Safety and Validation
9. Data and ML Operations
10. Regulation and Risk
11. Business and Finance

Each `agents/<agent-id>/agent.json` is the machine-readable source of truth.
Each adjacent `agent-card.md` explains the contract to people.

## Output contract

Every substantive answer must contain:

- a narrowly stated conclusion;
- confidence and the method used to calculate it;
- supporting evidence with source, retrieval date and applicability;
- assumptions;
- remaining uncertainty;
- manufacturer/model/software/jurisdiction/as-of-date scope; and
- an escalation decision.

`99%` confidence is permitted only when all gates in `GOVERNANCE.md` pass. It
is not a stylistic setting and cannot be requested into existence.

## Repository map

```text
agents/
  schemas/                  JSON Schemas for contracts and records
  catalog/                  Agent, source, feature and calculation registries
  profiles/                 Manufacturer and vehicle profile templates
  rules/                    Core behavior policy and jurisdiction packs
  assurance/                System claims, risks and evidence expectations
  evals/                    Cross-agent acceptance cases
  tools/                    Dependency-free validation utilities
  tests/                    Repository integrity tests
  <agent-id>/
    agent.json              Machine-readable capability contract
    agent-card.md           Human-readable capability and limitations
```

JSON is used for machine-readable files because it can be validated with JSON
Schema and consumed without a YAML dependency. JSON is also valid YAML 1.2.

## Validate

From the SOL repository root:

```powershell
python agents/tools/validate_repository.py
python -m unittest discover agents/tests
```

The validator checks IDs, required contract fields, source references, output
requirements, 99%-confidence gates and profile/rule relationships. It does not
replace legal, safety or engineering review.

## Adding a vehicle

1. Copy `profiles/vehicles/_template.json`.
2. Give the record a stable ID including model year/configuration.
3. Cite each material value to an approved source ID.
4. Keep ADS/ADAS level, ODD and software version separate from base vehicle
   specifications.
5. Add calculation parameters with units and measurement conditions.
6. Run validation and the applicable agent evaluations.
7. Obtain the approvals required by the risk class.

## Adding a jurisdiction

1. Copy `rules/jurisdictions/_template.json`.
2. Record country, subdivision, road authority and effective dates.
3. Encode turns, intersections, yielding, parking, stopping, speed, vulnerable
   road users, emergency vehicles and temporary traffic controls separately.
4. Link every normative rule to current official law or regulation.
5. Preserve municipal or road-authority overrides.
6. Require qualified legal review before marking the pack `approved`.

## Standards profile

The structure is designed to support NIST AI RMF Govern/Map/Measure/Manage,
ISO/IEC 42001 governance, ISO 26262 functional-safety evidence, ISO 21448 SOTIF,
ISO 34502 scenario evaluation, OMG SACM assurance cases, JSON Schema contracts,
OpenAPI tool interfaces and ASAM OpenDRIVE/OpenSCENARIO test assets. Possessing
this repository does not itself establish conformity with any standard.
