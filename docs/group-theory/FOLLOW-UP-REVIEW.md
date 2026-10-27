# Follow-up group implementations

The preserved finite-table, matrix and polycyclic implementation is experimental.
Before proposing these modules for upstream inclusion, adapt them to the
permutation API and certificate contracts in PR #482.

## Required contracts

- Use nominal input/result signatures instead of the broad name-table any signatures.
- Move execution budgets to installer settings and optional options dictionaries.
  Remove limits from GroupPcSequence identity and serialization.
- Recognize input/limit errors across bundle boundaries and register explanations.
- Represent a quotient together with its verified projection. A chosen lift is
  a section and must not be advertised as a homomorphism.
- Consolidate documentation into a design contract and capability ledger.

## Finite-group algorithms

- Route Sylow, Frattini, simplicity and minimal-generator queries away from
  complete subgroup-lattice enumeration where direct algorithms apply.
  C2^7 must not fail these queries merely because it has too many subgroups.
- Avoid certifying each automorphism twice. Keep a single explicit trusted
  verification boundary and test D128 with its 2048 automorphisms under the
  default work budget.
- Make finitePermutationModel account for closure work through its caller's
  budget and normalize PermutationClosureLimitError consistently.

## Matrices and polycyclic values

- Fix double charging between matrix parent and nested child work ledgers,
  including primeFieldMatrixGroupOrder and invariant-lattice computation.
- Remove the duplicate exact-field import and unused FiniteGroupSession import.
  Express matrix powering without the lint-rejected alias of this.
- FinitePcgs.sift is a membership reduction, not a unique right-coset
  representative for arbitrary subnormal sequences. Correct the public
  contract and add the S4, H=< (1 2 3 4) > regression. Use the verified
  canonical procedure when a canonical representative is required.

## Integration

Rebase the follow-up implementations onto the merged permutation foundation;
the preserved adapter uses an older positional-budget API and certificate
contract. Keep the original TypeScript implementation independent of GAP code.
Reference: https://github.com/cortex-js/compute-engine/pull/482#issuecomment-6431051317
