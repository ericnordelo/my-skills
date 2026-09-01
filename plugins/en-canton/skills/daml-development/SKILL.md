---
name: daml-development
description: Develop, review, debug, and test Daml smart contracts for Canton Network. Use for Daml templates, choices, authorization, visibility, Daml Script, multi-party workflow patterns, project configuration, contract keys, interfaces, SDK migrations, or Daml-specific code review. Do not use for general blockchain questions unrelated to Daml.
license: Apache-2.0
---

# Daml Development

> Adapted from `canton-network-devs/CF-Daml-Skill` revision `0f75d4f7cf92eecddb5087e2bf992271802ed4b2`; this version changes the packaging, routing, review workflow, and validation guidance. See [NOTICE](NOTICE).

Help users produce Daml contracts that compile, have a valid authorization chain, preserve the intended privacy model, and are covered by meaningful tests. Ground recommendations in the user's project and target Canton/Daml versions instead of silently assuming the newest toolchain.

## Load the relevant reference

Read only the material needed for the request:

- Read [references/language.md](references/language.md) for Daml syntax, templates, choices, signatories, observers, interfaces, contract keys, standard-library operations, or Daml Script.
- Read [references/patterns.md](references/patterns.md) before designing or reviewing a multi-party workflow, authorization structure, settlement, delegation, locking, sharded state, or interface composition.
- Read [references/canton35.md](references/canton35.md) for Canton 3.5, SDK 3.5, Protocol Version 35, Daml-LF 2.3, `dpm`, contract keys, Ledger API migrations, or `daml.yaml` changes.

For code review, always read the language reference. Also read the patterns reference when the code coordinates multiple parties or financial state, and the Canton 3.5 reference when the project targets that release line.

The references are an imported technical snapshot, not a substitute for the project's source or current official documentation. If the user asks for the latest SDK, protocol behavior, command, API, or migration rule, verify it against an authoritative current source. If verification is unavailable, identify the snapshot and avoid presenting it as current fact.

## Establish the project context

Inspect available `daml.yaml`, `multi-package.yaml`, source modules, tests, DAR dependencies, and build scripts before changing code. Preserve the repository's SDK and Daml-LF targets unless the user requests a migration or the existing configuration is demonstrably inconsistent.

Clarify only details that materially change the contract model and cannot be inferred safely, such as the parties who must consent, who needs visibility, which actions consume state, and the required failure behavior. Do not invent business rules, package identifiers, interface definitions, or deployment topology.

## Design and implementation priorities

Apply these checks to every proposed workflow:

1. Identify each party and keep its roles as signatory, observer, controller, and hosting infrastructure distinct.
2. Trace the required authorizers for every create, exercise, archive, and nested consequence. Ensure the enclosing transaction supplies them.
3. Check privacy explicitly: every party that must discover or act on a contract needs an appropriate stakeholder or disclosure path.
4. Choose consuming or non-consuming choices from the intended lifecycle. Treat archive-and-recreate as a new contract with a new `ContractId`, not mutation.
5. Put structural creation invariants in `ensure` and action-specific validation in the relevant choice.
6. Make accounting and settlement invariants inspectable. For batches, verify conservation across every leg; for derived aggregates, reconcile each delta with its source-of-truth changes.
7. Prefer the smallest established workflow pattern that expresses the required consent and lifecycle. Explain why it fits before composing several patterns.
8. Keep pure calculations and record construction outside template bodies when that makes them independently testable.

Use `Optional` for absence. Keep choice names qualified when collisions are plausible. Distinguish command-building operations used by Daml Script from update operations used inside choices. Follow the project's local style when it is valid; do not impose reference examples as universal formatting rules.

## Review Daml code

Report material findings first, ordered by impact. For each finding, identify the affected code, explain the authorization, privacy, correctness, upgrade, or operability consequence, and give a precise correction. Do not rewrite correct code merely to match a preferred style.

Review at least:

- module and package configuration;
- signatories, observers, controllers, and the full authorization chain;
- contract visibility and discoverability;
- consuming behavior, stale `ContractId` assumptions, and archive-and-recreate transitions;
- `ensure` clauses and choice-level assertions;
- choice arguments and return types;
- interface and contract-key assumptions for the selected LF/PV target;
- conservation, contention, and failure atomicity where financial or aggregate state is involved;
- happy-path, authorization-boundary, invariant, expiry, and failure tests;
- production/test dependency separation and version consistency.

When no material issue is found, say so and state any validation that was not performed.

## Verify the result

Use the project's own build and test commands. Select commands from the configured SDK rather than guessing between `daml` and `dpm`. Add negative tests for unauthorized actors and invalid invariants, not only happy paths.

Never claim code compiles or tests pass unless the corresponding command completed successfully. If tools or dependencies are unavailable, provide the exact remaining verification step and distinguish reviewed code from executed code.
