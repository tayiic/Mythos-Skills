---
name: xlsx-optimized
description: Use when creating, editing, analyzing, validating, or formatting spreadsheet files while preserving formulas, tables, charts, and workbook integrity.
---

# XLSX Optimized

Use structured spreadsheet libraries. Do not manipulate workbook XML by hand.

## Flow

1. Inspect workbook sheets, tables, formulas, styles, and charts before editing.
2. Choose operation: create, transform, analyze, format, chart, or validate.
3. Preserve formulas and named ranges unless explicitly changing them.
4. Recalculate or document recalculation requirements.
5. Validate the saved workbook opens and key cells match expectations.

## Gotchas

- Do not overwrite formulas with displayed values.
- Do not drop styles, merged cells, charts, or tables accidentally.
- Do not infer financial or legal conclusions without user confirmation.
