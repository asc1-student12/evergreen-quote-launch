# Evergreen Quote Launch: Vision Brief

## Product
**Name:** Evergreen Quote launch (final capstone)
**Delivery Lead:** Scott Cannon (solo, with instructor approval)
**Engineering team (represented by):** https://github.com/asc1-student12/evergreen-quote-launch
**GitHub Project board:** https://github.com/users/asc1-student12/projects/4

## Who is the customer?
A first-time insurance shopper who lands on our marketing page and clicks "Get your quote" to get an idea, ut expecting they can come back at any time when they are ready to move forward and not lose where they were. These users are typically a new renter or homeowner on their phone, so the three pieces need to work as one.

## What pain does the launch remove?
"I saved a quote. Where did it go?" Phase 1 gave the shopper a page; Phase 2 made it a fast, typed app; Phase 3 built a service that stores quotes and computes the premium of record. But the app has never asked the service anything: it shows its own sample rows, and a saved quote vanishes on reload. Wiring them together changes one thing for the customer that matters more than everything else: the price they are shown is the price we keep, and it is still there when they come back.

## What does "good" look like at end of the week?
- The recent-quotes panel shows the six quotes from the database, q1 to q6, and a saved quote survives a reload with a premium the API computed.
- The estimate on screen and the saved premium agree for the same inputs, because the server is the source of truth.
- The marketing page's "Get your quote" opens the running app, with the launch title and banner set.
- The API runs as the `evergreen-quote-api:2.0` image and as three replicas on a local cluster, and the app talks to it without changing a line.
- Both CI jobs, the API tests and the client type-check and build, are green on the merge commit.

## What are we explicitly NOT doing this week?
- No renters coverage: deferred last week, and it would now span two validation systems across the stack.
- No changes to the engineering teams' application logic; only the configuration and content the launch names.
- No public API, authentication or cross-origin access; the client reaches the API through a development proxy.
- No real rate engine; rates remain a sponsor decision.
- No dependency upgrades: the lock files stay as the teams pinned them.
- No dependence on the cloud: the gated EKS window is optional, and the demo runs locally.

## How will we know if it worked?
- Zero difference between the on-screen estimate and the saved premium for the same inputs.
- A saved quote survives a reload in every environment the API runs in: the dev server, the container, and the cluster.
- 2 of 2 CI jobs green on the merge commit; API tests 7 of 7; client type-check 0 errors.
