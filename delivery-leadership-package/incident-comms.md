# Incident Response: Inject #2, the shared demo environment

**From:** Scott Cannon, Delivery Lead · **Day:** 3, ~14:00 · **Channel:** #incidents

## What the evidence shows, in plain English

The shared demo environment is down: its three API pods keep restarting because they cannot find the database, while the database itself is healthy. The deployment there now carries a variable named `MONGO_URI`, but the application reads `MONGODB_URI`. With the name it expects missing, each pod looks for a database inside itself, is refused, and restarts.

Three details support that reading:

- **The database is fine.** The `mongo` pod is `1/1 Running` with zero restarts, and has been up for almost six days.
- **The API never asked the real database.** The refused address is `127.0.0.1`, the pod itself, not `mongo`.
- **The timing lines up.** The API pods are 32 minutes old, matching the variable rename "about 30 minutes ago": renaming a variable rolls out new pods.

## Which environment is broken, and which is not

- **Broken: the shared demo environment**, the `demo` namespace on the platform team's cluster. The platform team owns it, and I am not changing it.
- **Healthy: my launch stack**, verified at the time of the incident (`incident-own-environment-check.txt`). My cluster's API pods and database are all `Running`; my latest two-job CI run is green; and both my manifest and the application use `MONGODB_URI`, so my environment cannot have this fault.
- **Friday's demo runs on my stack**, as set out in `demo-plan.md`. It does not depend on the shared environment.

## Message 1: to the platform team (owner of the shared demo environment)

Hi, platform team. The shared demo environment's API has been restarting since about 13:25, and the quote page there shows "Could not load recent quotes." Your capture shows the three API pods in `CrashLoopBackOff` with the database pod healthy; the API is refused at `127.0.0.1`, so it is not reaching the `mongo` service at all. The deployment's environment now lists `MONGO_URI`, but the application reads `MONGODB_URI`, and the restarts began with this afternoon's variable-name tidy-up. **Can you confirm whether the rename is the cause, and restore the name the application reads, with a time by which it will be back?** I have not changed anything in that environment. If it helps, my own cluster's manifest shows the working configuration, and I can share it.

## Message 2: to the manager who reported it

Thanks for flagging this, and for the dry run. Here is what we know. The shared demo environment is down because of a configuration change made there this afternoon; the platform team owns that environment and is looking at it now. **Friday's launch demo does not run on that environment.** It runs on my own stack, which I checked at the time of your report: the service and database are running, and the latest automated checks are green. So Friday is not at risk from this. I will update you by 17:00 today, or sooner if the platform team confirms the fix.

