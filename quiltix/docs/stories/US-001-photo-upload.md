# US-001 — Photo Upload

## Epic
Convert a user-provided photo into a pixel-style quilt pattern.

## Story
**As a** quilter,  
**I want to** upload a photo or capture one from my device camera,  
**So that** I can use it as the source image for my quilt pattern.

## Inputs
- Image file (upload) or camera capture (mobile browser)
- Accepted formats: JPEG, PNG, WEBP
- Maximum file size: 10MB

## Acceptance Criteria
- [ ] User can select a file from their device via a file picker
- [ ] User can capture a photo directly from a mobile browser camera (via the native file picker's camera option — not a custom camera UI)
- [ ] Accepted file types are enforced (JPEG, PNG, WEBP); unsupported types show a clear error message naming the accepted formats
- [ ] Files exceeding 10MB are rejected with a friendly error message stating the limit
- [ ] A preview of the uploaded image is displayed in a constrained container (max 400px wide, aspect ratio preserved, no cropping) before the user proceeds
- [ ] If the uploaded image is below 300×300px, a non-blocking warning is shown: "This image is low resolution — pattern quality may be affected." The user can still proceed.
- [ ] After a valid upload, a clearly labeled "Continue" button appears to advance to the next step
- [ ] Upload works on current versions of Chrome, Firefox, and Safari (desktop and mobile)

## Definition of Done
- File validation (type + size) is enforced on the client before any server call
- Preview renders without layout shift or overflow
- Low-res warning is visible but does not block the continue action
- All error messages are user-friendly (no raw exception text)

## Environment / Testing Prerequisites
- All tests run inside Docker containers via Docker Compose
- Frontend served by the React dev server container
- Backend served by the FastAPI container
- Playwright E2E tests run in a dedicated test container with browser binaries included
- `docker compose up` must be the single command to bring up the full test environment
- No local Node, Python, or browser installs assumed outside of Docker

## Test Coverage
- Unit: file type validation, file size validation, resolution detection
- E2E (Playwright): upload flow (desktop), upload flow (mobile viewport), file type error state, file size error state, low-res warning display, continue button appearance after valid upload

## Notes
- Camera capture on mobile relies on the browser's native `<input type="file" accept="image/*" capture>` behavior — no custom camera UI
- Image is not persisted server-side beyond the active session (MVP)
- The 300px resolution threshold for the low-quality warning is a tunable constant, not a hard-coded magic number
