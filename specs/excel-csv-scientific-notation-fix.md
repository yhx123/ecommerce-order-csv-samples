# Preventing Excel CSV Corruption (Scientific Notation & Dropped Leading Zeros)

Opening a marketplace order CSV (`orders_export_1.csv`, eBay orders, or USPS tracking exports) by double-clicking it in Microsoft Excel frequently corrupts two critical fields before you even print:

1. **Tracking numbers & long IDs turn into scientific notation**: A 22-digit USPS tracking number like `9400111899223847102934` becomes `9.40011E+21`, and saving the file permanently overwrites the trailing digits with zeros.
2. **US East Coast ZIP codes & SKUs lose leading zeros**: `07001` (New Jersey) becomes `7001`, and SKU `00412` becomes `412`.

---

## Safe Ways to Inspect or Fix Order CSVs

### Option A: Do Not Double-Click in Excel Before Generating Packing Slips
Keep the original `.csv` downloaded from Shopify/eBay/Whatnot untouched and feed it directly into a client-side parser (such as [OrderQuill](https://orderquill.com/packing-slip-generator) or a Python/Node script) that reads fields as raw UTF-8 strings.

### Option B: Import via Excel "From Text/CSV" (Power Query)
If you must open the CSV in Excel:
1. Open a blank workbook in Excel.
2. Go to **Data -> From Text/CSV** (instead of `File -> Open`).
3. In the preview dialog, set **Data Type Detection** to **Do not detect data types**, or manually force `Zip`, `SKU`, `Tracking Number`, and `Order ID` columns to **Text** before clicking **Load**.

### Option C: Google Sheets Import
In Google Sheets, use **File -> Import -> Upload**, and **uncheck** `Convert text to numbers, dates, and formulas` so leading zeros and long tracking strings stay intact.
