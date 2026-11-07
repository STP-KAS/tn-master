> **Experimental. We are just trying this.** [Disclaimer](../DISCLAIMER.md) · [tn-master](../README.md)

# Open questions (needs more testing)

1. Does Kaspa Pulse's independent count of 11 Oct (07:30-12:30 UTC) match our chain count? **Answered:** yes, within 0.1% over the run (his 51.2M over 300 minutes vs our 51.5M over 303; [credits](../credits/KASPA-PULSE.md)).
2. Build's 11 Oct results: **pending**.
3. Why do mass sender stalls follow box pauses? **Not sure / open for debate.**
4. Can the network hold the 11 Oct peak minute (3,583.1 tx/s) for an hour? The mean was 2,833.1; the mass-ceiling estimate is 3,040-3,080.
5. Kaspa Stream iOS vs desktop Chrome numbers ([FINDINGS 12](../FINDINGS.md)): screenshots of the same minute pending.
6. Stale mempool after IBD ([FINDINGS 11](../FINDINGS.md)): upstream fix proposed; not tested by us. It also skews a node's fee estimate (priority 1,644 vs 100 in one report on the PR). Open: does the fix cover a non-mining node that falls behind without a full IBD? The PR does not say. Untested hypothesis: stale mempools after restarts or resyncs explain some high fee quotes from public nodes during our storms.
7. The keel lag spikes of 9 Oct: cause not found.

8. **Hypothetical (stp, 11 Oct 2026):** if the first big mainnet load after smart contracts is a mint rush, should dapps, wallets and infrastructure ship congestion monitoring with an automatic, capped fee raise now? The hypothesis is stp's; the idea to test it as a mint rush under storm load on TN10 came from TN10 ops (the bot). Test plan (no date yet): [tn10-storm-plan-mint-rush](https://github.com/STP-KAS/tn10-storm-plan-mint-rush). See [ADVICE](../ADVICE-TO-DEVELOPERS.md#hypothetical-scenario-mint-rush-after-smart-contracts-stp-11-oct-2026) and [FINDINGS 15](../FINDINGS.md). **Hypothetical, open for debate.** Label B. The 2,488 trump2028 KCC-20 mints on 11 Oct ([stp-trump2028](https://github.com/STP-KAS/stp-trump2028)) all landed with 0 rejects on a quiet network and are not a rush.

9. **Where does the covenant-family curve bend between 8 and 32, and does the number move when the other machine sends?** At 8 families the counted steps of this shape cleared 1.14, slowest family about 1.26 hop/s. At 32 families the total sat near 34 hop/s and the slowest family finished under 1.14 ([FINDINGS 19](../FINDINGS.md)). Sixteen families has not been run. Every run of this shape so far was the desk sending. Turn **43a** is the last part of the 8 Nov 2026 test, inside [GO.md](https://github.com/STP-KAS/tn10-storm-2026-11-08/blob/main/GO.md), at 04:15 UTC if the earlier part finishes clean. That test is not the official count. Turn **43b** has no date. The long page: [tn10-storm-plan-family-curve](https://github.com/STP-KAS/tn10-storm-plan-family-curve). **We do not claim this is the truth.** Label C until a window is counted. Not the 7 Nov window. The mint-rush question above stays its own plan.
