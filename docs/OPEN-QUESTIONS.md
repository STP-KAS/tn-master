> **Experimental. We are just trying this.** [Disclaimer](../DISCLAIMER.md) · [tn-master](../README.md)

# Open questions (needs more testing)

1. Does Kaspa Pulse's independent count of 11 Oct (07:30-12:30 UTC) match our chain count? **Pending** (his count; [credits](../credits/KASPA-PULSE.md)).
2. Build's 11 Oct results: **pending**.
3. Why do mass sender stalls follow box pauses? **Not sure / open for debate.**
4. Can the network hold the 11 Oct peak minute (3,583.1 tx/s) for an hour? The mean was 2,833.1; the mass-ceiling estimate is 3,040-3,080.
5. Kaspa Stream iOS vs desktop Chrome numbers ([FINDINGS 12](../FINDINGS.md)): screenshots of the same minute pending.
6. Stale mempool after IBD ([FINDINGS 11](../FINDINGS.md)): upstream fix proposed; not tested by us.
7. The keel lag spikes of 9 Oct: cause not found.

8. **Hypothetical (stp, 11 Oct 2026):** if the first big mainnet load after smart contracts is a mint rush, should dapps, wallets and infrastructure ship congestion monitoring with an automatic, capped fee raise now? Suggested future TN10 test: mint rush under storm load. See [ADVICE](../ADVICE-TO-DEVELOPERS.md#hypothetical-scenario-mint-rush-after-smart-contracts-stp-11-oct-2026) and [FINDINGS 15](../FINDINGS.md). **Hypothetical, open for debate.** Label B. The 2,488 trump2028 KCC-20 mints on 11 Oct ([stp-trump2028](https://github.com/STP-KAS/stp-trump2028)) all landed with 0 rejects on a quiet network and are not a rush.
