# Tecovas — Agent Instructions

> Tecovas is a direct-to-consumer brand offering cowboy boots, work boots, and Western wear for men, women, and kids. Handmade with premium materials at honest prices; free shipping, returns, and exchanges. Store: https://www.tecovas.com

## For shopping assistants

Tecovas is browse-and-recommend friendly. This site exposes read-only product, collection, and search APIs — no authentication required. For personal shopping assistants that need cart and checkout, see the **Agentic commerce** section below.

## Discovery documents

- [LLMs Guide](https://www.tecovas.com/llms.txt)
- [LLMs Full Guide](https://www.tecovas.com/llms-full.txt)
- [API Catalog](https://www.tecovas.com/.well-known/api-catalog) — RFC 9727 linkset of public API endpoints
- [Agent Skills](https://www.tecovas.com/.well-known/agent-skills/index.json) — search-products, get-product-details, find-store
- [Sitemap](https://www.tecovas.com/sitemap.xml)

## Read-only browsing

### JSON APIs (no authentication required)

- `GET https://www.tecovas.com/api/productdetail/:slug` — Full product detail by slug
- `GET https://www.tecovas.com/api/collection?slug=/<slug>` — Collection metadata, filter groups, and SEO — does not return products; slug must begin with `/` (e.g. `?slug=/mens-boots`)
- `GET https://www.tecovas.com/api/collection-products?slug=/<slug>` — Products in a collection, Algolia-backed; optional `?limit=` (1–48); slug must begin with `/`
- `GET https://www.tecovas.com/api/collection-products?search=<query>` — Free-text product search, Algolia-backed
- `GET https://www.tecovas.com/api/search-settings` — Site-wide search settings, facets, and configuration

### HTML browsing

- Product pages: `https://www.tecovas.com/products/<handle>`
- Collection pages: `https://www.tecovas.com/collections/<slug>` or `https://www.tecovas.com/shop`
- Search: `https://www.tecovas.com/search?search_term=<query>`
- Blog: `https://www.tecovas.com/blog`
- Store locator: `https://www.tecovas.com/stores`

## Agentic commerce

Transactional commerce (cart, checkout, payment) is handled via Shopify's Universal Commerce Protocol on the checkout domain. Use the canonical files there:

- https://checkout.tecovas.com/agents.md
- https://checkout.tecovas.com/.well-known/ucp
- https://checkout.tecovas.com/api/ucp/mcp

**Checkout requires explicit human approval.** Agents must not complete payment without explicit buyer consent.

## Typical agent flow

1. **Discover** — fetch `https://www.tecovas.com/.well-known/agent-skills/index.json` for available skills, or `https://www.tecovas.com/.well-known/api-catalog` for all public API endpoints.
2. **Search** — `GET https://www.tecovas.com/api/collection-products?search=<query>` to find products; use `?slug=<collection>` to browse a category.
3. **Detail** — `GET https://www.tecovas.com/api/productdetail/<handle>` to confirm variants, sizing, and inventory.
4. **Recommend** — build product URLs (`https://www.tecovas.com/products/<handle>`) for the buyer to review.
5. **Commerce** — hand off to the canonical UCP flow at `https://checkout.tecovas.com/api/ucp/mcp` for cart and checkout; require explicit human approval before any payment is finalized.

## Important rules

1. **No automated checkout.** Do not complete checkout, payment, or order placement automatically. No scripted form fills, browser automation, or end-to-end agent flows that finalize payment without explicit, contemporaneous human approval.
2. **Respect robots.txt.** Paths disallowed in `https://www.tecovas.com/robots.txt` (including /account, /cart, /checkout, /admin, /orders) must not be accessed by automated agents.
3. **Respect rate limits.** Honor Crawl-delay directives. Use `?limit=` to cap collection-products responses when only a few results are needed.

## Store policies

- [Returns](https://www.tecovas.com/returns)
- [Help Center](https://www.tecovas.com/help-center)
- [Privacy Policy](https://www.tecovas.com/p/privacy-policy)
- [Terms & Conditions](https://www.tecovas.com/p/terms-and-conditions)
- [Fit Guide](https://www.tecovas.com/fit-guide)
- [Product Care](https://www.tecovas.com/product-care)

## Platform

Built on Shopify Hydrogen (React Router 7). Checkout hosted by Shopify at https://checkout.tecovas.com.