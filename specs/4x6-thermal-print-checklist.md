# 4×6 & A4 Thermal Print Checklist (Browser Print Dialogs)

This checklist separates settings **verified directly in desktop browser print dialogs** from **hardware/driver behaviors** that vary by thermal printer model.

---

## 1. Verified Browser Print Dialog Settings

| Symptom | Common Cause | Fix |
| --- | --- | --- |
| Packing slip prints tiny with wide white borders | Print dialog is set to "Fit to page" or shrinks an A4 layout onto 4×6 | Set Scale to **Actual Size / 100%** and generate the layout specifically for **4×6** |
| One slip splits across two thermal labels | Browser margins are too wide or custom scale overflows page height | Set Margins to **None** (or **Minimum**), Scale to **100%**, and test page 1 first |
| Content is clipped on the right or bottom edge | A4 layout sent directly to a 4×6 roll/fanfold printer | Switch the document layout to **4×6** before opening the print dialog |
| Extra blank label after every slip | Page-break rules + extra margin overflow onto a second page | Set Margins to **None** and inspect total page count in Print Preview before batch printing |
| Faded text or missing header/barcodes | "Background graphics" disabled or printer driver in draft/dither mode | Enable **Background graphics** in Print Preview and disable draft/toner-save mode |

---

## 2. Recommended CSS `@page` Baseline for 4×6 Packing Slips

```css
@media print {
  @page {
    size: 4in 6in;
    margin: 0.15in;
  }

  .packing-slip {
    page-break-after: always;
    break-after: page;
    box-sizing: border-box;
    width: 100%;
  }

  .packing-slip:last-child {
    page-break-after: auto;
    break-after: auto;
  }
}
```

---

## 3. Hardware-Dependent Items (Verify Locally Per Printer)

Because OS print spoolers and thermal hardware vary (Rollo, Zebra ZD421, MUNBYN, DYMO, iDPRT):
- Always run **media/gap calibration** on your thermal printer after changing label stock.
- Print **1 test slip** first to catch a 1–2 mm hardware feed offset before sending a 50-order batch.
- Desktop Chrome / Edge / Safari print dialogs are recommended over mobile print share sheets.
