# Delivery Goal: Evergreen Quote

## Goal

> By Thursday 12 November, the wired Evergreen Quote app saves quotes that survive a reload, the containerized API has run as three replicas on the local cluster with the app unchanged, and the launch is merged to main through a reviewed pull request with both CI jobs green.

**Spoken version:** *Saved quotes survive a reload, the API runs on the cluster, and it merges with both jobs green.*

## "Done" looks like

- The quote page loads its recent quotes from the API, and a saved quote survives a reload.
- The estimate on screen and the saved premium agree, at the launch rates.
- `npm test` (API) and `npm run type-check` + `npm run build` (client) pass; both CI jobs on the merge commit are **green**.
- The containerized API serves the wired app, and the cluster demo shows three API pods behind one Service.
- The landing page carries the launch banner and points at the app.
- A reviewed PR is merged, branch deleted.
- `delivery-leadership-package/` is complete and committed.

## Out of scope (this week)

- No renters coverage, no changes to application logic beyond the named configuration, no dependency upgrades.
- No public API or cross-origin access; no dependence on the cloud.

