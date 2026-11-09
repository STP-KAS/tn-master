> **Experimental. We are just trying this.** [Disclaimer](../DISCLAIMER.md) · [tn-master](../README.md)
>
> This page is the rule for every storm from 9 Nov 2026 on. It does not start a machine. When a test is about to start, read this page first.

# Every neuron uploads

A **neuron** is one storm. One repo. One clock. One question. The name is `tn10-storm-YYYY-MM-DD`, plus a suffix when that date already has a repo.

The operator's start line is: go to tn-master and read the rules. This page is that page. [docs/LESSONS.md](LESSONS.md) is the operations list. The neuron's own `RULES.md` is the clock.

## The day the repo is created

tn-master gets all of these before anyone is asked to paste a go file:

- a row in [repos/INDEX.md](../repos/INDEX.md)
- a page in [history/storms/](../history/storms/README.md)
- a line in [history/TIMELINE.md](../history/TIMELINE.md)
- a row in the glance table of [history/MASTER.md](../history/MASTER.md)
- a line on [README.md](../README.md)

A plan, a miss, and a finish all get the row. An empty window stays in the index.

## The hour the clock closes

The desk runner, the same day, writes the result into those same pages and pushes tn-master.

- The index row says RAN or FAILED, and it links the method file or the failure file.
- The history page gains the numbers that are already public in the storm repo, or the statement that the window did not run.
- The plan pages inside the storm repo are not rewritten to match the result.
- The row is not deleted because the night failed, and it is not delayed because the night went well.

If the runner dies before that push, the desk session does it before logout. The next morning is late. Say so in the history page.

## What a later neuron inherits

- Two or three pastes. Each paste is the whole story. The first sentence names the machine. The operator sends the paste. That send is the arm.
- One runner per machine. Git by its full path. Empty git output is a failed read.
- The desk publishes `counts/desk/`. Mini publishes `counts/mini/`. A hash file shows Fixed and On origin, and On origin is read from origin.
- Counts only. No key, seed, txid, covenant id, address, host, or port.
- A miss keeps its clock. The next attempt is a new repo.

Tuesday 10 Nov 2026 stays Tuesday. Wednesday 11 Nov 2026 is [tn10-storm-2026-11-11](https://github.com/STP-KAS/tn10-storm-2026-11-11). It is not a spare rerun of Tuesday.
