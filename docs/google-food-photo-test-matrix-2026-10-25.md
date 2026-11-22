# Google food photo pilot — verification matrix

Status: REVIEW ONLY. Google photo pilot remains OFF. No paid API requests, deploys, or production activation were performed.

## Confirmed from current PR branch
- Web pilot flag is `GOOGLE_FOOD_PHOTO_PILOT_ENABLED=false`; it returns before fetch for every facility.
- Web external photo allowlist is restricted to the five approved IDs: fuk-0264, fuk-0283, fuk-0339, fuk-0262, fuk-0209.
- Worker has the same five IDs, both flags are false, and legacy/candidate routes return 503.
- Photo error handler hides the photo and credit and shows the type illustration; the 「イメージ」 label is in the fallback.
- Author names are HTML-escaped and author/Google Maps links only accept HTTPS.
- Worker CORS permits the official Pages origin. This is not authentication and does not prevent direct HTTP calls.
- Worker health response no longer reveals whether the API secret is configured.

## Results

| Check | Result | Evidence / limitation |
|---|---|---|
| Five facility allowlist | PASS | Web and Worker allowlists match exactly. |
| Web flag OFF prevents API call | PASS (static inspection) | Early return precedes fetch. No runtime browser instrumentation. |
| Worker off switch preserved | PASS (static inspection) | Both flags false; route guard precedes upstream calls. |
| Non-allowlisted Worker ID denied | PASS (static inspection) | ID check before disabled route guard/provider logic. No HTTP request run. |
| Candidate/review routes disabled | PASS (static inspection) | Return 503 before old route handlers. |
| Client HTML/URL escaping | PASS (static inspection) | Names escaped; only HTTPS href accepted. |
| Google Maps source link and author attribution on success | NOT RUN | No successful mock response or browser harness. |
| Type illustration and 「イメージ」 on failure | PASS (static inspection) | Error handler reveals placeholder; not visually rendered. |
| iPhone bottom sheet / desktop popup | NOT RUN | No browser or device run. |
| Rapid pin switch isolation | NOT RUN | No automated/browser interaction test. |
| 347 facilities / six categories / IDs / Wikimedia / Leaflet / OSM / favorites / SEO / GA4 regression | NOT RUN | No executable regression run. |
| Worker secret leakage | PASS (static inspection) | No key in client code or logs; health endpoint only reports providerEnabled. |
| Direct-call abuse and spend ceiling | FAIL for activation readiness | CORS is bypassable and no durable quota exists; repeated metadata calls can repeatedly invoke paid Text Search. |
| Official pricing and terms | PASS (document review) | See activation gate document for current findings and official source URLs. |

- Current main and PR spot arrays both evaluate to 421 facilities, not the required baseline of 347; this mismatch predates PR #20 and was not changed. Six categories are present. Facility IDs are assigned at runtime from canonical names, so a full ID-diff regression remains unrun.

## Activation blockers
1. Add durable concurrency-safe usage limits before provider calls; account independently for Text Search and Photo Media, and fail closed.
2. Confirm the final photo resource freshness/cache architecture complies with Google's no-caching rules.
3. Add a fully mocked browser test harness for success, failed media, unsafe URLs, fallback, sheet/popup, and rapid pin switching.
4. Run full regression checks and inspect a real device/browser before production.
5. Set Cloud Billing budget alerts; keep weekly Sunday review. Neither provides a hard cap.
6. Obtain explicit approval before any merge, deploy, billing change, or API activation.
