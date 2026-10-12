# GTech website + admin panel

The client site retains its animated home and service visuals, product catalog, company slider, and starred-products drawer. The new admin panel manages the content shown on the website.

## Run

Requires Node.js 22 or newer. Open this folder in VS Code and run:

```bash
npm run setup
npm start
```

The setup command creates your administrator account with your own password. No default credentials are included. No dependency installation is required.

- Website: http://localhost:5500
- Admin: http://localhost:5500/admin

Use `npm start` for future runs. See **ADMIN-GUIDE.md** for step-by-step editing, backups, recovery and production hosting.

## Administration

- All 483 source products and 10 existing companies are imported and editable.
- Product templates, specification fields, photo uploads and content previews.
- Company logos, sector labels, display order and approved testimonials.
- Draft / Published / Archived status; duplicate products as drafts.
- Search, filters and paginated content management.
- Password-protected administration, session controls and password changes.
- Downloadable backups, restore, recent activity and automatic content snapshots.

New published content is included when a visitor loads or refreshes the website. Opening `index.html` directly or using Live Server only displays the original static snapshot. The admin requires the included Node server.

## Files and persistence

`server/seed.json` contains the initial content. The server creates `data/content.json` on first startup. Admin credentials, uploads and automatic snapshots are also kept in `data`, or in the path configured by `GTECH_DATA_DIR`.

**Back up and preserve the data folder and original images when upgrading.** Do not upload credential/data files to a public static host. Production hosting requires HTTPS and persistent storage; configuration is in ADMIN-GUIDE.md.

## Existing content notes

The original Getaway product snapshot was retrieved October 5, 2026. Sources for all 483 records and their 428 unique primary images are in `CATALOG-SOURCES.json`; other images are documented in `IMAGE-SOURCES.md`. The catalog is not a live inventory feed; confirm specifications and availability with the supplier.

No client testimonials were supplied; the initial company entries have no invented quotes. The two specific Lebanese ministries represent the earlier ministry examples and should be confirmed before public use. Manufacturer installation photography demonstrates technology in real settings and does not assert GTech project authorship. The stock CEO portrait is marked illustrative.

The existing contact form remains a demo and does not send requests. Visitor stars are saved locally in each visitor's browser. No payments, checkout or order management is added.

Run `npm test` to verify the backend using isolated temporary data.
