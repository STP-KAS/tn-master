> **Experimental. We are just trying this.** [Disclaimer](DISCLAIMER.md) · Kaspa Testnet-10 only; tKAS has no value.

# What we observed, for developers and contributors (pre-runs 9–20)

Our intentions are good; our thought process may be questionable. These are notes from our own testing on Testnet-10, on our own nodes, mostly one desk node. Our methods may well be wrong, our readings of the code may be off, and none of this is advice or a claim about how Kaspa behaves in general. If you see a mistake, we would be glad to be corrected. Each line points to the numbered item in [FINDINGS.md](FINDINGS.md) with its source.

- **Submit-OK was not inclusion for us.** Under heavy payment load our desk could record a submit as OK while fewer of those payments landed in the same minutes (23–24).
- **Fee order seemed to matter once the ready set was larger than a block.** Under capacity our tiers landed alike; above it, higher sompi/gram landed more often, which looked consistent with our reading of the v2.1.0 selector's (fee/mass)^3 sampling. We may be reading the source wrong (25, 34).
- **Our own fee rates were not what we thought.** Our covenant hops were rated by the node on about three times the mass we priced them on, and our SDK's storage-mass helper read about four times low for one transaction shape. We fixed our pricing after that; the gap may be our misuse of the tools (37, 40, 43).
- **A heavy stream slowed cheaper transactions.** Our own heavy lane (about 266,700 mass a transaction) slowed our low-fee tiers and other TN10 users' transactions while it ran, and everything recovered within about a minute after it stopped. We are sorry for the slowdown to others (39, 44–49, 53, 58, 62, 66, 70).
- **Paying about twice a heavy stream's rate held up in our runs,** and about three times at the heaviest load we tried. That is a few short runs on one node (44, 47).
- **The node's own template sometimes left room unused** with many of our heavy transactions ready at a high rate, and stayed full with few of them at the same rate. Our guess about why rests on our reading of the sampler and is not proven (41, 65, 68).
- **Fee rules between our own lanes:** a rule that could step down settled every time we tried it; a rule that never stepped down kept climbing, even with a target it could reach. Both sides were always ours, on one node (51–52, 56, 59–60, 63–64, 67).
- **The node's fee estimate rose with our heavy lane's rate** even when low-fee transactions were barely slowed, so it may overstate what a transaction needs in that situation. One run, one node (69).

All runs were short, on Testnet-10 only, with our own coins and tools. Corrections, questions and better methods are welcome through issues on this repo.
