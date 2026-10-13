# CODE MASTER AI

Android coding workspace with black/red neon UI and a separate Node.js AI backend.

## Android features
- Black/red neon interface
- AI Generate, Debug, Explain, and Improve modes (requires deployed backend)
- HTML editor with sandboxed preview
- Save project locally and export HTML
- HTML/CSS/JavaScript templates and basic local checks

## Build the Android Debug APK
1. Push this folder's contents to the root of the GitHub repository.
2. Connect the repository to Codemagic.
3. Choose workflow `android-debug` in `codemagic.yaml`.
4. Run the build and download `app-debug.apk` from Artifacts.

## Activate AI backend
The app does not contain an API key. Deploy the `backend/` folder as a Node.js service on a hosting provider that supports Node 20+.
Set these environment variables in the hosting dashboard:
- `AI_API_KEY`: API key from your AI provider
- `AI_BASE_URL`: API base URL, default `https://api.openai.com/v1`
- `AI_MODEL`: model available to your API key, default `gpt-4.1-mini`
- `ALLOWED_ORIGIN`: use `*` for initial testing, then restrict it where possible
- `PORT`: usually assigned automatically by the host

After deployment, copy the backend HTTPS URL into CODE MASTER > Settings > Backend URL and tap Test Connection. `/health` should return JSON with `status: ok`.

## Important
- Keep `AI_API_KEY` as a server-side environment variable. Never put the real key in the Android app, HTML, or a public repository.
- AI calls may incur provider charges and are rate-limited to 12 requests per minute per client IP by this starter backend.
- This backend uses an OpenAI-compatible `/chat/completions` endpoint. Set `AI_BASE_URL` and `AI_MODEL` to values supported by your provider.
- The backend currently has basic rate limiting but no user accounts or per-user quotas. Do not expose it publicly with a paid key until you add stronger abuse controls.
- This app/backend has been assembled as a starter project; run a real build and test after pushing.
