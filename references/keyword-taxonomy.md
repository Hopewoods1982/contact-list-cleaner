# Keyword Taxonomy

This taxonomy combines general CRM data-hygiene guidance with generic contact-label patterns. It does not contain any user-specific contacts.

## Source Basis

- HubSpot: clean contact lists and suppression segments:
  https://knowledge.hubspot.com/marketing-email/how-to-clean-up-your-contact-lists-to-improve-deliverability
- Salesforce: data hygiene and stale/risky records:
  https://help.salesforce.com/s/articleView?id=mktg.mktg_apps_email_best_practices_hygiene.htm
- MassMailer: role-based addresses, invalid contacts, and inactivity:
  https://massmailer.io/blog/how-to-clean-email-list/
- Clearout: CRM data hygiene, role accounts, disposable or risky contacts:
  https://clearout.io/blog/crm-data-hygiene/
- Digital Applied: CRM contact data hygiene and duplicate/cleanliness practices:
  https://www.digitalapplied.com/blog/crm-data-hygiene-2026-contact-management-guide
- National Financial Regulatory Administration: risk warning about illegal loan intermediaries:
  https://www.nfra.gov.cn/branch/shenzhen/view/pages/common/ItemDetail.html?docId=1212987&itemId=1041

## Categories

### Strong exclusions

- `financial_services`: lending, credit, insurance, financing, debt collection, financial intermediaries.
- `tax_bookkeeping`: tax, bookkeeping, company registration, tax-planning sales.
- `real_estate`: estate agents, property agents, rental intermediaries.
- `training_education`: training, tutoring, education sales, calligraphy, music, art, driving schools, admissions.
- `recruitment`: recruiters, headhunters, job agencies, part-time recruitment.
- `automotive_lighting`: car audio/video, car modification, navigation, vehicle lighting, lighting agents.
- `role_accounts`: generic customer-service or role-based accounts and bots.
- `marketing_spam`: promotional or spam-like labels.

### Weak exclusions

- `consumer_retail`: retail, food, beverage, media, gifts, consumer supply chains, and lifestyle services.
- Weak exclusions are skipped when the record also contains a protected core-business term.

## Protected Core Terms

The default keep list is intentionally B2B/industrial:

`煤矿`, `矿业`, `煤业`, `榆通`, `物资`, `中煤`, `陕煤`, `延长`, `陕投`, `能源`, `工程`, `科技`, `研究院`, `研究所`, `大学`, `学院`, `设计院`, `自动化`, `仪器`, `设备`, `光纤`, `监测`, `安全`, `生产`, `矿用`.

## Identity Tiers

- Tier 1: explicit person name + phone/contact detail.
- Tier 2: explicit person name without contact detail.
- Tier 3: handle, nickname, brand, or organization name only.

Moving tier-3 records to the end is a sorting recommendation, not a deletion rule.