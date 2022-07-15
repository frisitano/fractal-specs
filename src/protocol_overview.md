# Protocol Overview

## Validity and Proving

The L2 relay chain operates an honest majority PoS BFT consensus algorithm (BABE) and finality gadget (GRANDPA).
The L3 collators propose blocks to the L2. The L2 validators validate the state transitions within L3 blocks
and attest to the blocks data availability via a reed-Solomon encoding which is distributed amongst the
validator set. Once all L3 blocks have completed validity and availability checks an L2 block containing
L3 block metadata is produced. A finality gadget is then run on the L2 chain and once a
block is considered final by the gadget the decentralised provers will begin to generate zero-knowledge
proofs attesting to the integrity of the state transitions associated with the zero-knowledge virtual
machine. This protocol achieves sharded sequencing and execution of state transitions on the L3’s and
parallel and distributed zero-knowledge proof generation via the network of decentralised provers.

## Data Availability

There are two modes in which this platform can operate – firstly in rollup mode where all transaction
data is posted to Ethereum via transaction blobs. Alternatively the platform can operate in validium
mode. As mentioned above, the platform contains a data availability sub-protocol. This can be
leveraged to provide data availability guarantees to Ethereum. This would work via BLS signature
aggregation of signatures associated with finality votes. If the validator set has marked a block as final
then we have guarantees that the block is available as per the rules of the data availability sub-protocol.
We can then combine this aggregated BLS signature with the zero-knowledge proof attesting to the
integrity of state transitions and post them to the validity bridge on Ethereum for verification. In the
validium model there is an additional honest majority trust assumption on the PoS validator set of
the L2 for data availability, however state transitions are cryptographically verifiable. This provides
superior data availability guarantees when compared to the typical trusted data availability committee
that is seen in industry. This is because the L2 validator set is permissionless and decentralised.

## L3 Block Lifecycle

Lifecycle of a L3 block:
- Block is created by an L3 collator
- Block is submitted to L2 validators
- Block is validated by L2 validators
- L3 block metadata is included in L2 block
- L2 block is finalised
- Decentralised provers generated proofs
- Proof, state delta and transaction data is submitted to ethereum