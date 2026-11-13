> [tn-master](../README.md)

# TIMELINE (UTC dates)

| Day | What happened |
|---|---|
| 14 Sep | Build tests STP-KAS repos against groks-wallet ([tn10-hard-test](https://github.com/STP-KAS/tn10-hard-test)) |
| 18-21 Sep | Farm mining stress: up to 150 CPU miners on one TN10 node |
| 25 Sep | Round 1 break test; public indexer freezes at 19:55Z |
| 25-26 Sep | Rounds 2-6 with vprogs; round 4 holds 1,219 accepted tx/s for 1 h 32 min |
| 26 Sep | Rounds 7 and 8: covenants under storm; unique vs Processed |
| 27 Sep | Desk CPU miners through a tunnel |
| 1-3 Oct | Box storm L1-L4: 58.9M included, best minute 4,253 tx/s (own, included) |
| 2 Oct | Full gusto on one public node |
| 3 Oct | n0 disk-full crash |
| 4 Oct | **Kaspa Pulse's five questions** arrive; the questions repo starts |
| 5 Oct | Kaspa Pulse's method points and four tightenings; the plan is rewritten |
| 6-7 Oct | Build desk: 2,207 tx/s seen accepted for 6 h; 6,321 was submit only |
| 7 Oct | The mass ceiling (about 3,040 tx/s); the Pulse window check |
| 8 Oct | Checkout on locus; n0 retired |
| 9 Oct | keel day: duplicates keep unique accepted near 2,000 |
| 9-10 Oct | Friday night storm; **Kaspa Pulse counts 7,541,103 in blocks**; senders fired at a dead node |
| 10 Oct | Take 2 halted; node-dead rule and chain count after END adopted (Kaspa Pulse); bot run and build run from 18:30Z |
| 11 Oct | Flat-out run on one clock: peak complete minute **3,583.1**, mean **2,833.1**, median **3,107.1** tx/s (07:30-12:33Z); Kaspa Pulse's method logged live from 10:48Z; repos renamed; tn-master starts |
| 29 Oct | Covenant families in parallel: total hops/s **0.81 / 1.96 / 3.24** for 1 / 2 / 4 families (19:00-20:00Z); [review](https://github.com/STP-KAS/tn10-storm-2026-10-29/blob/main/logs/storm-2026-10-29/REVIEW.md) |
| 7 Nov | Covenant families 1, then 2, then 4, then 8. The window failed. No genesis, no sends, no mini count, no load. Pre-tests stay published and are not that window. [tn10-storm-2026-11-07](https://github.com/STP-KAS/tn10-storm-2026-11-07). Record: [tn10-storm-2026-11-08](https://github.com/STP-KAS/tn10-storm-2026-11-08). |
| 8 Nov | Rehearsal, stands alone, start 00:40 UTC. Desk night closed 04:50 UTC. Confirmation, same day, T0 12:00 UTC, finished 16:10 UTC. Both publishers fired. [tn10-storm-2026-11-08](https://github.com/STP-KAS/tn10-storm-2026-11-08), [tn10-storm-2026-11-08-confirm](https://github.com/STP-KAS/tn10-storm-2026-11-08-confirm) |
| 10 Nov | Named, not run. Pulse named Tuesday. Saturday shape, T0 19:00 UTC. The operator sends the pastes that day. [tn10-storm-2026-11-10](https://github.com/STP-KAS/tn10-storm-2026-11-10) |
| 11 Nov | Plan, not armed. Sixteen covenant families under a payment climb. T0 12:00 UTC. Review first. [tn10-storm-2026-11-11](https://github.com/STP-KAS/tn10-storm-2026-11-11). Pre-run 1 of that plan opened 22:05 UTC on 10 Nov and failed before hashes. Pre-runs 2–7 ran later on 11 Nov. The rehearsal did not move Wednesday's clock. [history/storms/2026-11-11-prerun.md](storms/2026-11-11-prerun.md) |
| 12 Nov | Pre-runs 8, 9, 10, 11 and 12 of the same rehearsal finished through RETURN (Brussels 00:16–00:43, 02:11–02:38, 08:24–08:53, 10:00–10:46 and 11:38–12:46). Desk-node inclusion was counted. Pulse has not counted it. In pre-run 10, cheap chained tiers were already slow at 1,013; in pre-run 11 we observed that the floor followed the ready mass in our node's mempool, driven mostly by another sender's heavy stream at the same fee; in pre-run 12 fee tiers near the floor separated only while that stream was present. [tn10-storm-2026-11-11-prerun-10](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun-10), [tn10-storm-2026-11-11-prerun-11](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun-11), [tn10-storm-2026-11-11-prerun-12](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun-12) |
| 12 Nov | Pre-run 13 of the same rehearsal (Brussels 14:10–16:18): our own heavy lane on TN10, with the operator's OK, as the only heavy competitor against five family fee tiers; observed through HOLD-4, then failed before RETURN on a coin-count abort. We observed the tiers slow in steps with the lane's ready count and recover within a minute, and that our hops' node fee rate was about a third of the built rate. Our lane slowed other users' low-fee transactions while it ran; the repo says so. Pulse has not counted it. [tn10-storm-2026-11-11-prerun-13](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun-13) |
| 12 Nov | Pre-run 14 of the same rehearsal (Brussels 18:54–21:09, live run 19:20–20:58): covenant hops priced on the node's own mass, against our own heavy lane at 100 and 126 (operator's OK), with the outside heavy stream present; finished through RETURN. We observed that a hop at the lane's rate kept 76–88 percent of its BASE rate, about twice the lane's rate kept it within about 4 percent, and the families recovered within a minute. Our lane slowed other users' traffic while it ran; the repo says so. Pulse has not counted it. [tn10-storm-2026-11-11-prerun-14](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun-14) |
| 12 Nov | Pre-run 15 of the same rehearsal (Brussels 21:12–23:15, live run 21:44–23:11): the same node-priced covenant hops against our own heavy lane uncapped at 126 and 150 (operator's OK), with the outside heavy stream present; finished through RETURN. We observed that about twice the lane's rate kept a hop within about 5 percent of its BASE rate and about three times was needed at the heaviest step. Our lane slowed other users' traffic while it ran; the repo says so. The bot's box rebooted mid-run, so its file says `NO SEND check-failed`, pushed late. Pulse has not counted it. [tn10-storm-2026-11-11-prerun-15](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun-15) |
| 13 Nov | Pre-run 16 of the same rehearsal (Brussels 23:27 on 12 Nov – 01:45, live run 00:10–01:38): a fee-escalation duel, both sides ours, nine covenant families against our own heavy lane (operator's OK), both on one rule; finished through RETURN. We observed the rates settle near twice the lane's rate (median 1.96) within three minutes, with no spiral and neither side giving up; the covenant side was too light to hurt the lane. Our lane slowed other users' traffic while it ran; the repo says so. The bot filed `NO SEND no-free-node` on time. Pulse has not counted it. [tn10-storm-2026-11-11-prerun-16](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun-16) |
