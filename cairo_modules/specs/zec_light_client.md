# zec_light_client — specification

## Purpose
Provide a verifiable, auditable on‑chain compact light client for Zcash shielded headers allowing Starknet contracts to trust ZEC state roots and accept proof‑based state transitions.

## High level
- Input: serialized ZEC header or compact update, plus ZK proof (if required).  
- Output: on‑chain update of `verified_head` and epoch metadata; emits events for relayers.

## Invariants
- Only append monotonic increasing block heights/timestamps.
- Reject malformed headers or proofs.
- State must be deterministic and reproducible from serialized input and proof.

## Adversary model
- Relayers may be Byzantine. Require either on‑chain proof verification or multi‑party aggregator signatures / badge‑gated relayer set.
- Consider time/confirmation delays to avoid finality reorg attacks.

## Interfaces
- verify_zec_header(header_hash: felt, serialized_ptr: felt, serialized_len: felt) -> (ok: felt)
- get_latest_verified_block() -> (block_hash: felt)

## Expected gas / cost assumptions
- Proof verification costs (verifier call) vs storing raw headers — prefer succinct proofs.
- Gas budget per verify call: document expected upper bound after verifier chosen.

## Failure modes & mitigations
- Invalid proof accepted: require emergency pause and proposer slash/quorum rollback.
- Replay / duplicate headers: ignore duplicates by height/hash.
- Stalled relayers: fallback to badge‑gated manual post.

## Test vectors
- Include deterministic header samples: `header_sample_1.bin` (good), `header_sample_bad.bin` (tampered).
- Expected results: good → verified_head changes; bad → revert/ok=0.

## Audit checklist
- Deterministic serialization; canonical ordering specified.
- Proof verifier acceptance criteria documented.
- Edge cases (reorgs, forks, timestamp drift) covered.
specs/zec_light_client.md
