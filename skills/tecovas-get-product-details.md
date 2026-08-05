# Get Product Details

Return full product detail for a single product, including variants, sizes, media, and inventory.

## Endpoint

`GET https://www.tecovas.com/api/productdetail/:slug`

`:slug` is the product handle (e.g. `mens-the-cartwright`).

## Response

JSON product object with `title`, `description`, `variants` (with `size`, `width`, `available`), `colorways`, `media`, `price`, `compareAtPrice`. Use this when an agent needs to confirm SKU, sizing, or stock before recommending.
