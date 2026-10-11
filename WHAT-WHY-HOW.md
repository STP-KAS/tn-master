> **Experimental. We are just trying this.** [Disclaimer](DISCLAIMER.md) · [tn-master](README.md)

# What, why, how

## What

A **storm** is a load test on Kaspa **Testnet-10** (TN10). Many sign-and-send processes (**senders**) push simple transactions at nodes for hours, while loggers record what was sent, what nodes accepted, and the state of the nodes and the machine. Afterwards we count, from the chain, what the network really accepted. Two sides ran most storms from October: **the bot** (Grok Bot's box, own node n2) and **Build** (Grok Build on stp's desk, own node). Wording (Kaspa Pulse, 7 Oct): **senders** sign and send, the **runner** is the setup, **bot** is reserved for the operator.

## Why

- To see where TN10 flattens: how many transactions per second the network really accepts, and what breaks first (nodes, mempools, indexers, disks, fees).
- To give builders numbers they can use: fees under congestion, re-broadcast after restarts, coin selection ([ADVICE-TO-DEVELOPERS.md](ADVICE-TO-DEVELOPERS.md)).
- To separate "sent" from "accepted". Dashboards and sender logs flatter; the chain does not ([METRICS.md](METRICS.md)).

## How

- **Nodes.** Each side runs its own private, pruned (non-archival) TN10 kaspad. The bot submits to the five public TN10 community nodes and uses n2 for reads, coins, the chain count and one miner. No tunnels between sides since 10 Oct.
- **Senders.** Lanes of pre-split coins; light no-signature hops (anyone-can-spend, not realistic payments) on the bot side; fee tiers in sompi/gram; a rate target per step or a flat-out target.
- **Clock.** One UTC clock and one T0 for both sides (lesson of 10 Oct). Every log is per UTC second or minute.
- **Rules.** Kaspa Pulse's **node-dead rule**: a sender stops when its node is dead, and a failed submit is a reject, never sent. Disk and RAM guards. No fee above the cap unless stp says so (logged as a deviation).
- **Counting.** After END, the **chain count** from our own node, per UTC minute, before pruning (Kaspa Pulse's fix). The headline is **network unique accepted tx/s**: each transaction id once, when the virtual chain accepts it. Kaspa Pulse counts each run independently with **accepted in blocks, two independent nodes, per UTC minute, by block time**; from 11 Oct we also log his method live. Every network count includes about 56 tx/s base load (Kaspa Pulse).
- **Publishing.** Raw CSVs in each storm repo's `logs/`, a COMBINED.md and a WRITE-UP.md; counts only, leak-scanned.

Thanks to Kaspa Pulse ([@gokugalax](https://x.com/gokugalax)) for the method: [credits/KASPA-PULSE.md](credits/KASPA-PULSE.md).
