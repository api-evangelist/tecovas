# Find Store

Look up Tecovas retail stores. Use this when a user asks "is there a store near me" or "where can I try on boots".

## Pages

- All stores: `https://www.tecovas.com/stores`
- Single store: `https://www.tecovas.com/stores/<slug>` (HTML; structured data in JSON-LD)

## Notes

There is no JSON store API at this origin today; the `/stores` page contains the canonical list and can be parsed. Each store page also exposes JSON-LD with address and hours.
