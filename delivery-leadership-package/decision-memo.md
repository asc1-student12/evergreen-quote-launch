# Decision Memo: Keep the instant estimate, with the server as the source of truth

**Date:** Day 2
**Author:** Scott Cannon, Delivery Lead
**Decision area:** Where the premium is calculated

## Context

Once the app was connected to the quote service, the same inputs showed two prices. The on-screen estimate said $425 and the saved quote said $450. Both sides were working correctly; they used different rate tables. The app calculates an instant estimate in the browser, while the service calculates the official premium when a quote is saved. The sponsor's instruction was clear: the server is the source of truth. I aligned the app's rates to the service's, so both now show $450. But the price is still calculated in two places.

## Options considered

1. **Keep both calculations, aligned.** The customer sees a price instantly as they type, and the saved premium remains the official one. The risk is that a future rate change updates only one side.
2. **Ask the service for every estimate.** One calculation, so the two prices can never differ. But every keystroke becomes a network request: slower, more load on the service, and no estimate at all if the service is down.
3. **Have the app fetch the rates from the service when it opens.** One rate table and an instant estimate. This is the best long-term answer, but it is new code, and this week is assembly only.

## Recommendation

Option 1 for the launch, and Option 3 for the next round. Keep the instant estimate, with its rates aligned to the service's, and treat the saved premium as the official price. Next round, the app should read its rates from the service, so there is only one rate table.

## Why

A first-time shopper decides in seconds whether a price is worth pursuing. An instant estimate keeps them engaged, while a network request on every keystroke would make the page feel slower and fail completely if the service went down. With the rates aligned and the service as the source of truth, the customer sees one price today. The remaining risk is a future rate change applied to only one side, and that is now logged and owned (risk R2).

## What would change my mind

If rates start changing often, or if a regulator requires the displayed price to be calculated by the same system that issues it, I would move straight to Option 3, or to Option 2 if Option 3 could not be ready in time.

