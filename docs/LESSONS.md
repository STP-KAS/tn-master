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

**Every neuron uploads.** From 9 Nov 2026, the day a storm repo is created it gets an index row, a history page, a timeline line, and a glance row. The hour the clock closes, the desk runner writes the result or the miss into those same pages and pushes this repo. A failed window stays. A plan page inside the storm repo is not rewritten to match the result. The page is [NEURON.md](NEURON.md). The operator's start line is: go to tn-master and read the rules.

**Confirmation, Sun 8 Nov 2026, 12:00 UTC.** The 10:40 waiter was stopped before the hash because the desk had no line on the repo to see that Mini was armed. Mini's first push is `logs/MINI-ARMED.md`. A quiet chat does not stop the desk when that line is on origin. [tn10-storm-2026-11-08-confirm](https://github.com/STP-KAS/tn10-storm-2026-11-08-confirm). Same shape as the 8 Nov rehearsal, on a new clock, so both publishers fire. It is not a restart of the 00:40 rehearsal. 43b and the other drafts stay off that clock.

**Tue 10 Nov 2026, named.** Pulse named the official count for Tuesday, Saturday's shape and times. [tn10-storm-2026-11-10](https://github.com/STP-KAS/tn10-storm-2026-11-10). The operator sends the pastes on Tuesday. A read before that day does not start a runner. The 18:20 UTC paste is ours, so the eight-hash proof can finish before his 18:40 deadline. File 1 is due Wed 11 Nov at 12:00 CET. File 2 is due Thu 12 Nov at 18:00 UTC. Wednesday is not a spare rerun. That day is [tn10-storm-2026-11-11](https://github.com/STP-KAS/tn10-storm-2026-11-11). Sixteen families stay off Tuesday's clock.

**Wed 11 Nov 2026, not armed.** Sixteen covenant families under payment offers of 1,013, then 2,027, then 3,040, then one observation minute at 4,053, then 1,013 again. A scored step closes on three clean minutes of submit-OK, or as `NOT MET` after one repair pass. The bot sends payments only in that minute. Review rounds first. [prompts/REVIEW.md](https://github.com/STP-KAS/tn10-storm-2026-11-11/blob/main/prompts/REVIEW.md). The pastes refuse to start until that file contains `REVIEW_CLOSED`.

**Pre-run 1 is not that day.** [tn10-storm-2026-11-11-prerun](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun) uses the same targets and has no T0. It holds until Tuesday's runner is down and the clock is past 2026-11-10T22:15:00Z. It does not stop the desk node. A fix that works is locked in that repo for the next pre-run. Wednesday's pages stay as they were.

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
