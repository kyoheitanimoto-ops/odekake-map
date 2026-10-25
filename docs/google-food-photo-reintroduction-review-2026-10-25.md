# Google food photos: pre-activation audit (2026-10-25)

Status: REVIEW ONLY. This branch does not enable Google Places Photos, change the Cloudflare Worker, or incur API requests.

## Verified baseline
- Web main: 673fc90 (GA4 PR #19).
- Web `index.html` retains `facilityPhotoMetadata`, `EXTERNAL_PHOTO_PILOT_IDS`, and `ensureExternalPhotoMetadata`.
- The web function explicitly returns false for `photo.provider === 'google_places'`; the old Google photo metadata remains but is not fetched.
- Separate Worker repository: `kyoheitanimoto-ops/mycocomo-photo-api`, `worker.js` on main.
- Worker global `GOOGLE_PLACES_PHOTOS_ENABLED = false` and route guard remain in place.
- No deployment, API key change, billing configuration change, or Worker code modification has been performed.

## Approved planning constraints
- Prioritize actual food/cafe photos; retain Wikimedia photos and illustration fallbacks.
- Monthly target: JPY 500, with usage and actual billing observed during a small pilot.
- User is willing to reassess if spending exceeds target materially; this is NOT an authorization to incur unbounded costs.
- User must approve production activation/billing changes and merging PRs.

## Required before enabling
1. Verify current Google Maps Platform photo/media, search and place-details SKU pricing, free quotas and applicable terms from official sources.
2. Review Google photo attribution, caching/storage, and permitted presentation, including map-related restrictions.
3. Review existing Worker photo endpoints for per-request API calls, public abuse, duplicate calls, and secrets exposure.
4. Implement conservative rate/usage protection with a kill switch, and test the seven disabled routes still make zero Google calls.
5. Confirm actual food-category facility counts and image availability, not just photo metadata placeholders.
6. Prepare a separate Worker PR and Web PR; run syntax, regression, 347-facility/6-category/ID, license and mobile bottom-sheet checks.
7. Request explicit user approval before activating either API billing or production traffic.

## No-go criteria
- Unverified license/attribution requirements.
- No effective call-volume guard or inability to disable quickly.
- Any accidental activation of the previously disabled Worker endpoints.
