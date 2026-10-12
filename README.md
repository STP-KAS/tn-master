> **Experimental. We are just trying this.** [Disclaimer](DISCLAIMER.md) · Kaspa Testnet-10 only; tKAS has no value.

# tn-master: every TN10 storm, one map

TN10 storms are load tests we ran on Kaspa's Testnet-10 from 18 Sep to 11 Oct 2026: many senders pushing simple transactions at public and private nodes, then counting what the chain actually accepted. This repo holds no raw data. It links into each storm repo.

> ## Thank you, Kaspa Pulse ([@gokugalax](https://x.com/gokugalax), [kaspapulse.com](https://kaspapulse.com))
>
> Since 4 Oct 2026 Kaspa Pulse has counted our storms from the outside, on his own two nodes, and he shaped how we run and count them. These pages rest on his work:
>
> - **The node-dead rule.** A sender stops when its node is dead (RPC failing, not synced, lag over 60 s, or DAA still for 30 s); a failed submit is a reject, never "sent". He spotted our senders firing at a dead node on 9-10 Oct.
> - **The chain count right after END,** on non-archival nodes, before pruning removes the blocks. Every storm since 10 Oct has a COUNT step because of him.
> - **The "accepted in blocks" counter:** transactions accepted in blocks, two independent nodes, per UTC minute, by block time. It is the cross-check for every headline here ([METRICS.md](METRICS.md)).
> - **The base-load figure:** TN10 carries about **56 tx/s** of base load. Every network count on these pages includes it.
>
> Every input he gave and what we changed: **[credits/KASPA-PULSE.md](credits/KASPA-PULSE.md)**.

## Headline per storm

Best number per storm, with its counter. Counters differ between storms; read [METRICS.md](METRICS.md) before comparing rows. Every network count includes TN10 base load of about 56 tx/s (Kaspa Pulse).

| Storm | Best number (reported) | Counter | Repo |
|---|---:|---|---|
| 18-21 Sep, farm mining | not a tx rate | — | [tn10-storm-2026-09-18-mining-public](https://github.com/STP-KAS/tn10-storm-2026-09-18-mining-public) |
| 25 Sep, round 1 break test | 6,466 tx/s mean, 10-s peak 9,274 | Processed (overstates) | [tn10-storm-2026-09-25-r1](https://github.com/STP-KAS/tn10-storm-2026-09-25-r1) |
| 25-26 Sep, rounds 2-6 | 1,219 tx/s for 1 h 32 min (round 4) | Accepted (own runner) | [tn10-storm-2026-09-25](https://github.com/STP-KAS/tn10-storm-2026-09-25) |
| 26 Sep, round 7 | 267.2/s unique vs 357.2/s Processed | Both | [tn10-storm-2026-09-26-r7](https://github.com/STP-KAS/tn10-storm-2026-09-26-r7) |
| 1-3 Oct, box storm | best 1 min 4,253 tx/s; 58,905,910 included | Included (own) | [tn10-storm-2026-10-01](https://github.com/STP-KAS/tn10-storm-2026-10-01) |
| 2 Oct, full gusto | about 112 tx/s (one snapshot) | Accepted (sender) | [tn10-storm-2026-10-02-public](https://github.com/STP-KAS/tn10-storm-2026-10-02-public) |
| 6-7 Oct, Build desk | 2,207 tx/s seen accepted for 6 h 1 min | Seen accepted | [tn10-storm-2026-10-06](https://github.com/STP-KAS/tn10-storm-2026-10-06) |
| 7 Oct, mass ceiling | about 3,040-3,080 payments/s at 10 bps | Block reading (capacity) | [what-limits-tx-rate](https://github.com/STP-KAS/what-limits-tx-rate) |
| 8 Oct, checkout | 2,191 submit / 2,143 accept tx/s | Submit / local accept | [tn10-storm-2026-10-08](https://github.com/STP-KAS/tn10-storm-2026-10-08) |
| 9 Oct day, keel | max 2,435, avg 1,627 tx/s unique accepted | Network unique | [tn10-storm-2026-10-09](https://github.com/STP-KAS/tn10-storm-2026-10-09) |
| 9-10 Oct night | 7,541,103 in blocks; peak minute 1,223 tx/s | **Kaspa Pulse, accepted in blocks** | [tn10-storm-2026-10-09](https://github.com/STP-KAS/tn10-storm-2026-10-09) |
| 10-11 Oct (Sat 18:10 - Sun 02:35 UTC) | MAX step median 2,642.4 tx/s (n=9; corrected 11 Oct, was 2,644.9); Kaspa Pulse: 32.3M accepted, best minute 2,785 (21:20Z), 18:10-02:35Z | Network unique (headline) | [tn10-storm-2026-10-10](https://github.com/STP-KAS/tn10-storm-2026-10-10) |
| **11 Oct** (Sun 07:30-12:33 UTC) | **peak complete minute 3,583.1 (11:28Z); mean 2,833.1; median 3,107.1** (07:30-12:33Z); Kaspa Pulse: mean 2,844, median 3,055, best minute 3,646 (11:28Z), 51.2M accepted (07:30-12:30Z) | **Network unique (headline)**; Kaspa Pulse method live as cross-check | [tn10-storm-2026-10-11](https://github.com/STP-KAS/tn10-storm-2026-10-11) |

**11 Oct in one line:** network unique accepted, 07:30-12:33Z (303 minutes, halted early by stp: taking a break, other things on the agenda), about 51.5 million unique transactions; peak complete minute **3,583.1 tx/s** at 11:28Z, mean **2,833.1**, median **3,107.1** over 171 strict single minutes; includes about 56 tx/s base load. Build's results: pending. Source: [logs/bot/SUMMARY.md](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/bot/SUMMARY.md), [logs/COMBINED.md](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/COMBINED.md).

**Next test, plan only (no date yet):** [tn10-storm-plan-mint-rush](https://github.com/STP-KAS/tn10-storm-plan-mint-rush): a KCC-20 mint rush under storm load, capped auto-fee vs fixed-fee minters. Hypothesis: stp's; test idea: TN10 ops (the bot).

## Map

```
tn-master/
  README.md                 this page
  WHAT-WHY-HOW.md           what we test, why, how
  METRICS.md                TPS vs tx/s: one vocabulary, Kaspa Pulse's counter, base load
  FINDINGS.md               numbered findings, each with a label and a source
  ADVICE-TO-DEVELOPERS.md   what we would tell a builder, from what we saw
  history/                  MASTER.md (every storm), TIMELINE.md, storms/ (one page per storm)
  credits/                  KASPA-PULSE.md (every input and what we changed), kaspa-pulse/ (his counts)
  repos/                    INDEX.md (every storm repo), RENAME-LOG.md (old -> new names)
  docs/                     LESSONS.md, OPEN-QUESTIONS.md
```

| Page | What |
|---|---|
| [WHAT-WHY-HOW.md](WHAT-WHY-HOW.md) | What a storm is, why we run them, how (nodes, senders, clock, counting) |
| [METRICS.md](METRICS.md) | One vocabulary for tx/s; Kaspa Pulse's "accepted in blocks" counter; base load |
| [FINDINGS.md](FINDINGS.md) | Numbered findings with labels and sources |
| [ADVICE-TO-DEVELOPERS.md](ADVICE-TO-DEVELOPERS.md) | Fees, re-broadcast, coin selection, measuring |
| [history/MASTER.md](history/MASTER.md) | Every storm, oldest first (moved here from tn10-storm-2026-10-10) |
| [history/TIMELINE.md](history/TIMELINE.md) | One line per day |
| [history/storms/](history/storms/README.md) | One page per storm |
| [credits/KASPA-PULSE.md](credits/KASPA-PULSE.md) | Kaspa Pulse: every input and what we changed |
| [repos/INDEX.md](repos/INDEX.md) | Every storm repo: name, old name, date, class, visibility (incl. the [mint-rush plan](https://github.com/STP-KAS/tn10-storm-plan-mint-rush)) |
| [repos/RENAME-LOG.md](repos/RENAME-LOG.md) | The 11 Oct 2026 renames |
| [docs/LESSONS.md](docs/LESSONS.md) · [docs/OPEN-QUESTIONS.md](docs/OPEN-QUESTIONS.md) | Operations lessons; what still needs testing |
| [tn10-lowio-1148-notes](https://github.com/STP-KAS/tn10-lowio-1148-notes) | Notes on rusty-kaspa PR #1148 (lowio preset): diff read, risks, A/B test (FINDINGS 18) |

Counts only. No IP, host, port, key, seed, txid or wallet address on these pages. Public TN10 node names are allowed.

---

