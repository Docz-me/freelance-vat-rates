# freelance-vat-rates

> Open dataset: VAT, GST and sales-tax rates by country, for freelancers and the tools they use.

A small, hand-verified JSON dataset of consumption-tax rates relevant to freelancers and independent professionals. Maintained by [Docz.me](https://docz.me) — the all-in-one freelance toolkit.

If you build invoicing software, accounting tools, or freelancer dashboards, this saves you the work of stitching together OECD PDFs and government tax-authority pages.

## Data

[`data.json`](./data.json) — array of country records.

### Schema

```ts
type CountryVat = {
  country: string;             // kebab-case ISO-style slug, e.g. "united-kingdom"
  standard: number | null;     // standard VAT/GST rate (%) — null if no national VAT (US, HK)
  reduced: number[];           // reduced rates (%) for specific goods/services
  zero: boolean;               // true if the country effectively has no consumption tax
  notes: string;               // freelancer-relevant context, registration thresholds, edge cases
  source_url: string;          // primary government / tax-authority source
  verified_date: string;       // ISO date when the entry was last verified
};
```

### Example

```json
{
  "country": "united-kingdom",
  "standard": 20,
  "reduced": [5],
  "zero": false,
  "notes": "Standard rate 20%. Reduced 5% for energy, child car seats, etc. Registration threshold £90,000/year. Below threshold, freelancers typically don't charge VAT.",
  "source_url": "https://www.gov.uk/vat-rates",
  "verified_date": "2026-04-24"
}
```

## Usage

### Direct import (Node / Bun / Deno)

```js
import data from "https://raw.githubusercontent.com/Docz-me/freelance-vat-rates/main/data.json" assert { type: "json" };

const uk = data.find(c => c.country === "united-kingdom");
console.log(uk.standard); // 20
```

### As an npm-free dependency

```bash
curl -O https://raw.githubusercontent.com/Docz-me/freelance-vat-rates/main/data.json
```

### CDN

```
https://cdn.jsdelivr.net/gh/Docz-me/freelance-vat-rates@main/data.json
```

## Scope

This dataset focuses on what a freelancer needs to know to send a correct invoice. It is **not** a comprehensive tax compendium — for filing, registration, or audits, consult a qualified accountant in the relevant jurisdiction.

Out of scope:

- Industry-specific reduced rates (broadcasting, transport, etc.)
- Sub-national rates (US state sales tax, Canadian provincial)
- Historical rate changes
- Reverse-charge mechanics (covered in `notes` where relevant)

## Contributing

Spotted a stale rate or missing country? PRs welcome.

1. Fork and edit `data.json`.
2. Keep entries alphabetical by `country` slug.
3. Update `verified_date` to the ISO date you re-checked the official source.
4. Cite the primary government/tax-authority page in `source_url` — not a third-party summary.
5. Open a PR with the country slug in the title (e.g. `Add: india`).

## Verification policy

Every entry should be re-verified at least every 12 months. Help is appreciated.

## License

[MIT](./LICENSE) — use freely, attribution appreciated but not required.

## Related

- [late-payment-fees](https://github.com/Docz-me/late-payment-fees) — statutory late-payment rules by jurisdiction.
- [awesome-freelance](https://github.com/Docz-me/awesome-freelance) — curated freelance tools and resources.
- [Docz.me](https://docz.me) — invoicing that uses this data automatically.
