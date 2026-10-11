> **Experimental. We are just trying this.** [Disclaimer](DISCLAIMER.md) · [tn-master](README.md)

# Advice to developers

These storms exist so builders can rehearse under real TN10 congestion against a high-fee AI/LLM sender: practice for mainnet, not a claim that auto-raising fees stops attackers. Live fee auto-raise (with a hard cap) is an option for dapps that must keep working during congestion; each dapp builder decides. On TN10 this proves mechanics only, not attack cost. See the [goal](WHAT-WHY-HOW.md#goal).

Testnet-10 only. Each item says what we saw and where. Mainnet: label **B** (same node code, not tested on mainnet) unless stated otherwise.

1. **For critical infrastructure that needs steady flows, watch the network live and raise your fee automatically when congestion rises.** Read the node's fee estimate and mempool size every few seconds. When they jump, raise your feerate. If a transaction is not accepted within about 10 s, rebuild it at a higher fee. Put a cap on it so a flood cannot drain you.
   - Source: round 1, ["Mitigation ideas"](https://github.com/STP-KAS/tn10-storm-2026-09-25-r1/blob/main/findings/overload-30m-summary.md): *"Detect congestion (mempool size / fee-estimate jump) and auto-bump. Resubmit with a higher fee (RBF) if a tx waits >10 s."*
   - Working example: round 6 fee rule, *"feerate = max(2 × node getFeeEstimate normalBuckets[0], … 200) sompi/gram, recomputed every 30 s"* ([round 6](https://github.com/STP-KAS/tn10-storm-2026-09-26-r6#4-fee-rule-user-1222-double-the-standard-so-we-have-priority)). 1 Oct storm: normal bucket × 3, floor 300, recomputed live ([analysis notes/LAUNCH.md](https://github.com/STP-KAS/tn10-storm-2026-10-01-analysis-public/blob/main/notes/LAUNCH.md)).
2. **Pay above the floor for anything time-sensitive.** Under a 57-minute overload, the minimum fee waited about 7 s at the median and up to 105 s. 10× the minimum always confirmed in 3.7 s or less. 100× bought nothing more than 10×. [overload summary](https://github.com/STP-KAS/tn10-storm-2026-09-25-r1/blob/main/findings/overload-30m-summary.md), [Build opinion](https://github.com/STP-KAS/tn10-storm-2026-09-26-build-opinion).
3. **Cap your fee. "Priority" follows whoever floods.** Paying the priority bucket as-is burned about 900 TKAS in 11.5 min, and the issuers went broke. Priority vs normal reached 8.4×. Use `min(priority, k × normal)` or an absolute maximum per transaction, and return an error instead of draining. [stress-findings item 5](https://github.com/STP-KAS/tn10-storm-2026-09-25#not-addressed-by-pr-165-status-per-the-author-26-sep), [draft issue](https://github.com/STP-KAS/tn10-storm-2026-09-25/blob/main/drafts/issue-fee-cap-multiplier.md).
4. **Make sure your fee setting is actually used.** Tic-tac-toe carriers always paid the floor (`min_fee`). Raising the fee estimate through a proxy changed nothing, and 0 games finished in 12 min of storm. [round 4 upstream-issues](https://github.com/STP-KAS/tn10-storm-2026-09-26-r4/blob/main/upstream-issues/README.md), [stress-findings item 2](https://github.com/STP-KAS/tn10-storm-2026-09-25).
5. **Re-broadcast pending transactions after a node reconnect or restart.** A node's mempool is not saved. A crash or restart drops every pending transaction silently. [F2](https://github.com/STP-KAS/tn10-storm-2026-09-25-r1/blob/main/findings/F2-mempool-not-persisted.md). Related upstream work: a node that finishes IBD may keep already-accepted transactions in its mempool; see [FINDINGS 11](FINDINGS.md) (upstream, not tested by us).
6. **Retry "mempool full" with backoff, and do not run a public node with a tiny mempool.** `--ram-scale=0.1` gives a 100k cap, and kaspad 2.1.0 panicked at `100001 > 100000`. Stay on the default scale. [F1](https://github.com/STP-KAS/tn10-storm-2026-09-25-r1/blob/main/findings/F1-mempool-cap-panic.md), [what-limits-tx-rate](https://github.com/STP-KAS/what-limits-tx-rate#how-a-full-mempool-panics).
7. **Never pick coins from an indexer balance alone. Confirm them against a node.** The public indexer froze for days and served spent outputs, and "orphan" rejects are the signal. [F3](https://github.com/STP-KAS/tn10-storm-2026-09-25-r1/blob/main/findings/F3-public-api-stale-utxos.md), [indexer-stall](https://github.com/STP-KAS/tn10-storm-2026-09-25-indexer-stall).
8. **Track coins already in flight.** Do not reuse a coin your own unconfirmed transaction already spends. Chain on the unconfirmed change, or pin chained sends to one node. Without that, 1,322 of 1,327 games failed. [stress-findings item 4](https://github.com/STP-KAS/tn10-storm-2026-09-25), round 1 solutions table.
9. **Avoid tiny outputs, and batch small payments (storage mass, KIP-9).** A 0.5 TKAS output costs 20,001 grams, so only about 25 fit per block. A 150× fee on small coins raised storage mass and lowered throughput. [stress-findings item 7](https://github.com/STP-KAS/tn10-storm-2026-09-25), [round 5](https://github.com/STP-KAS/tn10-storm-2026-09-26-r5).
10. **Pace, do not stop and start.** At thousands of tx/s, a brake that stops at the cap is too late, because in-flight work keeps flowing. Keep the rate below the mempool's reaction envelope. [round 4 lessons](https://github.com/STP-KAS/tn10-storm-2026-09-26-r4#flaws-and-operational-lessons).
11. **Know the ceiling.** A full block is about 3,000 ordinary payments per second. Submitting faster only fills mempools. More sockets or hostnames do not add capacity: six public names were three machines. [what-limits-tx-rate](https://github.com/STP-KAS/what-limits-tx-rate), [DESK-SHAPE-9-OCT](https://github.com/STP-KAS/tn10-storm-2026-10-04-questions/blob/main/plan/DESK-SHAPE-9-OCT.md).
12. **Stop sending to a dead node (Kaspa Pulse's node-dead rule).** From Kaspa Pulse ([@gokugalax](https://x.com/gokugalax)), who saw our senders fire at a dead node in his outside count of 9-10 Oct: RPC failing, not synced, lag over 60 s, or DAA still for 30 s means pause and fail over. A failed submit is a reject, never "sent". [credits/KASPA-PULSE.md](credits/KASPA-PULSE.md).
13. **Measure the right number.** Report network unique accepted, and keep submit-OK apart. Cross-check with an independent count such as **Kaspa Pulse's "accepted in blocks, two independent nodes, per UTC minute, by block time"**, and remember the ~56 tx/s base load (his figure). Do not treat dashboards as truth. See [METRICS.md](METRICS.md), [MASTER.md](history/MASTER.md), [tn10-storm-2026-10-06](https://github.com/STP-KAS/tn10-storm-2026-10-06).
14. **Operators: budget disk for pruning bursts (up to about 16 GB in 30 min) and keep `utxoindex` stable.** Rebuilding it took 18.5 min offline and about 13 GB. Count the chain right after a run, before pruning (Kaspa Pulse). [round 4 lessons](https://github.com/STP-KAS/tn10-storm-2026-09-26-r4#flaws-and-operational-lessons), [stress-findings item 6](https://github.com/STP-KAS/tn10-storm-2026-09-25).

---

## Hypothetical scenario: mint rush after smart contracts (stp, 11 Oct 2026)

> **Hypothetical, open for debate.** TN10 only, not tested on mainnet (**label B**). Not a prediction.

**Hypothetical (stp):** the first big real-world load on mainnet after smart contracts land may well be a mint rush, like the KCC-20 mints on TN10. If so, dapps, wallets and infrastructure should already have congestion monitoring with an automatic, capped fee raise in place.

**Evidence we already have** (links only; do not duplicate the numbered items above):

- Item 1 — auto fee raise on a congestion signal
- Item 2 — min fee waited ~7 s at the median and up to 105 s under overload; 10× min confirmed in ≤3.7 s
- Item 3 — cap the fee: paying priority as-is burned ~900 TKAS in 11.5 min
- Item 5 — re-broadcast after node restarts
- Item 8 — track coins in flight

**Observation (11 Oct storm):** fees were raised mid-run (400/600 → 560/840 → 1,120/1,680 sompi/gram) as covenant activity grew, per stp's observation on Kaspa Stream, not our measurement. [tn10-storm-2026-10-11](https://github.com/STP-KAS/tn10-storm-2026-10-11).

**Related but not a rush:** on 11 Oct, tn ops2 minted 2,488 trump2028 KCC-20 odd-leaf tokens on a quiet network; all landed with 0 rejects. That is not a mint rush under storm load. Logs: [STP-KAS/stp-trump2028](https://github.com/STP-KAS/stp-trump2028). A mint rush under storm load is a suggested future TN10 test (see [OPEN-QUESTIONS](docs/OPEN-QUESTIONS.md)).
