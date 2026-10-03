# Example 3: a test that was green on two browsers

This test from my Playwright framework passed on Chromium and Firefox and failed on WebKit.

## Before

```ts
test('product detail page shows the same name and price as the list', async ({ inventoryPage, page }) => {
  const first = inventoryPage.items.first();
  const name = await first.getByTestId('inventory-item-name').innerText();
  const price = await first.getByTestId('inventory-item-price').innerText();

  await first.getByTestId('inventory-item-name').click();

  await expect(page).toHaveURL(/inventory-item\.html/);
  await expect(page.getByTestId('inventory-item-name')).toHaveText(name);
  await expect(page.getByTestId('inventory-item-price')).toHaveText(price);
});
```

The failure on WebKit:

```
Error: strict mode violation: getByTestId('inventory-item-name') resolved to 6 elements
```

## What the review found

**Will cause flaky failures.** `toHaveURL` is used as proof that the detail page has loaded. The store is a single page app: it changes the URL first and renders the new view afterwards. For a moment the URL says "detail" while the page still shows the list of six products. The next locator matches all six names and strict mode fails. Chromium and Firefox happened to render fast enough to hide it.

A second test had the same cause in another form. It read the item prices on the order overview with `allTextContents`, which does not wait, right after clicking Continue. On WebKit it read an empty list and compared a subtotal of 0 with the page's 39.98.

## After

```ts
  await first.getByTestId('inventory-item-name').click();

  // The URL changes before the detail view renders, so wait for a detail-only control.
  await expect(page).toHaveURL(/inventory-item\.html/);
  await expect(page.getByTestId('back-to-products')).toBeVisible();
  await expect(page.getByTestId('inventory-item-name')).toHaveText(name);
  await expect(page.getByTestId('inventory-item-price')).toHaveText(price);
```

For the overview, the page object got a method that clicks Continue and waits for the Finish button before anything is read.

## Verification

The full suite was run with `--repeat-each=2` on Chromium, Firefox, WebKit and a mobile viewport: 139 of 139 passed.

## Why this example is here

Both patterns are in the `playwright-test-review` checklist, under "Waiting and timing". The code reads naturally and passes on the browser it was first tried on, which is why it survives review so easily.
