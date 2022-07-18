# Runtime Architecture

The runtime is divided into modules of discrete units of logic. This allows
for clean engineering of modules with a single responsibility and clearly
defined interfaces.  Each module defines its own storage, routines and
entry points. The L2 relay chain and L3 rollup chains have different runtime
logic.

The relay chain runtime logic contains the following modules related to
validating and proving L3 rollup blocks and message passing:

- Initializer: manage initialization order of the other modules.
- Shared: manages shared storage and configurations for other modules.
- Configuration: manage configuration and configuration updates in a non-racy
manner.
- Paras: manage chain-head, validity proofs, state roots, state updates and
validation code for parachains and parathreads.
- Scheduler: manages parachain and parathread scheduling as well as validator
assignments.
- Inclusion: handles the inclusion and availability of scheduled parachains and
parathreads.
- Validity: handles secondary checks and dispute resolution for included,
available parachain blocks.
- HRMP: handles horizontal messages between paras.
- UMP: Handles upward messages from a para to the relay chain.
- DMP: Handles downward messages from the relay chain to the para.
- ZKVM: execute and prove transactions on the zkvm - used for L2 zkvm

The L3 runtime contains the following modules related to rollup block
construction and proving:

- ZKVM: execute and prove transactions on the zkvm
- Talisman: exposes API for proof generation
- HRMP: handles horizontal messages between paras.
- UMP: Handles upward messages from a para to the relay chain.
- DMP: Handles downward messages from the relay chain to the para.
