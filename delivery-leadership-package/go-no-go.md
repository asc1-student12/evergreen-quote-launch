# Go / No-Go: Friday's Launch Demo

**Date / time:** Day 3, after Inject #2
**Decision:** ☐ GO   ☐ NO-GO   ☑ **GO WITH CONDITIONS**

## Evidence, by environment

The decision depends on keeping three environments separate.

| Environment | Owner | What the evidence shows | Status |
|---|---|---|---|
| **My launch stack:** the kind cluster `evergreen` on my VM | Me | Three API pods and the database `1/1 Running`; the manifest and the application both use `MONGODB_URI` (`incident-own-environment-check.txt`) | ✅ Healthy |
| **My CI:** the two-job pipeline | Me | Latest run green on both jobs, Test the API and Type-check and build the client: https://github.com/asc1-student12/evergreen-quote-launch/actions/runs/44652771899 | ✅ Green |
| **The shared demo environment:** the `demo` namespace | Platform team | API pods in `CrashLoopBackOff`; the deployment injects `MONGO_URI` where the application reads `MONGODB_URI`; the database pod itself is healthy (`incident-comms.md`) | ❌ Broken |

## What the workflow checks

On every push: install from each lock file with `npm ci`; run the API's test suite against a throwaway `mongo:7` database; run the client's type-check; and produce the client's production build.

## What "GO" means

- Friday's demo runs on my stack, exactly as set out in `demo-plan.md`.
- The launch PR is merged to `main` once both CI jobs are green on the PR, and green again on the merge commit.

## What "NO-GO" would mean

- Hold the merge and the demo until my own stack and CI are green again.
- Owner: me. I re-check before opening the PR, and again on the morning of the demo.

## My call

**GO WITH CONDITIONS.** Friday's demo runs on my own stack, and both pieces of evidence for it are green: my cluster is running and my two-job CI run passed. The shared demo environment is genuinely broken, and that incident is real. But it belongs to the platform team, it is tracked, and Friday's demo does not depend on it. Treating someone else's broken environment as my blocker would be the wrong call; pretending the incident does not exist would be the other wrong call.

**Conditions:**

1. Both CI jobs are green on the launch PR, and again on the merge commit.
2. The demo rehearsal passes on my stack, following `demo-plan.md`.
3. Nothing from the shared demo environment enters my merge path or my demo.

**The shared incident** is routed to the platform team with the evidence and a question (`incident-comms.md`), and the manager who reported it has a holding message and a time for the next update.

## What would change my mind

- **My own CI goes red, or my cluster fails the rehearsal:** NO-GO on the merge until it is green again.
- **The platform team says the rename is a new standard,** meant to apply to every deployment: then it would reach my manifest too. I would hold the merge and agree the variable name with them first, because the application reads `MONGODB_URI`.

**Re-evaluate:** before opening the launch PR, and again at 13:00 on the day of the demo.
