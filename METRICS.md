> **Experimental. We are just trying this.** [Disclaimer](DISCLAIMER.md) · [tn-master](README.md)

# METRICS: TPS vs tx/s, one vocabulary

**TPS and tx/s are the same unit** (transactions per second). What differs is **what is counted** and **over what window**. Always say both.

| Counter | What it counts | Use |
|---|---|---|
| **Submitted** (submit-OK) | What senders handed to a node and the node acknowledged. Not inclusion. | Sender health only |
| **Node-accepted / seen accepted** | What one sender saw land on one node's virtual chain | Per side, per node |
| **Network unique accepted** (the headline) | Each transaction id counted once, when the virtual chain accepts it, for the whole network (all senders), from a chain count after the run | **Headline** |
| **Accepted in blocks (Kaspa Pulse)** | Transactions accepted in blocks, **two independent nodes, per UTC minute, by block time**. Independent counts by Kaspa Pulse ([@gokugalax](https://x.com/gokugalax), [kaspapulse.com](https://kaspapulse.com)) on two external nodes. | Independent cross-check |
| **Processed** (kaspad log) | Block-body counter: a transaction once per block it sits in, so copies in parallel blocks count again | Overstates; never a headline |
| **Dashboards** (Kaspa Stream, api-tn10) | Their own indexed counts over a socket, their own node's mempool | Lag and can freeze; never a headline |

**Base load.** Every network count in this file and on every tn-master page includes TN10's base load of about **56 tx/s** (figure from Kaspa Pulse).

## Kaspa Pulse's counter

Independent counts by Kaspa Pulse ([@gokugalax](https://x.com/gokugalax), [kaspapulse.com](https://kaspapulse.com)): accepted in block counts on two external nodes, per UTC minute, by block time. From 11 Oct the bot also logs his method live in [logs/bot/pulse-method-minute.csv](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/bot/pulse-method-minute.csv), **live from 10:48 UTC (12:48 CEST); first full minute 10:49 UTC**, with the start time written at the top of the file. Earlier minutes come from the after-run chain count. Because it buckets by the accepting chain block's timestamp, its minutes differ slightly from the chain-count rows (11:28Z: 3,645.9 tx/s there vs 3,583.1 in the chain count). His own count of 11 Oct: mean 2,844, median 3,055, best minute 3,646 (11:28Z), 51.2 million accepted, 07:30-12:30Z ([credits](credits/kaspa-pulse/2026-10-11/README.md)).

## Dashboard tile vs per-minute count

An explorer's TPS tile and accepted tx per UTC minute are **different measures**: the tile is an instantaneous dashboard reading over a short, unstated window, the per-minute count is every accepted transaction in one full UTC minute divided by 60. A tile can read higher than the best full minute without either being wrong. On 11 Oct the explorer tile showed 3,708 tx/s; Kaspa Pulse's best full minute was 3,646 tx/s. Both are right: one is an instantaneous dashboard reading, the other a per-minute count.

**Two ways to bucket the same chain into minutes.** Our chain count ([chain-count.csv](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/bot/chain-count.csv.METHOD.md)) buckets by **when n2 saw each block** (the chain tip n2 had at each UTC-minute boundary): peak **3,583.1 tx/s** at 11:28Z on 11 Oct. A count **by block time** puts each block in the minute of its timestamp: our own mirror ([pulse-method-minute.csv](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/bot/pulse-method-minute.csv.METHOD.md)) read **3,645.9 tx/s** for the same minute. Kaspa Pulse's own count, by block time on two independent nodes, also reads 3,646 for 11:28Z, matching our block-time mirror (3,645.9). Our chain count, by when n2 saw each block, reads 3,583.1 for that minute. Same chain, a few boundary blocks shifted; totals over many minutes agree. Always say which bucketing a minute uses. Method sidecars for every published per-minute CSV: [tn10-storm-2026-10-11 logs](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/README.md#method-per-file), [tn10-storm-2026-10-10 logs](https://github.com/STP-KAS/tn10-storm-2026-10-10/blob/main/logs/README.md#method-per-file).

## Windows

Per block (one 0.1 s block, very spiky), per second, per minute (headline: median of complete minutes), per step or hold (mean and median). Always state the window. A 10-second or 20-second peak is not a sustained rate.

**Complete minute (11 Oct rule):** a chain-count row that covers exactly one UTC minute with at most 400 chain blocks; rows that lump several minutes (a boundary block missing or off the final chain, or a node freeze) count in the mean but not in the peak or median. In [chain-count.csv](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/bot/chain-count.csv) this is the column `headline_strict`.

## Why the gap matters

When submitted is above accepted, the excess sits in mempools. Mempools grow, fees rise, transactions are evicted or dropped on restart, and the "sent" figure looks good while nothing extra lands. Example: 6,321 tx/s submit-OK for 20 s, about 1,900/s seen accepted (6 Oct).

## How past storms labelled their numbers

| Storm | Their label | Means | Maps to |
|---|---|---|---|
| 2026-09-18-mining | no tx rate; blocks, `RouteIsFull` | — | not a tx rate |
| 2026-09-25 / r1 / r2 | "Network TPS", "Processed", 10-s peak | kaspad block-body counter | Processed (overstates) |
| 2026-09-26 r4 to r6 | "accepted tx/s" (runner) | own txs seen accepted | node-accepted (own) |
| 2026-09-26 r7 | "unique selected-chain accepted" vs "Processed" | both | network unique / Processed |
| 2026-10-01 | "included", best 1 / 10 / 60 min | own txs on the virtual chain | node-accepted (own) |
| 2026-10-02 gusto | "about 112 tx/s" snapshot | sender accepted | node-accepted (own) |
| 2026-10-06 / 07 | "submit-OK", "seen accepted", "included" | kept apart | submitted / node-accepted |
| 2026-10-07 mass ceiling | per-block payments × 10 bps | block reading | capacity, not a rate |
| 2026-10-08 | "submit / local accept" | locus | submitted / node-accepted |
| 2026-10-09 | "unique accepted" + duplicate share; **Kaspa Pulse "accepted in blocks"** | network | **network unique** |
| 2026-10-10 | "network unique accepted", median of complete minutes | chain count | **network unique (headline)** |
| 2026-10-11 | the same as 10 Oct, plus **Kaspa Pulse's "accepted in blocks" live per UTC minute** (from 10:48Z) | network | **network unique (headline)**; Kaspa Pulse counter as cross-check |

Source of the counters: [history/MASTER.md, "Counters are not the same"](history/MASTER.md#counters-are-not-the-same). Credit for the counter and the base-load figure: [credits/KASPA-PULSE.md](credits/KASPA-PULSE.md). Independent counts by Kaspa Pulse ([@gokugalax](https://x.com/gokugalax), [kaspapulse.com](https://kaspapulse.com)).
