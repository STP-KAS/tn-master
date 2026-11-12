> **Experimental. We are just trying this.** [Disclaimer](DISCLAIMER.md) · [tn-master](README.md) · Kaspa Testnet-10 only; tKAS has no value.
>
> **This is the current playbook for the 11 November 2026 rehearsal and later pre-runs.** It is not Wednesday. It is not Tuesday. It does not start a machine and it does not arm one. It is taken from [pre-run 9's PLAYBOOK](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun-9/blob/485e4189a3f22c369956b9393dc3f57339d2d192/PLAYBOOK.md) (commit `485e418`) and updated with the lessons locked after that run. Live results stay in [FINDINGS.md](FINDINGS.md) and [history/storms/2026-11-11-prerun.md](history/storms/2026-11-11-prerun.md).

# Playbook

Who does what, and the gates before each machine may start. A pre-run's own plan, lock, and go files, when it has them, are not overridden by this page.

## Oversight

TN10 ops oversees this rehearsal end to end: Mini, the desk (Build), and the bot. TN10 only. Never mainnet. Do not edit the Tuesday repo, the Wednesday repo, or a closed pre-run's go files. Do not write `REVIEW_CLOSED`.

The operator's start is the arm. From pre-run 3 on, that start was his instruction to go, not a paste in chat. The agents start their runners once the gates are facts.

## Start gates

1. **Mini node synced.** Existing TN10 kaspad, existing data, no wipe. `isSynced` true, DAA moving. If that kaspad is down, start it from its existing data. Do not wipe.
2. **Desk node synced.** Existing private TN10 kaspad, existing data, loopback only, started with `pwsh` (PowerShell 7), never Windows PowerShell 5.1. No wipe. Synced, DAA moving. Do not start `KaspaPublicNode`. Leave the desk devnet alone. A pre-run does not stop the desk node process.
3. **No other runner.** No earlier runner, waiter, or counter on any machine. Lane above the abort line (2,500 coins and 18,000 usable tKAS). **The desk's private candidate list is present and not empty** (`HELD candidates-missing` otherwise). That open check was locked after pre-run 8 (the first open of that run read a hold when the private folder had no candidates file).
4. **Hashes first.** `hashes/SIXTEEN.md` with sixteen rows and an On origin line, from that repo's sixteen-family publisher. Genesis launch paths begin `launch::storm-2026-10-`. A hash is never invented. The old 8- or 32-family publisher is not used for this rehearsal.
5. **Open.** The desk pushes `logs/PRE-RUN-OPEN.md`. Mini then pushes `logs/MINI-ARMED.md`. Mini does not publish `MINI-ARMED` unless its node is synced with DAA moving.
6. **Counter, families, senders.** The desk runner starts the counter on its private node and waits for its start line (`HELD counter-down` otherwise). Then the genesis from the bundle that wrote `hashes/SIXTEEN.md`, the families, and the payment steps.

## Who does what

| Who | Role | What not to do |
|---|---|---|
| **Desk (Build)** | Sends the covenant families and the payment offers. Its private TN10 node counts what the chain accepted (the inclusion figure for pre-runs 8 and 9). Publishes `hashes/SIXTEEN.md`, `logs/PRE-RUN-OPEN.md`, `counts/desk/` per step, `counts/chain/TIMELINE.md` after the tail, and `logs/METHOD.md`. | Do not stop or wipe the desk node. No Windows PowerShell 5.1, no `KaspaPublicNode`, no devnet. No 8- or 32-family publisher. No second runner. Never restart the runner mid-run to apply a fix. |
| **Mini** | Second chain read on its own node. Does not send, mine, or hold a key. Publishes `logs/MINI-ARMED.md`, then `counts/mini/` when the matching desk file is on origin. Each head is Mini's own read: `READ`, `PARTIAL`, or `NOT READ`. | Do not wipe. Do not repeat the desk's head as Mini's. Until `classify()` is fixed offline to one hop per transaction, Mini's hop columns are not a comparable second read (see [FINDINGS.md](FINDINGS.md) item 30). |
| **Bot (TN10 ops)** | Sends payments in the HOLD-4 minute only, on a synced public kaspad that is not one the desk kept, or publishes a legal `NO SEND`. | Do not send on HOLD-1, HOLD-2, HOLD-3, or RETURN. One waiter. No local node. A waiter does not outlive its run. |

## Lines that stay, from the pre-runs

These are the worked lines we carry forward. The lock files in the pre-run repos are the source.

- A runner is never restarted mid-run to apply a scoring or tooling fix. The run is left alone and the fix goes into a later repo. If a runner must ever be replaced, its children are started detached so they survive the parent. (Pre-run 2.)
- A family STALL (no hop of that family landing for a while) is logged and is not dirt for HOLD scoring. (Pre-run 2.)
- The desk runner is rehearsed offline through HOLD-1 scoring, with faked logs and no live send, before a live run. A dry start that only reaches the gate check is not a rehearsal. (Pre-run 3.)
- Kept public nodes are unique kaspads, not unique hostnames. Two hostnames with one node id count as one node and get the senders for one kaspad. The bot's free node must be a different kaspad, read in the same pass. If none is free and synced, the bot writes a legal `NO SEND` and `no-free-node`. In this rehearsal only two unique public kaspads answered our checks, so HOLD-4 was a `NO SEND` from pre-run 5 on. A third kaspad is used only if it answers synced with its own node id. (Pre-runs 4–9.)
- After a payment-sender repair, the missing senders are actually started. The runner waits until the stopped senders are gone, takes them off its list, starts the ones that are missing, and checks that each one logged its start. (Pre-run 4.)
- A failed push of a HOLD file or of `logs/FAILED.md` is retried. A FAILED file is written locally first. If origin still refuses, the operator publishes the local file. (Pre-run 4.)
- A payment sender that restarts mid-run must not take its pool from the confirmed UTXO set alone while its chains are in the mempool. The repair hands pools off; the deal total must not exceed the preflight pile; the even split is checked after a reload. A payment ceiling is read against the pile size before it is called a node or network limit. (Pre-runs 5–6.)
- A family sender's mempool skip must clear when the node's mempool falls back under the line, or the skip must not apply to the families. A skip is logged. In pre-run 6 a one-way `mempool_90k` skip stopped all sixteen families from 20:31Z and made RETURN read not met even though the payments were on target. (Pre-run 6, fixed for pre-run 7.)
- Three payment senders per kept unique kaspad, once the pile is large enough that the cap has moved off the pile. (Pre-run 7.)
- The desk's private TN10 node is the inclusion counter when Mini cannot keep up. The desk node is not stopped for that count. (Pre-runs 7–9.)
- Offers and fee cohorts are chosen for the question of that pre-run and are locked in that repo before the arm. Pre-run 9 used HOLD-1 1,013, HOLD-2 1,800, HOLD-3 2,500, then dropped to 1,013 as soon as HOLD-3 was scored, so the over-capacity stretch stayed short. Scoring stays three clean minutes of submit-OK, or `NOT MET` after one repair. Inclusion is reported next to it and is not the score.
- Family keys are funded again before a next repo publishes a new hash file. Pre-run 9's playbook recorded that keys 1–15 had no genesis coin left at the end of that run. We did not re-read those wallets for this page.

## When something breaks

Append a worked fix to that pre-run's `locks/LOCKED.md` in the form that page shows, and a repair line to `logs/FIXES.md` if the runner uses it. If the run dies before RETURN, write `logs/FAILED.md`, stop every runner, waiter, and counter, and do not resume. The next attempt is a new repo that starts from that repo's lock file. The result, or the miss, is also written into this map ([docs/NEURON.md](docs/NEURON.md)).
