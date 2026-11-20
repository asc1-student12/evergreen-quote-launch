# Copilot-Assisted Step and Critique

**Author:** Scott Cannon, Delivery Lead · **Day:** 3
**Tool:** GitHub Copilot in VS Code, the program's approved assistant
**Prompt:** "Add two more seed quotes to this list, matching the existing shape and the Mongoose schema in api/src/Quote.js."
**Evidence:** `copilot-seed-diff.txt` (Copilot's exact output)

## Critique

Copilot got the shape right: two new quotes with unique ids, valid coverage types, ages inside the schema's limits and numeric premiums, and the schema accepted both. What it got wrong was everything it was not asked to do. It edited the file's header comment from "six known quotes" to "eight," invented a new tag value that no one had defined, and made up premiums with no basis in any rate table: life cover of $500,000 at $210 a month, where today's rates give $3,500. They look like the existing historical premiums because Copilot copied the pattern, not the pricing logic. I would not ship its rows.

## Accepted, adapted or rejected

**Rejected.** I restored `seed.js` to the platform team's original. The rows were valid to the schema but not fit to ship, and editing the team's seed file is outside this week's scope.

## Which gates would catch a bad row, and when?

I tested this rather than assuming it. I changed one of Copilot's rows to age 12. **Running the seed:** the Mongoose schema rejected it, but only at runtime, when the seed actually ran. **The test suite:** still green, 7 of 7. TypeScript never reads `seed.js`, and the CI tests check the routes, not the seed data. So a bad seed row would merge with green CI and fail only when someone ran the seed, possibly on demo morning.

## Data handling

Copilot saw only the prompt and the open file: sample quote data, with no customer information or credentials.
