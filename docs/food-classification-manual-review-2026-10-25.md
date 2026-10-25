# Food facility classification review — 2026-10-25

## Status

The existing 347-facility A/B/C classification remains **provisional**. Four obvious candidate false negatives were already corrected in commit `7526997d`. No other changes to A/B/C classifications are authorized by this report.

## Manual decision queue

| Facility ID | Facility | Existing class | Why manual verification is needed |
|---|---|---|---|
| fuk-0012 | BOSS E・ZO FUKUOKA | C | Venue's primary function cannot be reliably inferred from name alone |
| fuk-0042 | Moff animal cafe マークイズ福岡ももち店 | C | Venue's primary function cannot be reliably inferred from name alone |
| fuk-0043 | Moff animal cafe ららぽーと福岡店 | C | Venue's primary function cannot be reliably inferred from name alone |
| fuk-0115 | パームビーチクラブ | C | Venue's primary function cannot be reliably inferred from name alone |
| fuk-0204 | 三井港倶楽部 | C | Venue's primary function cannot be reliably inferred from name alone |
| fuk-0271 | 道の駅むなかた | B | Venue's primary function cannot be reliably inferred from name alone |

## Review requirements

- Use all 421 spot records to consolidate explicit category, subcategory and tags by stable facility ID; do not classify by free-text description alone.
- Animal cafes may primarily be animal-interaction venues, not conventional cafes; keep unresolved until checked.
- Distinguish restaurants from multi-purpose tourist and commercial venues.
- Check that all dining-tagged date, solo, pet and other categories are captured even if the registry category is not `food`.
- Record both false-positive and false-negative examples, then verify all 347 classifications before claiming a definitive total.

The 145 A / 63 B / 139 C counts are **draft only**, not a photo coverage denominator. No merge, deployment or paid API usage.
