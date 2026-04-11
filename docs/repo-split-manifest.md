# Repo Split Manifest

## Purpose

This file is the practical split list.

It says what should stay in the web repo and what should move out.

Use it before creating the new repos.

## Target Repos

- `aramabul-istanbul-web`
- `aramabul-depo`
- `aramabul-android`

## Rule Set

- If a file is needed to run the live Istanbul site, keep it in web.
- If a file exists mainly for archive, backup, scraping, or research, move it to depot.
- If a file belongs to the Flutter shell or Android web snapshot, move it to Android.
- If a script writes into `android_app/...`, it should not stay in the web repo long term.

## Keep In `aramabul-istanbul-web`

### Root product pages

Keep the live product and account pages:

- `index.html`
- `yeme-icme.html`
- `gezi.html`
- `istanbul-kesfet.html`
- `venue-detail.html`
- `favorites.html`
- `search.html`
- `profile.html`
- `about-settings.html`
- `account-settings.html`
- `feedback-settings.html`
- `help-settings.html`
- `language-settings.html`
- `verify-email.html`

Keep the admin pages:

- `admin-login.html`
- `admin-taxonomy.html`
- `admin-venues.html`
- `admin-auth.js`
- `admin-login.js`
- `admin-taxonomy.js`
- `admin-venues.js`

### Root shared frontend files

Keep:

- `styles.css`
- `profile.css`
- `web-runtime.js`
- `header-state.js`
- `header-i18n.js`
- `header-nav.js`
- `header-shell.js`
- `header-search-ui.js`
- `header-search-data.js`
- `header-search.js`
- `app.js`
- `city.css`
- `city.js`
- `gezi-kesfet.js`
- `istanbul-kesfet.js`
- `venue-detail.js`
- `favorites.js`
- `language-settings.js`
- `profile.js`

### Root category and discovery pages to review

These can stay short term if they are still linked or still served.
We can trim them later.

- `restaurant.html`
- `keyif*.html`
- `hizmetler*.html`
- `kultur*.html`
- `sanat*.html`
- `saglik-mekanlar.html`
- `seckin-mekanlar.html`
- `city.html`

### Backend

Keep all of:

- `backend/`
- `deploy/`

These are core app runtime pieces.

### Runtime config and package files

Keep:

- `package.json`
- `package-lock.json`
- `.env.example`
- `Dockerfile`
- `docker-compose.postgres.yml`
- `render.yaml`
- `POSTGRESQL_SETUP.md`
- `PRODUCTION_DEPLOY.md`

### Root assets

Keep only assets used by live web pages and admin.

Keep:

- `assets/` that are referenced by current product pages

Clean later:

- old one-off images that are no longer referenced

### Data that should stay in web

Keep only data needed by:

- `db:import:venues`
- live product support
- current Istanbul product scripts

Keep:

- `data/venues.json`
- `data/districts.json`
- `data/location-neighborhoods.json`
- `data/location-postcodes.json`
- `data/fallback-category-data.js`
- `data/fallback-data.js`
- `data/fallback-food-data.js`

Keep short term if product pages still use them or if current scripts still depend on them:

- `data/akaryakit.json`
- `data/asm.json`
- `data/atm.json`
- `data/dis-klinikleri.json`
- `data/duraklar.json`
- `data/eczane.json`
- `data/health-family-centers.json`
- `data/health-hospitals.json`
- `data/kargo.json`
- `data/kuafor.json`
- `data/nobetci-eczane.json`
- `data/noter.json` if present later
- `data/otopark.json` if present later
- `data/gezi-butik-oteller.json`
- `data/gezi-kamp-alanlari.json`
- `data/gezi-oteller-1-yildiz.json`
- `data/gezi-oteller-2-yildiz.json`
- `data/gezi-oteller-3-yildiz.json`
- `data/gezi-oteller-4-yildiz.json`
- `data/gezi-oteller-5-yildiz.json`
- `data/gezi-oteller-diger.json`
- `data/gezi-oteller.json`
- `data/keyif.json`
- `data/keyif-food.json`
- `data/keyif-restoran.json`
- `data/keyif-kafe.json`
- `data/keyif-kahvalti.json`
- `data/keyif-kebap.json`
- `data/keyif-doner.json`
- `data/keyif-pide.json`
- `data/keyif-cigkofte.json`
- `data/keyif-pub-bar.json`
- `data/keyif-michelin-guide.json`
- `data/ktb-tesis-kayitlari-gezi.json`
- `data/ktb-tesis-kayitlari-keyif.json`
- `data/ktb-oteller-yildizli.json`
- `data/ktb-pansiyon-ek-kayitlari.json`
- `data/ktb-tesis-turleri-gezi.json`
- `data/ktb-tesis-turleri-keyif.json`
- `data/kultur-camiler.json`
- `data/kultur-devlet-tiyatrolari.json`
- `data/kultur-magaralar.json`
- `data/kultur-muzeler.json`
- `data/kultur-opera-bale.json`
- `data/kultur-oren-yerleri.json`
- `data/kultur-ozel-tiyatrolar.json`
- `data/kultur-sehir-tiyatrolari.json`
- `data/kultur-selaleler.json`
- `data/sanat-galeriler.json`

### Scripts to keep in web

Keep scripts needed for product operations:

- `scripts/start-local.sh`
- `scripts/enrich-google-place-details.js`
- `scripts/discover-menu-links-from-websites.js`
- `scripts/discover-menu-links-from-platform-links.js`
- `scripts/add-harita-istanbul-venue.js`

Keep scripts needed for current Istanbul data maintenance, if we still use them:

- `scripts/fetch-fenerbahce-cafes.js`
- `scripts/merge-istanbul-local-keyif-venues.js`
- `scripts/apply-istanbul-cluster-cache-coordinates.js`
- `scripts/merge-harita-istanbul-into-venues.js`
- `scripts/clean-harita-istanbul-venue-duplicates.js`
- `scripts/delete-cleaned-harita-venues-from-db.js`

Keep only if still part of the active Istanbul pipeline:

- `scripts/fetch-gezi-butik-oteller.js`
- `scripts/sync-gezi-oteller-stars-with-ktb.js`
- `scripts/build-gezi-oteller-stars-from-turob.js`
- `scripts/clean-gezi-oteller-with-turob.js`
- `scripts/enrich-ibb-hotels.js`

Keep only if current product still needs refreshes from them:

- `scripts/fetch-keyif-kafe.js`
- `scripts/fetch-keyif-restoran.js`
- `scripts/fetch-keyif-kahvalti.js`
- `scripts/fetch-keyif-kebap.js`
- `scripts/fetch-keyif-doner.js`
- `scripts/fetch-keyif-pide.js`
- `scripts/fetch-keyif-cigkofte.js`
- `scripts/fetch-keyif-pub-bar-yandex-istanbul.js`
- `scripts/build-keyif-food-aggregate.js`

## Move To `aramabul-depo`

### Heavy archive data

Move all backup and report-heavy data:

- `data/*.backup.json`
- `data/*.pre-*.json`
- `data/*report*.json`
- `data/*preview*.json`
- `data/*cache*.json`

Move all source dump trees:

- `data/istanbul-net-kafe/`
- `data/istanbul-net-restoran/`

Move raw scrape or research files:

- `data/istanbul-net-kafe-1.html`
- `data/istanbul-net-kafe-deduped.json`
- `data/istanbul-net-kafe-extracted.json`
- `data/istanbul-net-restoran-deduped.json`
- `data/istanbul-net-restoran-detail-cache.json`
- `data/istanbul-net-restoran-details.json`
- `data/istanbul-net-restoran-extracted.json`
- `data/osm-istanbul-kafe.json`
- `data/osm-istanbul-restoran.json`
- `data/harita-restoran-grid-dense.json`
- `data/harita-restoran-grid-sample.json`
- `data/harita-oteller-sapko.json`

Move the archive split:

- `data/non-istanbul/`

Move office docs and raw spreadsheets:

- `data/Ruhsatlı Muayenehaneler.xls`
- `data/Ruhsatlı Poliklinikler.xls`

### Data scripts that belong in depot

Move scripts whose main job is collection, cleanup, merge, or archive work:

- `scripts/fetch-*`
- `scripts/build-*`
- `scripts/merge-*`
- `scripts/parse-*`
- `scripts/geocode-*`
- `scripts/report-*`
- `scripts/normalize-*`
- `scripts/remove-*`
- `scripts/fix-*`
- `scripts/dedupe-*`
- `scripts/resolve-google-photo-uris.js`
- `scripts/refresh-missing-websites.js`
- `scripts/enrich-instagram-from-websites.js`
- `scripts/enrich-instagram-via-search.js`
- `scripts/enrich-keyif-ratings.js`
- `scripts/enrich-istanbul-net-restoran-details.js`
- `scripts/enrich-istanbul-venue-cluster-coordinates.js`
- `scripts/enrich-kultur-muzeler-districts.js`
- `scripts/enrich-kultur-muzeler-google-maps.js`
- `scripts/enrich-kultur-muzeler-official-districts.js`
- `scripts/split-istanbul-datasets.js`

Move Python helpers used for pipeline work:

- `scripts/*.py`

Move generated cache and temp script output:

- `scripts/__pycache__/`

### Why depot gets these

These files are valuable, but they do not belong in the daily product repo.

They create weight, noise, and deploy risk.

## Move To `aramabul-android`

Move the whole directory:

- `android_app/`

This includes:

- Flutter app code
- platform folders
- Android and iOS config
- embedded web snapshots
- Android-side scripts

### Clean before or after move

Do not carry generated build output into the new Android repo if we can avoid it.

Ignore or remove from version control later:

- `android_app/build/`
- `android_app/.dart_tool/`
- `android_app/android/.gradle/`
- `android_app/ios/Flutter/ephemeral/`
- `android_app/linux/flutter/ephemeral/`
- `android_app/macos/Flutter/ephemeral/`
- `android_app/windows/flutter/ephemeral/`
- `android_app/macos/Pods/`

## Short-Term Exceptions

These can stay in web at first, even if we later move them.

- old category pages still linked from current navigation
- data files still read by legacy pages
- a few Istanbul scripts we still actively use during cleanup

The first split should favor safety over perfect purity.

## Immediate Clean Wins

These are the lowest-risk first moves.

1. Move `android_app/` to `aramabul-android`.
2. Move `data/non-istanbul/` to `aramabul-depo`.
3. Move `data/*.backup.json` and scrape dumps to `aramabul-depo`.
4. Keep `backend/`, `deploy/`, `data/venues.json`, and live pages in web.

## Validation Checklist After Split

After the first split, the web repo must still pass these checks:

1. `npm start` works.
2. `npm run db:migrate` works.
3. `npm run db:import:venues` works.
4. `127.0.0.1:8787` serves the homepage.
5. Admin login works.
6. `yeme-icme.html` still loads category data.
7. Venue detail pages still render photos and metadata.

## Next Task

The next implementation task should be:

- create `aramabul-android`
- move `android_app/`
- replace Android copy scripts in the web repo with a release note or external sync step

That is the cleanest first real split.
