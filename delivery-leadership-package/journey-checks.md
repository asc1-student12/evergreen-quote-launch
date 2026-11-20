# Journey Checks

One question per day, tying the day's work back to a phase of the program.

## Day 1: Phase 1

**Question:** You opened the week the way the program opened: a static page in Live Server, a terminal, a fresh repo, a branch. What could the product do at the end of Phase 1, and which part of today's run was exactly that?

**Answer:** At the end of Phase 1, Evergreen was a static site: a marketing page describing the coverage and a quote page that computed an estimate when the visitor pressed a button. Today's Live Server run of `landing/` was exactly that: a static page, no build step, no server of its own. The Phase 1 working method was there too: a fresh repo, a first commit, a delivery branch, and a `.gitignore` that I had to write myself because the starter did not include one.

## Day 2: Phase 2

**Question:** Today a type error crossed a network seam, and the fix was one line in a mapper, not a weakening of the contract. Which Phase 2 topic is that discipline, and where else today did a contract (TypeScript's, or the database's) hold a line for you?

**Answer:** It is the Phase 2 discipline of TypeScript contracts with the compiler as the quality gate, the same move as Phase 2's QA bug, where RecentQuotes read a field the Quote type did not have. This time the contract stood between two systems: `ApiQuote` described what the API really sends (`_id`), and the mapper was corrected to match it rather than the contract being loosened. Elsewhere today: the rate change was values only, because `BASE_RATES` is typed `Record<CoverageType, number>`, and on the database side the Mongoose schema still guards every write, whichever door it comes through, REST or the GraphQL mutation.

## Day 3: Phase 3

**Question:** The API answered from three homes today: a dev server, a container, a cluster, and the client never noticed. What, concretely, made that indifference possible, and which Phase 3 courses built each piece of it?

**Answer:** Three things. The client only ever calls relative /api URLs, and the dev proxy forwards them to whatever answers on port 3000, so the dev server, the container and the port-forward could take turns without the client knowing. Configuration travels by environment variable under fixed names: MONGODB_URI and SERVICE_NAME came from .env on the VM, from --env-file in the container, and from the Deployment env block in the cluster, and the code never changed. And the image is immutable: evergreen-quote-api:2.0 is the same bytes in Docker and on kind. Those pieces came from the Express and MongoDB weeks (environment-driven configuration), the Docker week (the image and its tag), and the Kubernetes week (the Deployment, the Service and port-forward).

## Day 4: the whole program

**Question:** If you could show your manager only one file from the merged diff to explain what this program made of you, which file, and what is the sentence you would say over it?

**Answer:** client/src/api.ts. "This is where two systems that had never met agree on what a quote is. The compiler found the one place they disagreed before any customer did, and the fix was one line that made the code match the truth, not the other way round."
