# ZKVM

This module is responsible for executing and proving transactions associated
with the zkvm.  There are two core entry points that are exposed to be
called via extrinsics or from other runtime pallets.  These are:

```rust
pub fn create(origin: OriginFor<T>, code: Vec<u8>);

pub fn call(origin: OriginFor<T>, target: ProgramIndex, inputs: Vec<u64>, 
    num_outputs: u32);
```

- create: create a contract with the given initialisation code
- call: execute the target program with the given inputs and number of outputs.

More detail to be provided as zkvm matures.

The runtime module will expose a `prove` method such that both `create` and
`call` extrinsics can be proven.  This will be leveraged by the talisman module
which provides the logic required to prove a block.  The proving will be
performed by the the L2 relay chain via invocation of the API provide by
talisman.
