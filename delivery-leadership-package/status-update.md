# Stakeholder Status Update: Evergreen Quote Launch

**To:** Priya Ramanathan, Project Sponsor
**From:** Scott Cannon, Delivery Lead
**Date:** Day 2 (Inject #1 response)

## What shipped today

- **The app and the quote service are connected.** The quote list now comes from the database, and a saved quote is still there after a reload: the first quote in the program to survive a reload.
- **The type-check caught a defect at the join before anyone saw it.** The app read a field the service never sends; a one-line fix, and the check is clean.
- **One price on screen.** The estimate and the saved quote disagreed ($425 against $450) because the app still had last phase's rates. Following your instruction that the server is the source of truth, I aligned the app's rates as configuration, and both now show $450.
- **Launch configuration is set:** the app's title, and both "Get your quote" links on the marketing page now open the app.
- **The partner door is open:** GraphQL is mounted, and a life quote created through it priced correctly at $700.

## What slipped (and why)

- Nothing against the delivery goal.
- **Life-first, split into two decisions.** I approved and made the content change: the marketing page's banner and headline now lead with life coverage. The form's default is a different kind of change. It is one word, but it sits in the engineering team's estimate hook, which every quote flows through, two days before launch. I have routed it to the client team with the launch date attached, rather than changing it myself.
- **Renters is not in this launch.** It now crosses two validation systems, the app's type rules and the database's rules, and the service rejects it today. No renters rate exists yet. It is on the board for the next round.

## What's next

- Package the service as a container, demonstrate it on the local cluster, and turn on the two-job pipeline.
- **The demo plan, in writing** (`demo-plan.md`): the Friday demo runs locally on my machine. The cluster is rebuilt from the repo that morning, the app opens from the marketing page, and screenshots stand by as a fallback. Nothing depends on the cloud.

## What I need from you

1. **Confirm the life-first banner and headline wording by 10:30 tomorrow**, or send changes.
2. **A decision from the client team on the form default by end of day tomorrow.** If none arrives, it becomes the first change after launch.
3. **A renters rate**, before the next round can start.
4. **Acknowledgement from the platform team** that the local demo plan works for them.

