# Scratch log (raw, unpolished)

Mon Nov 9 20:15 - Platforms green: Node 22.22.0, Docker, kind, kubectl, mongosh ok:1, Live Server. AWS: no credentials at first; configured via aws configure (keys in ~/.aws, outside the repo). Found Monday, not Thursday.
Mon Nov 9 20:25 - Starter ships with NO .gitignore: THIRD PHASE IN A ROW. The guide says dist/ stays out of Git thanks to the .gitignore. Created one covering node_modules/ in api and client, and dist/. Caught before the first commit.
Mon Nov 9 20:30 - Repo created PUBLIC (the guide says private; reviewers need access). delivery/lead pushed.
Wed Nov 11 (Day 1) - THE GAP: the client recent-quotes panel shows its own bundled sample rows (numeric ids); the API serves six MongoDB documents (q1-q6). They do not match: the client has never called the API. Saved a quote, reloaded: gone. The page estimates; the service remembers; they have never met.
Wed Nov 11 (Day 1) - API: health ok, q1-q6 seeded, q1 auto 41 / 50000 at 96 (historical premium, older rate table). npm test 7/7 before any change. Client still titled Evergreen Insurance - Get a Quote (Phase 2 value). Landing: banner and quote links are CHANGEME.
Wed Nov 11 (Day 1) - npm install rewrote both api/ and client/ package-lock.json. Restored with git restore: committing them would slip an unrequested dependency change into the launch PR. Use npm ci (installs exactly from the lock, never rewrites it), as CI does. .gitignore verified: 0 node_modules entries after installing both packages.
Wed Nov 11 (Day 1) - Kit inconsistency: templates/task-list.md marks the Copilot critique P2 (stretch); the Peerceptiv deliverables list it as required. Treating it as required.
