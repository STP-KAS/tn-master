# Kaspa Pulse's count, 11 Oct 2026, 07:30-12:30 UTC

Credit: Kaspa Pulse ([@gokugalax](https://x.com/gokugalax), [kaspapulse.com](https://kaspapulse.com)). Published with his OK (12 Oct 2026). Credit him when you reuse it.

**Method:** tx accepted in blocks, two independent nodes, per UTC minute, bucketed by block time; every minute confirmed by both nodes. Includes ~56 tx/s TN10 base load. Testnet-10 only. Counts only. All times UTC (CEST = UTC+2).

**Window:** 07:30-12:30Z, 300 full minutes. Mean **2,844**, median **3,055**, best minute **3,646 tx/s** (11:28Z), **51.2 million** accepted, 163 minutes above 3,000 tx/s.

| File | What |
|---|---|
| [pulse-vs-ours-1110.csv](pulse-vs-ours-1110.csv) | Minute-by-minute comparison, 07:30-12:33Z. Columns `pulse_*`: his count; `ours_*`: our chain count (n2, by n2 receive time); `ours_blocktime_*`: our live mirror of his method (from 10:49Z); `diff_tx_s` on our 171 strict minutes. The header lines of the file explain every column. |
| tn10-2026-10-11-0715-1244-accepted.csv | His own per-minute file, unchanged. **To be added** (not yet on our side). |

Our count and his agree within 0.1% over the run. Side by side: [logs/COMBINED.md](https://github.com/STP-KAS/tn10-storm-2026-10-11/blob/main/logs/COMBINED.md#ours-vs-kaspa-pulse).
