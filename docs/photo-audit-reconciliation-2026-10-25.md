# Photo audit reconciliation — 2026-10-25

Source: `docs/photo-audit-2026-10-25.csv` on PR #20. This is a static metadata audit, not a browser/photo-loading test.

## Full 347-row status reconciliation

| Status | Facilities |
|---|---:|
| pilot_loading (Google Places dependent; display unverified) | 253 |
| available | 14 |
| 記録上URLあり (URL recorded; display unverified) | 14 |
| 未設定 | 66 |
| **Total** | **347** |

The earlier 14-row discrepancy is explained by the fourth status, `記録上URLあり`, which must not be merged into `available`.

## Category values recorded in the CSV

| Category value | Facilities | pilot_loading | available | URL recorded | unset |
|---|---:|---:|---:|---:|---:|
| date | 142 | 118 | 0 | 11 | 13 |
| kids | 55 | 43 | 9 | 1 | 2 |
| food | 41 | 41 | 0 | 0 | 0 |
| pet | 14 | 14 | 0 | 0 | 0 |
| tourism | 43 | 11 | 5 | 1 | 26 |
| solo | 37 | 26 | 0 | 1 | 10 |
| 未分類 | 15 | 0 | 0 | 0 | 15 |
| **Total** | **347** | **253** | **14** | **14** | **66** |

The 15 `未分類` entries need reconciliation against the app's six displayed categories. Do not silently assign categories or delete records.

## Source metadata

- Google Places: 253
- myCocomo: 14
- Wikimedia Commons: 4
- spot.image (attribution metadata not linked): 10
- Empty: 66

The 14 URL-recorded entries comprise 4 Wikimedia Commons records and 10 `spot.image` records without linked attribution metadata. The latter need rights/attribution verification before any replacement or publication changes.

## Next gate

1. Determine why 15 registry entries have `未分類` and whether each is rendered as a spot.
2. Confirm `available` image URLs and rights metadata; do not equate metadata with live image success.
3. Rank free-photo candidates for food and scenic locations; Google pilot remains limited to five approved IDs.
4. Run mock/browser tests separately before production approval.

No production changes or paid API calls are authorized by this document.
