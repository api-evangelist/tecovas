# Search Products

Run a free-text search against the Tecovas catalog. Backed by Algolia.

## Endpoint

`GET https://www.tecovas.com/api/collection-products?search=<query>`

## Query parameters

- `search` — free-text query (e.g. `brown roper boots`)
- `limit` — optional, 1–48 (default unbounded)

To list products in a specific collection instead of running a search, use `?slug=<collection-slug>` (e.g. `?slug=mens-boots`) instead of `?search=`.

## Response

`{products: [...], queryID?: string}` — array of product cards with `title`, `handle`, `price`, `images`, `colorways`, `availableForSale`. Use the `handle` to construct a PDP URL (`https://www.tecovas.com/products/<handle>`) and to call `get-product-details`.
