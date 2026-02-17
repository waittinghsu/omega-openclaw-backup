---
name: notion-expense-logger
description: Detect plain-language expense notes and log them to the Notion "Monthly Budget" Expenses database (date + item + amount in TWD). Use whenever the user provides spending records or asks to record expenses in Notion.
---

## Overview
Use this skill to capture expense statements (e.g., `高鐵板橋到台中 700`, `2026-02-17 WeMo 100`) and push them into the Notion **Monthly Budget → Expenses** database. Each entry must include:

- **Date** – ISO `YYYY-MM-DD`. If absent, assume today in Asia/Taipei timezone.
- **Expense Item** – the textual label provided by the user.
- **Amount** – numeric value in TWD (default currency). Strip commas and trailing currency markers.

## Database Details
- Database ID: `107dc601-4b1f-44d6-88b0-1dab3804a321`
- Data Source ID: `b88d4c92-1f8c-484e-9fef-82b1a3513412`
- Properties:
  - `Expense Item` (title)
  - `Amount` (number)
  - `Date` (date)

The Notion integration key is available via the `NOTION_API_KEY` environment variable (value starts with `ntn_`).

## When to Trigger
Activate this skill whenever the user supplies expense entries, whether single-line or batched, or explicitly asks to "記帳", "寫到 Notion", or similar. If the user only inquires about configuration (e.g., "有沒有接 Notion"), respond normally; no logging is required.

## Parsing Rules
1. **Tokenize** each expense line:
   - Pattern preference: `[optional date] <item text> <amount>`.
   - Treat the last number in the line as the amount. Remove commas or suffixes like `元`, `NT`, `$`.
   - Item text is everything between the optional date and the amount.
2. **Date handling:**
   - Accept explicit `YYYY-MM-DD`, `MM/DD`, or Chinese formats like `2月17日` (convert to the current year).
   - Keywords: `今天` → today, `昨天` → today - 1.
   - If missing, default to today (Asia/Taipei). Use `date +%Y-%m-%d -d 'TZ="Asia/Taipei" now'` to compute.
3. **Validation:** If either item text or amount is missing, ask the user to clarify before logging.

## Notion API Call
Use the Notion Pages endpoint to create each expense:

```bash
curl -s -X POST "https://api.notion.com/v1/pages" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2025-09-03" \
  -H "Content-Type: application/json" \
  -d '{
    "parent": {"database_id": "107dc601-4b1f-44d6-88b0-1dab3804a321"},
    "properties": {
      "Expense Item": {"title": [{"text": {"content": "高鐵 板橋→台中"}}]},
      "Amount": {"number": 700},
      "Date": {"date": {"start": "2026-02-17"}}
    }
  }'
```

For multiple expenses, loop over each parsed entry. Return a concise confirmation listing what was logged (item, amount, date). If an API call fails, surface the error details and note which entries were not saved.

## Best Practices
- Batch messages: accumulate all expense lines in the user’s latest request before calling the API.
- Preserve original wording for `Expense Item` unless the user requests a transformation.
- Always confirm back to the user after logging (e.g., "已記錄：高鐵 板橋→台中 700 元，日期 2026-02-17").
- If the user later corrects an entry, locate it via the Notion UI or the API (`POST /v1/data_sources/{id}/query`) and patch as needed.
