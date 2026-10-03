# Example 2: from notes to a bug report

## Input

```
saucedemo standard_user chromium
empty cart -> checkout btn still works
filled Ada / Lovelace / 01010 -> continue
overview: Item total $0, Tax $0.00, Total $0.00
finish -> "Thank you for your order!"
```

## Output

**Title:** An order can be placed with an empty cart

**Severity:** Critical (proposed). The store confirms an order that contains nothing.

**Environment:** https://www.saucedemo.com, Chromium, account `standard_user`

**Steps**

1. Log in as `standard_user` with an empty cart.
2. Click the cart icon.
3. Click Checkout.
4. Enter `Ada`, `Lovelace` and `01010`, then click Continue.
5. Click Finish.

**Expected**

Checkout is not available while the cart is empty, or the user is told to add a product first. Source: tester's judgement; no requirement was provided.

**Actual**

The overview shows "Item total: $0", "Tax: $0.00" and "Total: $0.00". Finish shows "Thank you for your order!".

**Impact**

Customers can create empty orders. On a real store each one produces an order record and a confirmation.

**Evidence**

None attached to the notes.

**Open questions**

- Which date and browser version was this seen on?
- Is there a requirement that says what checkout should do with an empty cart?
- Was a screenshot taken of the overview and the confirmation?

## What to notice

The expected result names its source as the tester's judgement, because the notes gave no requirement. The missing date, browser version and screenshots are listed as open questions instead of being filled in. The finished report, with evidence, is BUG-01 in the `qa-case-study-saucedemo` repository.
