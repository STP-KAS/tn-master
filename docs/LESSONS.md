> **Experimental. We are just trying this.** [Disclaimer](../DISCLAIMER.md) · [tn-master](../README.md)

# Operations lessons

## Arming

We automate as much as possible.

**7 Nov 2026.** A scheduled task is not an arm. A clock by itself is not an arm. The miss: plans were changed while a run was still being calculated, the outcome was not read at the minute, and a task started a check it could not see. A git error was logged as zero hashes. The mini waited for a spoken word. Record: [tn10-storm-2026-11-08 WHAT-WENT-WRONG](https://github.com/STP-KAS/tn10-storm-2026-11-08/blob/main/WHAT-WENT-WRONG.md).

**8 Nov 2026 test.** One plan: [GO.md](https://github.com/STP-KAS/tn10-storm-2026-11-08/blob/main/GO.md). The human boots the desk and Mini and leaves both logged in. Each machine reads that one file before 00:20 UTC. From that read, the clock runs the rest, including the sixteen-family step. No second sheet. No spoken word. The 7 Nov tasks stay unused. The bot reads the same file, watches, and does not send. The official count date stays unlocked. The plan is not edited after 00:20 UTC.

- **Disk.** Pruning bursts take up to about 16 GB in 30 min; a 126 GB box disk cannot hold an 86 GB node plus 14-18 GB dips. Keep guards (senders pause at 8 GB, node stop at 5 GB) and never delete the storm SDK in cleanup. ([MASTER](../history/MASTER.md))
- **Nodes.** One node is a single point of failure. Each side needs its own node on its own machine; no tunnels (a node behind a tunnel lags). Keep `utxoindex` stable; rebuilding it takes about 18.5 min and 13 GB.
- **Node-dead rule (Kaspa Pulse).** Senders stop when their node is dead; a failed submit is a reject, never "sent".
- **Count right after END (Kaspa Pulse).** Non-archival nodes prune; count the chain before that, in parts if memory is short (11 Oct: the full count ran n2 out of memory; five segments worked).
- **One clock.** Both sides use the same T0 file (10 Oct: different clocks meant the sides were never at full rate together).
- **Schedulers.** Rate checks must read every sender file (11 Oct: a partial read held the bot back for about an hour). Mass stalls followed box pauses; RAM caps the bot at about 18 senders.
- **Coins.** Pre-split lanes; track coins in flight; never pick coins from an indexer alone.
- **Gates and deviations.** Lock prompts; log every change after the lock as a deviation with who and why ([tn10-storm-2026-10-11 CHANGES-DURING-RUN](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/bot/CHANGES-DURING-RUN.md)).
- **Logging.** Per-transaction submit and accept times are needed for `confirm.csv` and `order.csv` (missing on 11 Oct). Keep the headline rule in the repo (`headline_strict`).
