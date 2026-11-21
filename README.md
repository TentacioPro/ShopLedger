# ShopLedger workshop — Abishek M

ShopLedger is a small Node.js point-of-sale app that tracks inventory, customer credit (Khata), and GST invoices. For the GeeksforGeeks × OpenAI workshop, I took the app through the explain, diagram, test, fix, and pull request checkpoints.

[View the workshop fixes](https://github.com/TentacioPro/ShopLedger/tree/fix/shopledger-workshop) · [Review the combined pull request](https://github.com/JayanGupta/ShopLedger/pull/20)

## What I fixed

| Issue | Change | Verified result |
| --- | --- | --- |
| [#1 Invoice and GST](https://github.com/JayanGupta/ShopLedger/issues/1) | Reused checkout pricing for GST slabs, capped coupons, and invoice totals. | The GST audit went from **7 of 8 mismatches to 0 of 8**. Invoice #1002 matches the billed ₹963.90. |
| [#2 Stock and cancellation](https://github.com/JayanGupta/ShopLedger/issues/2) | Allowed sales of the exact sellable quantity, counted repeated SKU lines together, and restored physical stock on cancellation. | The last sellable unit can be bought, and cancellation returns stock once while preserving wholesale holds. |
| [#3 Order history and Khata](https://github.com/JayanGupta/ShopLedger/issues/3) | Used chronological date keys and normalized payments before updating balances. | A January filter returns only January orders. A ₹500 settlement reduces ₹1,232.01 due to ₹732.01. |

## How I verified it

I captured the original behavior with in-memory fixtures, ran new regression tests before making the fixes, and checked the results in an isolated copy of the app. The final `node --test` run reported **15 passed, 0 failed**. The fix branch adds no dependencies and contains no changes to `data/db.json`.

- [Architecture diagram](https://github.com/TentacioPro/ShopLedger/blob/fix/shopledger-workshop/docs/architecture.svg)
- [Workshop repository instructions](https://github.com/TentacioPro/ShopLedger/blob/fix/shopledger-workshop/AGENTS.md)
- [Regression tests](https://github.com/TentacioPro/ShopLedger/tree/fix/shopledger-workshop/test)

## Run the fixed version

Use Node.js 22 or newer.

```sh
git clone --branch fix/shopledger-workshop https://github.com/TentacioPro/ShopLedger.git
cd ShopLedger
npm install --no-package-lock
node --test
npm start
```

Open [localhost:3000](http://localhost:3000/). Checkout, cancellation, and settlement actions update the local `data/db.json` in that clone.

Workshop submission by [Abishek M](https://github.com/TentacioPro). The original exercise is maintained in [JayanGupta/ShopLedger](https://github.com/JayanGupta/ShopLedger).

