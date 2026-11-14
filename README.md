# E-Commerce Order CSV Samples & 4×6 Thermal Print Specs

Curated, 100% fictional e-commerce order CSV fixtures, field-mapping references, and browser-verified 4×6 / A4 thermal packing slip & pick list printing notes for Shopify, eBay, Whatnot, and multi-channel sellers.

> **Privacy notice:** Every row, name, street address, username, and order number in `samples/` is fictional test data created for parser QA and fulfillment workflow testing. No real buyer PII is included.

---

## What's Inside

| File | Purpose | Key Edge Cases Covered |
| --- | --- | --- |
| [`samples/shopify-orders-export.csv`](samples/shopify-orders-export.csv) | Shopify-style order CSV export | `Name` (`#1041`) vs `Lineitem name` grouping, multi-line orders, SKU aggregation |
| [`samples/ebay-orders-export.csv`](samples/ebay-orders-export.csv) | eBay Seller Hub order CSV export | `Order Number` (`EB-4081`), `Custom Label` as SKU, `Buyer Note` |
| [`samples/whatnot-orders-export.csv`](samples/whatnot-orders-export.csv) | Whatnot livestream order CSV export | UTF-8 BOM, multi-item orders (`DEMO-2041`), `Bin` location & `Order Note` |
| [`samples/same-buyer-multi-order.csv`](samples/same-buyer-multi-order.csv) | Same buyer placing separate orders | Verifying two distinct `Order ID`s for the same `Buyer Username` are **not** silently merged by name |
| [`samples/csv-edge-cases.csv`](samples/csv-edge-cases.csv) | Validation & QA test suite | Missing Order ID, missing SKU/item name, blank or zero quantity, duplicate rows |
| [`specs/4x6-thermal-print-checklist.md`](specs/4x6-thermal-print-checklist.md) | 4×6 & A4 browser print troubleshooting | Scale `100%` / `Actual Size`, `Margins: None`, blank page overflow fixes |
| [`specs/excel-csv-scientific-notation-fix.md`](specs/excel-csv-scientific-notation-fix.md) | Preventing Excel CSV corruption | Tracking numbers turning into `1.23E+11` and ZIP codes losing leading zeros (`07001` -> `7001`) |

---

## Quick Column Mapping Reference

When converting raw marketplace CSVs into consolidated SKU **pick lists** and per-order **packing slips**:

| Marketplace / Export | Order Grouping Key | Item Title | SKU | Quantity |
| --- | --- | --- | --- | --- |
| **Shopify (`orders_export_1.csv`)** | `Name` (e.g. `#1041`) | `Lineitem name` | `Lineitem sku` | `Lineitem quantity` |
| **eBay Seller Hub** | `Order Number` | `Item Title` | `Custom Label` | `Quantity` |
| **Whatnot** | `Order ID` | `Item Name` | `SKU` | `Qty` |

> **Common Shopify trap:** Mapping `Lineitem name` instead of `Name` as the Order ID splits a multi-item order into separate packing slips. Always group by `Name`.

---

## Browser-Based Verification Tool (Free, No Signup)

You can test any of the sample CSVs above directly in your browser without uploading files to a server:

- **Packing Slip & Pick List Generator:** [OrderQuill Packing Slip Generator](https://orderquill.com/packing-slip-generator) — client-side CSV parser supporting 4×6 thermal and A4 layouts (free for up to 20 orders per batch, no account required).
- **Shopify Pick List Guide (`orders_export_1.csv`):** [Shopify Pick List Workflow](https://orderquill.com/shopify-pick-list)
- **4×6 Thermal Label & Slip Setup:** [Shipping Label Printer Guide](https://orderquill.com/shipping-label-printer)

---

## License

MIT — feel free to fork, reuse these fictional test CSVs in CI/CD or shipping parser tests, and submit PRs with anonymized column layouts for other marketplaces.
