CINEWAVE — CLOUDFLARE WORKERS PACKAGE

This version is built for Cloudflare Workers + static assets + D1 database.
The website files are inside the site folder. worker.js handles account APIs.

IMPORTANT ABOUT THE BURP SUITE TRAINING LAB
The /api/lab/vip-check endpoint is intentionally vulnerable for a private,
disposable learning demo. It trusts the client-supplied is_vip value when the
lab switch is enabled. Do not enable this on a public production site. Disable
ENABLE_VIP_BURP_LAB after your recording. Real VIP access must be checked on
the server against trusted payment/account records.

DEPLOY USING CLOUDFLARE DASHBOARD + GITHUB
1. Extract this ZIP.
2. Upload ALL extracted files and the site folder into the ROOT of a new GitHub
   repository. Keep the site folder; do not move its contents out.
3. In Cloudflare, open Workers & Pages and create a Worker. Choose Connect to
   Git / deploy from GitHub, then select this repository.
4. Build/deploy command: npm install && npx wrangler deploy
   Root directory: / (repository root).
5. Create a D1 database named cinewave-db in Cloudflare.
6. Copy the D1 database ID into wrangler.toml, replacing
   PASTE_YOUR_D1_DATABASE_ID_HERE. Commit the change to GitHub.
7. In the Cloudflare terminal/build environment (or with Wrangler locally),
   apply schema.sql:
   npx wrangler d1 execute cinewave-db --remote --file=./schema.sql
8. In Worker Settings > Variables and Secrets, add:
   SESSION_SECRET = a long random secret (mark as Secret)
   ENABLE_VIP_BURP_LAB = true (only for a private training demo)
9. Redeploy. Open the Worker URL to test CineWave.

If using the Cloudflare dashboard editor rather than Git integration, choose
Workers with static assets and use this repository's Wrangler configuration.
The easiest reliable deployment path is Git integration with Wrangler.

NOTES
- This package does not use Railway, Dockerfile, or PHP.
- Accounts are stored in Cloudflare D1, not temporary local files.
- The VIP Burp demo only changes access in the current browser session; it does
  not upgrade the stored account. Refreshing or signing out resets the demo.
- Use only movie/video content you own or are licensed to stream.
- Do not use real passwords in this demo project.
