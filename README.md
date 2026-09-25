# contact-list-cleaner

A Codex skill and standalone classifier for cleaning exported contact lists without modifying the source system.

It separates:

- high-risk service/spam contacts
- type 1 contacts with a person name and phone/contact detail
- type 2 contacts with a person name but no contact detail
- type 3 handle-only, nickname-only, or brand-name contacts

The taxonomy protects core B2B terms such as coal mines, mining, procurement, research institutes, engineering, automation, instrumentation, optical fibre, and monitoring.

## Safety

- Never deletes or edits the input list.
- Never deletes contacts from WeChat, a CRM, or a phone.
- Never uploads contact data.
- Produces a reviewable CSV audit copy.

## Install as a Codex skill

Copy this directory to:

```text
%CODEX_HOME%\skills\contact-list-cleaner
```

If `CODEX_HOME` is not set, use:

```text
%USERPROFILE%\.codex\skills\contact-list-cleaner
```

The skill is then available on the next Codex turn.

## Standalone usage

CSV input:

```powershell
python scripts\classify_contacts.py contacts.csv classified.csv
```

XLSX input requires `openpyxl`:

```powershell
python -m pip install openpyxl
python scripts\classify_contacts.py contacts.xlsx classified.csv --name-col "微信备注名" --username-col "微信号" --notes-cols "备注"
```

The script auto-detects common Chinese and English column names when explicit columns are omitted.

## Output columns

- `original_name`
- `resolved_name`
- `username`
- `identity_tier`
- `contact_info`
- `exclude`
- `exclude_categories`
- `exclude_reasons`
- `protected_keep_terms`
- `notes`

## Public sources used

- HubSpot contact list cleanup
- Salesforce data hygiene
- MassMailer list cleaning
- Clearout CRM hygiene
- Digital Applied CRM data hygiene
- National Financial Regulatory Administration risk warning on illegal loan intermediaries

See `references\keyword-taxonomy.md` for links and category rationale.

## License

MIT