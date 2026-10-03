# Example 1: from one sentence to charters

## Input

> Checkout for the Sauce Demo store. The customer opens the cart, enters first name, last name and postal code, sees an overview with item total, tax and total, and confirms the order.

## Output

Ordered by what would hurt most if it were wrong: an order that should not exist, then wrong money, then lost state.

### Charter 1

Explore **checkout** with **empty carts and invalid customer details** to discover **whether an order can be placed that should have been refused**.

- Why it matters: a confirmed order is a promise to the customer and a record in the system.
- Starting ideas: check out with nothing in the cart; a single space in each field; digits as a name; free text as a postal code; each field empty in turn.
- Stop when: every field has been tried empty, whitespace only and with the wrong kind of value.

### Charter 2

Explore **the order overview** with **carts of one, several and all products** to discover **whether item total, tax and total always add up**.

- Why it matters: a wrong total is a wrong charge.
- Starting ideas: one cheap item; all six items; add, remove and add again before checkout; prices that produce a tax amount needing rounding.
- Stop when: the tax rule can be stated and has held for every cart tried.

### Charter 3

Explore **cart state during checkout** with **reloads, the back button, direct URLs and Reset App State** to discover **whether the page ever shows something different from what the cart holds**.

- Why it matters: customers lose trust when the cart changes under them.
- Starting ideas: reload on each checkout step; go back from the overview and change the cart; open the overview URL directly; reset state halfway through.
- Stop when: each checkout step has been interrupted at least once.

## What came of it

Following charter 1 leads to an order that completes with an empty cart, and charter 3 to a button that keeps the wrong state after a reset. Both are written up in the `qa-case-study-saucedemo` repository.
