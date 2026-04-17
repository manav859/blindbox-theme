# Blind Box Storefront Guide

## Audit Summary

### What existed

- Product page:
  `sections/main-product/main-product.html`
  already contained a tag-gated blind-box panel, native product form, media gallery, and supporting cards.
- Collection page:
  `sections/main-collection/main-collection.html`
  rendered a clean product grid but had no blind-box card treatment.
- Cart page:
  `sections/main-cart/main-cart.html`
  supported quantity editing and checkout, but had no blind-box messaging.
- Reusable assets:
  `components/blind-box-badge-icon/blind-box-badge-icon.html`
  existed and was reusable.
- Optional block:
  `blocks/blind-box-note.html`
  existed, but its default copy exposed backend implementation language.

### UX issues found

- The product page mixed a standard purchase card with a separate blind-box shell, which created two competing purchase experiences.
- Blind-box copy referenced backend assignment mechanics too explicitly for a storefront surface.
- Above-the-fold hierarchy was too busy around the purchase decision.
- Collection cards and cart lines did not explain blind-box items early enough.
- The existing detection logic supported multiple tags, which increased merchant ambiguity.

### What was reusable

- Product gallery and thumbnail interactions
- Native SHOPLINE product form and cart flow
- Existing badge icon component
- Shared theme layout, card styling, and section structure

### What changed

- Product page was refactored into one primary purchase flow using the native product form only.
- Blind-box messaging now focuses on shopper clarity:
  one surprise item after payment, no manual selection, based on availability.
- Collection cards now show a blind-box badge and short surprise-item label.
- Cart lines now show a minimal blind-box note without revealing any reward.
- A shared blind-box detection helper was added for consistent behavior across product, collection, and cart.

## Detection Rule

The theme uses one detection rule only:

- Product tag: `blind-box`

Shared helper:

- `public/blind-box-theme-core.js`
- Global helper name: `window.BlindBoxTheme.isBlindBoxProduct(product)`

The helper normalizes the tag list and is used by:

- `public/blind-box-product-shell.js`
- `public/theme-interactions.js`

## Merchant Setup In SHOPLINE

To enable blind-box UI for a product:

1. Open the product in SHOPLINE admin.
2. Add the tag `blind-box`.
3. Make sure the product title, price, media, and description are complete.
4. Publish the product to the storefront as a normal SHOPLINE product.

To keep the experience clear:

- Use strong product imagery.
- Keep the product description focused on the collection, packaging, shipping, and what customers should expect.
- Do not add reward-selection copy to the product page.

## Theme Responsibilities

The theme handles:

- Detecting blind-box products by tag
- Showing blind-box badge and trust messaging
- Explaining how the blind-box purchase works
- Preserving the native SHOPLINE cart and checkout flow

The theme does not handle:

- Reward selection
- Randomization
- Assignment logic
- Post-payment fulfillment logic
- Custom checkout

## Reusable Components Added

- `components/blind-box-badge/blind-box-badge.html`
- `components/blind-box-info-block/blind-box-info-block.html`
- `components/how-it-works-block/how-it-works-block.html`
- `components/cart-blind-box-note/cart-blind-box-note.html`

Supporting assets:

- `public/blind-box-theme-core.js`
- `public/blind-box-product-shell.js`
- `public/blind-box-product-shell.css`

## Where The UI Was Applied

- Product page:
  `sections/main-product/main-product.html`
- Collection page:
  `sections/main-collection/main-collection.html`
- Cart page:
  `sections/main-cart/main-cart.html`
- Home messaging cleanup:
  `sections/storefront-home/storefront-home.html`

## Notes

- Normal products remain on the standard storefront flow.
- Blind-box CTA copy and explainer text are configurable in the product section settings.
- The cart note intentionally stays minimal:
  `Blind box item. Reward assigned after payment.`
