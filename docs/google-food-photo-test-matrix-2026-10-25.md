# Google food photo pilot — verification matrix

Status: implementation review, NOT a runtime/browser test report. API stays disabled.

## Code inspection findings (2026-10-25)
- Pilot flag: `GOOGLE_FOOD_PHOTO_PILOT_ENABLED=false`; five facility IDs.
- `ensureExternalPhotoMetadata` exits before fetch unless the flag and allowlist match.
- Mobile pin click opens the existing bottom sheet and refreshes its body only when the same facility remains active.
- Desktop popup refreshes only if the same popup is still open.
- `facilityVisualHtml` retains the facility-type illustration and an 「イメージ」 label.
- `handlePhotoError` hides a broken image and its credit, then reveals the illustration.
- Google author names are escaped as text; attribution URLs and Google Maps links are accepted only when HTTPS.
- Worker review branch retains both disable flags. Candidate and legacy routes return 503.
- The pilot is not enabled and no chargeable provider requests were made during this review.

## Runtime tests still required before production approval
1. Mock metadata success for each of the five facility IDs and verify photo, Google Maps link and attribution on iPhone bottom sheet and desktop popup.
2. Mock missing image, failed media response, missing attribution and invalid author URLs; verify illustration and no broken links.
3. Verify rapid pin switching cannot replace the currently open facility's sheet.
4. Verify 347 facility records, six categories, all IDs, existing Wikimedia credits and Google-disabled baseline remain unchanged.
5. Check browser console, JS syntax, responsive layout, and Worker route behavior using a local test harness.
6. Review Google Maps Platform photo media and text search pricing and Terms; set Cloud Billing budget alerts and weekly Sunday manual check.
7. Obtain explicit approval before any merge, deployment or API enablement.

**Important:** Weekly billing review is not a hard spending cap and billing data can be delayed. This plan reflects the owner's acceptance of that residual risk.
