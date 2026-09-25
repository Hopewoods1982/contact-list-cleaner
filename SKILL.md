---
name: contact-list-cleaner
description: Clean, classify, deduplicate, score, and audit exported contact lists from CRM systems, spreadsheets, or chat exports. Use when a contact list needs identity tiers, service/spam exclusions, keyword-based hygiene rules, or a reviewable cleaned copy without modifying the source system.
metadata:
  version: 1.0.0
  short-description: Clean CRM, spreadsheet, and exported contact lists safely.
---

# Contact List Cleaner

Use this skill to produce a reviewable cleaned copy of a contact list. Never delete or mutate contacts in the source CRM, phone, chat client, or live database.

## Workflow

1. Read `references/keyword-taxonomy.md` before choosing exclusion rules.
2. Inspect the input schema and identify name, username, notes, phone, aliases, and chat-message columns.
3. Run `scripts/classify_contacts.py` to generate an audit CSV or XLSX-compatible CSV.
4. Preserve strong business contacts using the `keep_terms` in `references/keyword-taxonomy.json`.
5. Separate results into:
   - excluded service/spam contacts
   - identity tier 1: explicit person name + contact detail
   - identity tier 2: explicit person name without contact detail
   - identity tier 3: handle, brand, or organization name only
6. Review ambiguous matches before applying any downstream workflow.
7. Keep the original name in `original_name`; only put a confidently resolved name in `resolved_name`.

## Safety Rules

- Default to dry-run behavior: write a cleaned copy, never edit the input.
- Never delete a contact from WeChat, a CRM, a phone, or another live service.
- Never infer a real name from a brand name alone.
- Keep role/service keywords configurable so the taxonomy can be adapted by industry.
- Treat financial, lending, insurance, training, recruitment, and intermediary keywords as high-risk exclusions unless the user explicitly defines a legitimate exception.
- Do not upload contact data to external services when using this skill.

## Files

- `references/keyword-taxonomy.md` — categories, examples, public sources, and rationale.
- `references/keyword-taxonomy.json` — machine-readable keyword rules.
- `scripts/classify_contacts.py` — dependency-light classifier for CSV and XLSX inputs.