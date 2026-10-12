> **Experimental. We are just trying this.** [Disclaimer](../DISCLAIMER.md)

# MASTER: every TN10 storm, mid Sep to 11 Oct 2026

> Moved here from [tn10-storm-2026-10-10/history/MASTER.md](https://github.com/STP-KAS/tn10-storm-2026-10-10/blob/main/history/MASTER.md) on 11 Oct 2026; storm repos were renamed the same day to `tn10-storm-YYYY-MM-DD` ([RENAME-LOG](../repos/RENAME-LOG.md)). [tn-master](../README.md)

Thank you, Kaspa Pulse ([@gokugalax](https://x.com/gokugalax), [kaspapulse.com](https://kaspapulse.com)), for the questions and the outside count from 4 Oct on ([credits](../credits/KASPA-PULSE.md)).

One file, oldest first. Each run: date, setup, peak numbers, what broke, what we learned. Clocks are UTC. Older repos often wrote CEST; times here were converted.

**Every number is "reported": it is what the linked file says.** We did not re-measure it here. Where a number was not found, this page says so.

## Counters are not the same

Numbers from different eras are not directly comparable.

| Counter | Meaning |
|---|---|
| **Processed** | kaspad's block-body counter. All senders, and copies in parallel blocks. Overstates unique throughput. |
| **Seen accepted / included** | A sender saw its own transaction on a node's virtual chain. |
| **Submit-OK** | The node took it into its mempool. Not inclusion. |
| **Unique accepted** | Each id once, when the virtual chain accepts it. **This is the score now.** |
| **Accepted in blocks (Kaspa Pulse)** | His count on his own two nodes, per minute. |

## At a glance

| Date (UTC) | Run | Setup | Headline, reported | Counter | What broke |
|---|---|---|---|---|---|
| 14 Sep | Repo catalog | Build vs groks-wallet | 36-row snapshot | — | — |
| 18–21 Sep | Farm mining stress | One TN10 node, up to 150 CPU miners | not found as a tx rate | — | IBD stuck near 99% headers; `RouteIsFull` |
| 25 Sep | Break test, round 1 | n0 alone, small mempool cap | 6,466 tx/s mean, 10-s peak 9,274 | Processed | Mempool ~100k, 30,298 fee evictions; public indexer froze ≥ 3 d 15 h |
| 25–26 Sep | Rounds 2–6 with vprogs | n0 + own runners | Round 4: 1,219 tx/s for 1 h 32 min; round 6: 10,058,024 accepted | Accepted (runner) | Pruning disk; a 150× fee backfired |
| 26 Sep | Round 7 | n0 | 267.2/s unique vs 357.2/s Processed | Both | — |
| 1–3 Oct | Box storm, legs L1–L4 | n0 runners + Build via public nodes | 58,905,910 included; best 1 min 4,253 tx/s | Included | Public API lag 11.7 min, freeze ~85 min; n0 disk-full 3 Oct |
| 1–2 Oct | Full gusto | Desk, one public node | about 112 tx/s in one snapshot | Accepted (sender) | Public mempools > 100k |
| 6–7 Oct | Build desk runs | Desk via public nodes | 2,207 tx/s seen accepted for 6 h 1 min | Seen accepted | 6,321 was submit, not inclusion |
| 7 Oct | The mass ceiling | Desk | ~304–307 payments per full block, ~3,040 tx/s | Block reading | 3,500 not reached |
| 8 Oct | Checkout | Desk node locus | 2,191 submit / 2,143 accept tx/s (6 senders) | Submit / local accept | locus exited twice; n0 syncing |
| 9 Oct day | keel runs 1–5 | keel via tunnel | Unique accepted avg 1,627, max 2,435 tx/s | Unique accepted | keel lag up to 868.3 s |
| 9–10 Oct night | Friday storm | locus (Build) + keel (bot) | **7,541,103** in blocks; peak minute 1,223 tx/s | Kaspa Pulse | Wrong step file; locus died 01:28 |
| 10 Oct morning | Take 2 | locus + keel | Rehearsal row: 58 tx/s mean, clean | Submit | locus aborted 06:52 and 07:26; halted 08:06 |
| **10 Oct, from T0** | **Bot run + Build run** ([times](https://github.com/STP-KAS/tn10-storm-2026-10-10/blob/main/go/README.md#key-times)) | **n2 (box) + Build's own desk node** | MAX median **2,642.4** tx/s (complete n=9; corrected 11 Oct); 3000 line **not met**; Build HOLD desk med **4,032** | Unique accepted | Disk freeze zeroed C1500; sdk210 delete; n2 utxoindex off; HOLD WS stalls; Build clock mismatch |
| **11 Oct** | **Flat-out run, one clock** | **n2 (box) + Build's desk node** | Network unique accepted 07:30-12:33Z: peak complete minute **3,583.1** (11:28Z), mean **2,833.1**, median **3,107.1** | Unique accepted; Kaspa Pulse method live from 10:48Z | n2 froze 11:08-11:25Z; box pauses; mass sender stalls; halted early 12:33Z |

## Mid September: first contact

### 14 Sep: repo catalog
- **Setup:** Grok Build tested STP-KAS repos against groks-wallet on TN10. Frozen 36-row snapshot.
- **Source:** [tn10-hard-test](https://github.com/STP-KAS/tn10-hard-test).

### 18–21 Sep: farm mining stress
- **Setup:** a dedicated TN10 kaspad with up to 150 one-thread CPU miners. Desk CPU miners from 27 Sep ([tn10-storm-2026-09-27-desk-miners-public](https://github.com/STP-KAS/tn10-storm-2026-09-27-desk-miners-public), public clean copy).
- **Reported:** IBD stuck near 99% headers on one peer; `RouteIsFull` on block submits under farm load; one datadir lock panic. A tx rate: not found.
- **Source:** [tn10-storm-2026-09-18-mining-public](https://github.com/STP-KAS/tn10-storm-2026-09-18-mining-public) (public clean copy); summary in the [mainnet-implications note §1](https://github.com/STP-KAS/tn10-storm-2026-10-01/blob/main/TN10-STORMS-MAINNET-IMPLICATIONS-2026-10-04.md).
- **Learned:** one node under farm load is fragile; mining load and tx load need separate watching.

## 25–26 Sep: the September storm, with vprogs

### 25 Sep: break test (round 1)
- **Setup:** box node n0 alone, small mempool cap.
- **Reported:** Processed counter mean **6,466 tx/s**, 10-s peak **9,274**; mempool 99.97k; **30,298** evictions by feerate; one panic at `100001 > 100000`.
- **Source:** [mainnet-implications note §2](https://github.com/STP-KAS/tn10-storm-2026-10-01/blob/main/TN10-STORMS-MAINNET-IMPLICATIONS-2026-10-04.md); [round 1 findings](https://github.com/STP-KAS/tn10-storm-2026-09-25-r1/blob/main/findings/overload-30m-summary.md). Local handoff notes on the box (not on GitHub).
- **What broke:** the public api-tn10 indexer stopped advancing accepted transactions at **19:55:38** and still returned HTTP 503 on 29 Sep (at least 3 days 15 hours). Cause not proven; time correlation is not causation. [tn10-storm-2026-09-25-indexer-stall](https://github.com/STP-KAS/tn10-storm-2026-09-25-indexer-stall).
- **Learned:** Processed is not unique throughput. A full mempool panics at its cap.

### 25–26 Sep: rounds 2–6
- **Setup:** about 17 hours of load on n0 while running vprogs and the vprog tic-tac-toe.
- **Reported:** round 2: 10-s samples median 1,548, mean 2,507, peak 12,175 "TPS", mixed regimes, peak mempool ~88k ([round 2](https://github.com/STP-KAS/tn10-storm-2026-09-25-r2)). Round 4: **1,219 accepted tx/s** for 1 h 32 min, about 6.7M transactions, at a 6× fee ([round 4](https://github.com/STP-KAS/tn10-storm-2026-09-26-r4)). Round 5: a 150× storm fee was counterproductive ([round 5](https://github.com/STP-KAS/tn10-storm-2026-09-26-r5)). Round 6: **10,058,024** own-runner transactions accepted ([round 6](https://github.com/STP-KAS/tn10-storm-2026-09-26-r6)).
- **What broke:** pruning disk spikes on n0 (round 4 "pruning disk emergency").
- **Source, overview:** [tn10-storm-2026-09-25](https://github.com/STP-KAS/tn10-storm-2026-09-25), [round 1 public](https://github.com/STP-KAS/tn10-storm-2026-09-25-r1), [round 3](https://github.com/STP-KAS/tn10-storm-2026-09-26-r3), [final verdict](https://github.com/STP-KAS/tn10-storm-2026-09-26-verdict), opinions ([Build](https://github.com/STP-KAS/tn10-storm-2026-09-26-build-opinion), [bot](https://github.com/STP-KAS/tn10-storm-2026-09-26-bot-opinion)).
- **Learned:** paced load beats blasts; very high fees do not buy more room.

### 26 Sep: rounds 7 and 8, covenants under storm
- **Reported:** round 7, three counters side by side: **267.2/s** unique selected-chain accepted vs **357.2/s** Processed ([round 7](https://github.com/STP-KAS/tn10-storm-2026-09-26-r7)). 3,208/3,208 illegal spends rejected (round 7); 8,927/8,927 (round 8, [repo](https://github.com/STP-KAS/tn10-storm-2026-09-26-r8)).
- **Learned:** count unique accepted, not Processed.

### 26 Sep–3 Oct: n0 disk
- Pruning spikes and resyncs on n0, temporary disk 11–15 GB, a disk-full crash on 3 Oct ([mainnet-implications note §6](https://github.com/STP-KAS/tn10-storm-2026-10-01/blob/main/TN10-STORMS-MAINNET-IMPLICATIONS-2026-10-04.md)). Why later plans carry disk guards.

## 1–4 Oct: the box storm

### 1–3 Oct: legs L1–L4
- **Setup:** index-free runners on n0; Build adding load from the desk through public nodes.
- **Reported:** **58,905,910** box transactions included in four legs, 152 rejected, 361,814 tKAS fees. Best 1 min **4,253 tx/s**, best 10 min **3,717**, best 60 min **2,518**. Our block share 50–63% while the box miners ran.
- **What broke:** public API lagged up to 11.7 min and froze about 85 min on the night of 2 Oct; each episode we saw end recovered within 2–5 min. n0 disk-full on 3 Oct.
- **Source:** [tn10-storm-2026-10-01](https://github.com/STP-KAS/tn10-storm-2026-10-01); raw data and analysis in [tn10-storm-2026-10-01-analysis-public](https://github.com/STP-KAS/tn10-storm-2026-10-01-analysis-public) (public clean copy); [tn10-storm-2026-10-01-reports-public](https://github.com/STP-KAS/tn10-storm-2026-10-01-reports-public) (public clean copy); local box notes (not on GitHub).
- **Learned:** "about 5k TPS" does not hold as unique included transactions. Label every mainnet sentence A/B/C ([note, 4 Oct](https://github.com/STP-KAS/tn10-storm-2026-10-01/blob/main/TN10-STORMS-MAINNET-IMPLICATIONS-2026-10-04.md)).

### 1–2 Oct: full gusto
- **Setup:** desk wallet self-spend on one public node, avoiding public nodes whose mempools were over 100,000.
- **Reported:** one snapshot at 08:19:59 UTC, 2 Oct: about **112 tx/s**, 0 rejected. A run total: not found.
- **Source:** [tn10-storm-2026-10-02-public](https://github.com/STP-KAS/tn10-storm-2026-10-02-public) (public clean copy; the four full gusto repos were merged into one on 11 Oct: ramp/, ledger/, match/).
- **Learned:** public mempools fill first; a private node is needed.

### 4 Oct: Kaspa Pulse's questions
- His five questions arrive by X DM; [tn10-storm-2026-10-04-questions](https://github.com/STP-KAS/tn10-storm-2026-10-04-questions) starts. See [credits](../credits/KASPA-PULSE.md).

## 5–7 Oct: method first, and the mass ceiling

- **5 Oct.** His four tightenings; the plan is rewritten around his questions ([NEXT-STORM-PLAN.md](https://github.com/STP-KAS/tn10-storm-2026-10-04-questions/blob/main/plan/NEXT-STORM-PLAN.md)).
- **6–7 Oct, Build's desk runs via public nodes.** **Reported:** **6,321 tx/s** submit-OK for 20 s with about 1,900/s seen accepted, so 6,321 is submit, not inclusion. A hold of **2,207 tx/s seen accepted** from 6 Oct 23:53 to 7 Oct 05:54 (6 h 1 min), fee 200/300. Source: [tn10-storm-2026-10-06](https://github.com/STP-KAS/tn10-storm-2026-10-06).
- **7 Oct, the ceiling.** **Reported:** full blocks of about 304 payments at about 498,800 of 500,000 compute mass, about 3,040 tx/s for the network. A signed 1-in/1-out is about 1,624 mass, so about 308 per block and about 3,080 tx/s. 3,500 included was not reached. Source: [what-limits-tx-rate](https://github.com/STP-KAS/what-limits-tx-rate), [tn10-storm-2026-10-07](https://github.com/STP-KAS/tn10-storm-2026-10-07).
- **7 Oct, the Pulse window.** His count for 18:52–19:23 came out much lower than our screenshot; our log had stopped at 18:38:39. **Learned:** one window, one clock, sent and accepted kept apart ([PULSE-WINDOW-7-OCT.md](https://github.com/STP-KAS/tn10-storm-2026-10-04-questions/blob/main/plan/PULSE-WINDOW-7-OCT.md)).
- **7 Oct.** [tn10-storm-2026-10-08](https://github.com/STP-KAS/tn10-storm-2026-10-08) hub; storm set for Fri 9 Oct. [tn10-storm-2026-10-09-challenge](https://github.com/STP-KAS/tn10-storm-2026-10-09-challenge) opens, still empty.

## 8 Oct: the checkout, and n0 retired

- **Setup:** desk node locus, ten rounds, 18:00–20:11.
- **Reported:** six senders: submit mean **2,191.2**, local accept mean **2,142.9** tx/s, 0 rejects. Ten senders: **2,100.1** / **1,954.1**. More senders added waiting, not throughput.
- **What broke:** locus exited twice (19:00:06 and 19:03:41) and was restarted. n0 had frozen at 06:54 UTC after pruning filled the disk and was resyncing, so the bot side was not measured (TN10 ops, 8 Oct message; not in git). n0 was retired.
- **Source:** [tonight-8-oct/RESULTS.md](https://github.com/STP-KAS/tn10-storm-2026-10-08/blob/main/tonight-8-oct/RESULTS.md), [AFTER-8-OCT.md](https://github.com/STP-KAS/tn10-storm-2026-10-04-questions/blob/main/plan/AFTER-8-OCT.md).
- **Learned:** a 126 GB box disk cannot hold an 86 GB node plus 14–18 GB pruning dips (TN10 ops, 8 Oct; not in git). One node on the desk is a single point of failure.

## 9 Oct day: keel pre-test and duplicates

- **Setup:** second desk node keel; the bot reached it through a tunnel. Light 643-mass hops, fee 200/300.
- **Reported:** 15 runners held 60 tx/s; 100 tx/s failed the p90 ≤ 10 s rule; run 5 ended on keel lag (302 s). 48–49% of tx slots in blocks were duplicates. Network unique accepted while keel kept up (12:24–13:15): average **1,627**, median 1,704, max **2,435** tx/s.
- **What broke:** with no bot load, keel lag reached **868.3 s** at 15:28:26 and keel froze for minutes about every 10 min from about 14:05. Cause not found.
- **Source:** [monitoring-result/bot-result](https://github.com/STP-KAS/tn10-storm-2026-10-09/blob/main/monitoring-result/bot-result/README.md), [goal/OPINION.md](https://github.com/STP-KAS/tn10-storm-2026-10-09/blob/main/goal/OPINION.md), [tn10-storm-2026-10-09 README](https://github.com/STP-KAS/tn10-storm-2026-10-09).
- **Learned:** duplicates, not block space, keep unique accepted near 2,000. A node behind a tunnel lags.

## 9–10 Oct night: the Friday storm (failed as a test of the plan)

Details and both step tables: [2026-10-09-night.md](https://github.com/STP-KAS/tn10-storm-2026-10-10/blob/main/history/2026-10-09-night.md).

- **Setup:** locus (Build) and keel (bot, through a tunnel), one miner per node. Planned restart: gate 21:45, T0 22:30, end 06:30.
- **Reported by Kaspa Pulse (his own two nodes):** **7,541,103** tx accepted in blocks 21:25–05:35; **6,607,409** in 22:00–01:28, mean **526.9 tx/s**; peak minute **00:47, 1,223 tx/s**; 493–716 blocks/min, 9.92 blocks/s, longest gap 1.13 s; miners-off 22:01–22:24 confirmed; our count 1.2% higher in sum over 238 minutes (median 3.5%); base load about 55 tx/s after 01:28 (measured that night; TN10 base load is about 56 tx/s, figure from Kaspa Pulse). Source: [his notes](../credits/kaspa-pulse/2026-10-09-night/tn10-2026-10-09-2125-0535-notes.txt) (published with his yes, as relayed by stp, 10 Oct).
- **What broke:** the desk ran the voided 21:00 step file from 21:52; a second holder started; the max step did not run; locus aborted at about 01:28 (`Rust cannot catch foreign exceptions`) and the hold kept "sending" to it until 04:45. Source: [RUN-REPORT.md](https://github.com/STP-KAS/tn10-storm-2026-10-09/blob/main/tn10-storm-2026-10-09/build/RUN-REPORT.md).
- **Learned:** one step file and one holder; a sender must stop when its node dies; count the chain soon after the run.

## 10 Oct morning: take 2 (halted)

Details: [2026-10-10-take2.md](https://github.com/STP-KAS/tn10-storm-2026-10-10/blob/main/history/2026-10-10-take2.md).

- **Setup:** same desk nodes. Gate 06:15, T0 07:00, end 15:00.
- **Reported:** 06:15 gate passed (keel lag 1 s). Build's rehearsal row closed at 06:59:02: target 60, mean submit 58, clean.
- **What broke:** locus aborted at 06:52:56 and 07:26 with `0xc0000409` at the same offset; a watcher restarted it. stp halted the storm at 08:06 and retired both desk nodes (TN10 ops message, 10 Oct; not in git).
- **Source:** [INCIDENT-0652.md](https://github.com/STP-KAS/tn10-storm-2026-10-09/blob/main/tn10-storm-2026-10-10/build/INCIDENT-0652.md), [go/take2](https://github.com/STP-KAS/tn10-storm-2026-10-09/blob/main/go/take2/README.md).
- **Learned:** that kaspad build on the desk crashes at one offset; each side needs its own node on its own machine.

## 10 Oct, from T0: the bot run and the build run ([tn10-storm-2026-10-10](https://github.com/STP-KAS/tn10-storm-2026-10-10))

- **Setup:** bot on n2 (box), Build on its own new desk node. Private, pruned, no tunnel, one miner per side. Bot submits to the five public TN10 nodes; n2 for reads/coins/count/miner. Build sends to its desk node (public fallback). Plan: [tn10-storm-2026-10-10-plan @ 517fb43](https://github.com/STP-KAS/tn10-storm-2026-10-10-plan/tree/517fb43), refined in [go/](https://github.com/STP-KAS/tn10-storm-2026-10-10/blob/main/go/README.md). Times: [go/README.md](https://github.com/STP-KAS/tn10-storm-2026-10-10/blob/main/go/README.md#key-times) (T0 18:30Z, END 02:30Z). Build's own SUMMARY used T0 15:00Z / END 23:00Z — align by UTC wall clock.
- **Reported (bot chain-count, `complete_minute=yes`, bot clock windows):** X250 med **293.4** (n=7); C1000 **512.0** (n=4); C1500 **251.1** (n=1); C2000 **1,241.6** (n=6); C2500 **2,526.3** (n=7); MAX **2,642.4** (n=9); HOLD **939.1** (n=123). Recount averages (supporting): C2500 **2,512.7**, MAX **2,617.2**. **Corrected 11 Oct 2026:** the first chain-count.csv counted 89 minutes inside lumped recount rows twice (window sum 38.36M → **32.30M**), and the old recount averages (3,426.4 / 3,271.5) divided lumped rows by 60; details in [tn10-storm-2026-10-10 chain-count METHOD](https://github.com/STP-KAS/tn10-storm-2026-10-10/blob/main/logs/bot/chain-count.csv.METHOD.md). Bot submit means (steps.csv): X250 64.29 … MAX 916.69, HOLD 638.74. Build submit on UTC overlap during bot C2500/MAX ~1.6–1.8k; Build HOLD own-clock mean submit **1,718**, desk network-unique median **4,032** over 175 min.
- **Success line (3,000 tx/s, median of ≥10 complete minutes):** **not met**. Best plan-metric step MAX ~2,642 (n=9). Miners **off** at END 02:30Z; after-END wrap senders=0 miner=0.
- **What broke:** box disk/freeze 21:08–21:29 CEST zeroed C1500; sdk210 deleted in cleanup then restored; n2 restarted without utxoindex ~19:58Z; HOLD overnight WS/RPC stalls and coin buffer to 0; Build late join, wrong clock, C2000 skipped, HOLD re-armed at 1875 not 2400.
- **Source:** [logs/COMBINED.md](https://github.com/STP-KAS/tn10-storm-2026-10-10/blob/main/logs/COMBINED.md), [logs/WRITE-UP.md](https://github.com/STP-KAS/tn10-storm-2026-10-10/blob/main/logs/WRITE-UP.md), [docs/RESULTS.md](https://github.com/STP-KAS/tn10-storm-2026-10-10/blob/main/docs/RESULTS.md), [logs/bot/](https://github.com/STP-KAS/tn10-storm-2026-10-10/blob/main/logs/bot/README.md), [logs/build/](https://github.com/STP-KAS/tn10-storm-2026-10-10/blob/main/logs/build/README.md).
- **Learned:** both sides must run the same T0 file; disk reclaim must spare the storm SDK; dropping utxoindex mid-HOLD ends top-ups; plan pass/fail stays on complete-minute chain medians, not recount averages or a partner desk HOLD.

## 11 Oct: the flat-out run, one clock ([tn10-storm-2026-10-11](https://github.com/STP-KAS/tn10-storm-2026-10-11))

- **Setup:** both sides on one clock, START 07:30Z, no steps: as many tx/s as possible. Bot: 15, then 18 senders to the five public TN10 nodes; n2 for reads, coins, the count and one miner. Build on its own desk node. stp raised effort at 09:28Z, the bot fee to 560/840 at 10:31:10Z and to 1,120/1,680 at 12:08:40Z (covenant activity growing on Kaspa Stream, stp's observation), held the rate high and extended END to 13:30Z.
- **Reported (chain count from n2 after the halt, network unique accepted, 07:30-12:33Z, 303 minutes):** about **51.5 million** unique transactions; peak complete minute **3,583.1 tx/s** (11:28Z), mean **2,833.1**, median **3,107.1** (171 strict single minutes). Includes about 56 tx/s base load (Kaspa Pulse). Bot alone: about 1,212 tx/s accepted mean, best full minute about 1,630. Kaspa Pulse's method, live from 10:48Z on two nodes: 11:28Z at 3,645.9 tx/s. His own count and Build's results: pending.
- **What broke:** n2 froze 11:08-11:25Z (DAA stuck, sink lag about 16 min) and was restarted; box pauses left 24 bot minutes without logs; five mass sender stalls; the 15-minute rate check undercounted until fixed at 10:31Z.
- **Stopped early by stp: taking a break, other things on the agenda** (HALT 12:33:01Z).
- **Source:** [logs/bot/SUMMARY.md](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/bot/SUMMARY.md), [logs/COMBINED.md](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/COMBINED.md), [logs/WRITE-UP.md](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/WRITE-UP.md), [chain-count.csv](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/bot/chain-count.csv) (`headline_strict` rebuilds the peak and median).
- **Learned:** one clock works; past the mass-ceiling estimate for single minutes, but the mean stays below it; the box's own pauses and RAM, not the network, now limit the bot side.
