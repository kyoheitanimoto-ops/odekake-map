# Food photo batch execution policy — 2026-10-25

## Authorization

User approved continuous work without per-facility approvals for no-cost photo research, verification, review-branch implementation and testing. Report results in batches rather than asking for confirmation for every venue.

**Approval gates retained:** any actual expense or paid API invocation; licensing or identity ambiguity requiring a policy decision; regressions or other problems; merge to main and production deployment. Do not expand the existing five-site paid Google pilot without a cost approval.

## Work queue

Source: `docs/food-photo-a-priority-tracker-2026-10-25.csv`. Of its 145 provisional records, 142 are marked photo priority A and 3 priority B (Futamigaura cafe area, Hatsu beach, Itozu Yoru Zoo). Priority A is a work queue, **not proof of dining classification**. Preserve stable facility IDs.

For each A venue:
1. Check facility identity and actual primary purpose; preserve records even when reclassified.
2. Search no-cost authorized photo sources (Wikimedia Commons file-level licenses; written permissions from venue owners); verify exact venue and subject.
3. Record evidence: source page, original file URL, author, license, attribution, modification/redistribution terms, identity match, and date.
4. If evidence is complete, prepare review-branch changes, retaining existing author/license metadata and illustration fallback; test on mobile and desktop.
5. If evidence is incomplete, leave the illustration and mark the issue as pending. Do not copy images from search results, social media or official websites without redistribution permission.

## Batch report format

Report: venues reviewed, photo candidates found, licenses verified, photos implemented and rendered, unresolved exceptions, API requests, expenses, commits and preview links. Distinguish discovered images from adopted images and verified display. Do not claim work has been performed without evidence.

## Existing candidate status

`docs/food-photo-source-evidence-2026-10-25.csv` records 5 photo leads, all on hold; no confirmed new licensed image or production change yet.
