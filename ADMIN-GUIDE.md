# GTech admin panel

## Start in VS Code on Windows

Install Node.js 22 or newer. Open the extracted `gtech-website` folder in VS Code, then open its terminal.

Run these commands once:

```bash
npm run setup
```

Choose your admin username and a password of at least 12 characters. Password entry is hidden. There is no default password.

Start the website:

```bash
npm start
```

- Client website: http://localhost:5500
- Admin panel: http://localhost:5500/admin

No dependency installation is required; the server uses Node.js built-in modules. Keep the terminal running. Use **Ctrl+C** to stop it. Use `npm start` the next time you want to run it.

Use this server for content updates. VS Code Live Server and opening `index.html` directly display the original static snapshot rather than the managed content.

## Add or edit products

1. Open **Products → Add product**. Existing entries have **Edit** and **Copy** actions; Copy creates an unsaved draft with the original fields.
2. Choose an optional template: general, biometric/access reader, card printer, barrier/turnstile, or POS/scanner. Applying a template sets the category and replaces specification fields; it does not erase your name, descriptions or photo.
3. Enter the product name, brand, primary category/subcategory and descriptions. Add additional categories where relevant.
4. Fill in technical specifications, or add/remove specification rows. Enter accurate values; templates suggest field names only.
5. Upload a JPG, PNG or WebP photo, up to 5 MB. The preview updates immediately.
6. Save as **Draft** to keep the entry private, or select **Published** and save to show it on the website. A photo is required for publication.
7. **View on website** opens the published detail page. Refresh an already-open client page to load new content.

All 483 imported products are editable. Published counts, search, categories and product pages use the managed catalog. Product links and visitor stars use stable IDs when other entries are archived.

## Companies and testimonials

1. Open **Companies → Add company**.
2. Enter the name, sector, optional short name, and display order. Smaller order numbers appear first.
3. Upload the actual logo. Choose white or dark background to suit it.
4. Optionally enter an approved quote, speaker name and role. Check the approval box only when publication is authorized.
5. Save as Draft or Published.

A company can be published with its logo and no quote. A published quote requires a speaker name and approval. Existing references are imported with no fabricated testimonials. Company entries appear in the home and projects sliders; approved quotes appear in their popups.

## Publishing, archiving and previews

- **Draft:** private; excluded from the public catalog and client slider.
- **Published:** visible on the website.
- **Archived:** hidden but retained for later editing or republishing.
- Changes apply when you save. The editor preview shows unsaved form content; the website shows the last saved published content.
- Leaving a form with unsaved changes prompts you first.
- Concurrent edits are checked; a stale form cannot silently overwrite a newer saved version.

## Backups and recovery

Use **Settings & backups → Download backup** regularly and before large changes. The JSON file includes product/company records and admin-uploaded images. It excludes admin credentials and the original catalog images, which remain in the website's `images` folder.

To restore: select the downloaded file, type **RESTORE**, and confirm. Restore replaces the managed catalog and companies, retains the admin account, and first snapshots the existing content. Uploaded images in the backup are restored with new private file names.

The server stores the last 30 content snapshots in `data/history`. These are JSON content snapshots, not full image backups. For emergency recovery with a snapshot: stop the server, preserve the current `data/content.json`, copy the selected snapshot to `data/content.json`, keep `data/uploads`, and restart.

**Preserve the `data` folder when upgrading or moving this website.** It contains managed content, password hash, uploads and content history. Also retain the original `images` folder.

## Login and account recovery

One owner/admin account is included. Change its password under **Settings & backups**; this signs out all admin sessions. Sessions also expire after 12 hours or when the server restarts.

If the password is lost, stop the server and run:

```bash
npm run setup -- --reset
```

Choose new credentials, then restart. This does not remove products, companies or uploaded images.

Automated deployment can create the account using `GTECH_ADMIN_USER` and `GTECH_ADMIN_PASSWORD` environment variables with `npm run setup`. Do not commit credentials. Clear the password environment variable after setup.

## Hosting

This version requires a persistent Node.js server; static-only hosting cannot save admin changes. For production, set:

```text
NODE_ENV=production
HOST=0.0.0.0
PORT=5500
PUBLIC_ORIGIN=https://your-domain.example
GTECH_DATA_DIR=/persistent/path/gtech-data
```

Set these in the hosting provider's environment settings, substituting your real domain and persistent storage path. `PUBLIC_ORIGIN` must have no trailing slash. Terminate HTTPS through the host/reverse proxy; its secure origin must match `PUBLIC_ORIGIN`. Never expose the project folder through another static server that serves `server`, `data` or credential files.

Run **one Node process** per data folder. This small CMS uses atomic JSON storage with snapshots, not a shared multi-instance database. Mount durable storage for `GTECH_DATA_DIR`, and keep off-server backups. The initial catalog is seeded only when `content.json` does not exist.

The admin uses an HTTP-only session cookie, CSRF checks, hashed passwords, login throttling, server-side validation and a restricted static-file allowlist. Admin scripts/styles are covered by a Content Security Policy. The public catalog contains published records only.

## Scope

- Includes products, company profiles, testimonials, uploads, drafts, archive, duplication, content previews, activity history, backup/restore and password management.
- Visitor stars stay in each visitor's browser. They are not orders and are not visible to the admin.
- No payments or checkout are added.
- The existing contact form remains a demo; this update does not add inquiry delivery or email.
- Existing site branding, contact details, public animations and layout remain unchanged.

## Verify the backend

```bash
npm test
```

The automated test uses a temporary account and temporary data, checks authorization, CSRF protection, validation, drafts/publishing, archiving, uploaded images, stale edits, backup restoration and password/session invalidation. It leaves the real catalog unchanged.
