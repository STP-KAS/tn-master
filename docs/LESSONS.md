> **Experimental. We are just trying this.** [Disclaimer](../DISCLAIMER.md) · [tn-master](../README.md)

# Operations lessons

## Arming

We automate as much as possible.

**7 Nov 2026.** A scheduled task is not an arm. A clock by itself is not an arm. The miss: plans were changed while a run was still being calculated, the outcome was not read at the minute, and a task started a check it could not see. A git error was logged as zero hashes. The mini waited for a spoken word. Record: [tn10-storm-2026-11-08 WHAT-WENT-WRONG](https://github.com/STP-KAS/tn10-storm-2026-11-08/blob/main/WHAT-WENT-WRONG.md).

**From 8 Nov 2026, the go-plan rule.** A storm has two go plans. One for the desk. One for Mini. Each file carries the whole story. The first sentence names the machine, so a Build session does not guess. Paste the desk file on the desk and the Mini file on Mini. A rehearsal stays in its own repo. When both machines have reported and Pulse names a date, the counted storm is a new repo, `tn10-storm-YYYY-MM-DD`.

**8 Nov 2026 rehearsal.** Desk: [GO-DESK.md](https://github.com/STP-KAS/tn10-storm-2026-11-08/blob/main/GO-DESK.md). Mini: [GO-MINI.md](https://github.com/STP-KAS/tn10-storm-2026-11-08/blob/main/GO-MINI.md). The human boots the desk and Mini and leaves both logged in. Each machine reads its own file before 00:20 UTC. From that read, the clock runs the rest, including the sixteen-family step. No spoken word. The 7 Nov tasks stay unused. Bot reads either file, watches, and does not send. The pastes are not edited after 00:20 UTC. The repo stands on its own.

**Benchmark, from this rehearsal.** The next storm copies [tn10-storm-2026-11-08 BENCHMARK.md](https://github.com/STP-KAS/tn10-storm-2026-11-08/blob/main/BENCHMARK.md). Two root pastes, each the whole story, first sentence names the machine. One runner process per machine. Git by its full path. A schedule may share a clock only when a SKIP file turns one row off before that clock opens. The steps, the offer, and the abort line are the measurement. A later storm does not retune them.

**Mini publishes his own counts.** The 8 Nov paste told Mini not to commit the count files, so they stayed on Mini during the night. They were copied once afterwards, commit 6e5f086 at 2026-11-08T07:27:53Z. From then on the Mini runner writes `counts/mini/FIRST.md`, `counts/mini/LOAD.md`, and `counts/mini/SIXTEEN.md`, and that same runner pushes each file at its count-off. Git is called by the full path resolved when the runner starts. The desk does not write that folder. The chat does not publish it.

**The desk publishes its own counts.** Previous counted storms already counted on the sending machine. The 8 Nov desk counted, and the scores were written into the method log from the desk hop log. The runner did not publish a desk count file. From then on the desk runner writes `counts/desk/FIRST.md`, `counts/desk/LOAD.md`, and `counts/desk/SIXTEEN.md` for the same three windows, and pushes each file at the window end. Mini does not write that folder.

**A hash file shows when it reached GitHub.** Fixed is the local write. On origin is the commit time of the commit that put the rows on GitHub. The 8 Nov rows: eight at 2026-11-08T00:07:21Z, commit 430e905; thirty-two at 2026-11-08T02:30:02Z, commit 180529c; sixteen at 2026-11-08T04:00:04Z, commit abb8ac5. A later runner writes that time into the file after the push, from origin. A file with rows and no On origin line is not proof the push happened.

**Standing rule.** Who publishes, how a hash file is proved, and one runner per machine: [RULES.md](https://github.com/STP-KAS/tn10-storm-2026-11-08/blob/main/RULES.md) for the closed rehearsal, and [RULES.md](https://github.com/STP-KAS/tn10-storm-2026-11-08-confirm/blob/main/RULES.md) for the confirmation. A chat note does not replace that page.

**Confirmation, Sun 8 Nov 2026, 10:40 UTC.** [tn10-storm-2026-11-08-confirm](https://github.com/STP-KAS/tn10-storm-2026-11-08-confirm). Same shape as the 8 Nov rehearsal, on a new clock, so both publishers fire. It is not a restart of the 00:40 rehearsal. 43b and the other drafts stay off that clock. The counted storm is still a later repo, when Pulse names that day.

**Method log.** What this rehearsal did, which faults were already fixed, and what each phase proved, is [logs/METHOD.md](https://github.com/STP-KAS/tn10-storm-2026-11-08/blob/main/logs/METHOD.md). A later month starts from that page. A missed night keeps its clock. The next attempt is a later rehearsal, not a new clock on the same night.

- **Disk.** Pruning bursts take up to about 16 GB in 30 min; a 126 GB box disk cannot hold an 86 GB node plus 14-18 GB dips. Keep guards (senders pause at 8 GB, node stop at 5 GB) and never delete the storm SDK in cleanup. ([MASTER](../history/MASTER.md))
- **Nodes.** One node is a single point of failure. Each side needs its own node on its own machine; no tunnels (a node behind a tunnel lags). Keep `utxoindex` stable; rebuilding it takes about 18.5 min and 13 GB.
- **Node-dead rule (Kaspa Pulse).** Senders stop when their node is dead; a failed submit is a reject, never "sent".
- **Count right after END (Kaspa Pulse).** Non-archival nodes prune; count the chain before that, in parts if memory is short (11 Oct: the full count ran n2 out of memory; five segments worked).
- **One clock.** Both sides use the same T0 file (10 Oct: different clocks meant the sides were never at full rate together).
- **Schedulers.** Rate checks must read every sender file (11 Oct: a partial read held the bot back for about an hour). Mass stalls followed box pauses; RAM caps the bot at about 18 senders.
- **Coins.** Pre-split lanes; track coins in flight; never pick coins from an indexer alone.
- **Gates and deviations.** Lock prompts; log every change after the lock as a deviation with who and why ([tn10-storm-2026-10-11 CHANGES-DURING-RUN](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/bot/CHANGES-DURING-RUN.md)).
- **Logging.** Per-transaction submit and accept times are needed for `confirm.csv` and `order.csv` (missing on 11 Oct). Keep the headline rule in the repo (`headline_strict`).
