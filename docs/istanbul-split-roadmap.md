# Istanbul Split Roadmap

## Goal

Split the product into three clear repos.

- `aramabul-istanbul-web`: the live Istanbul product
- `aramabul-depo`: heavy data, backup files, and research scripts
- `aramabul-android`: Flutter shell and Android web bundle snapshots

This keeps daily product work fast and keeps archive data out of the main app repo.

## Why This Path

Today the repo does three jobs at once.

- It runs the live web product.
- It stores large archive and backup data.
- It stores the Android shell and mirrored web assets.

That makes deploys heavier, reviews noisier, and the mental model harder.

The new split keeps one source of truth for each concern.

- Web repo: product and API
- Depot repo: archive and pipeline work
- Android repo: mobile shell

## Repo Roles

### aramabul-istanbul-web

This repo should contain only what is needed to build, run, and deploy the Istanbul product.

Keep:

- root web pages used by the live product
- shared frontend files like `styles.css`, `header-*.js`, `web-runtime.js`
- `backend/`
- `deploy/`
- `assets/` used by the live web pages
- `scripts/` needed for live import, migration, and selected Istanbul data updates
- small runtime data files that the scripts still need
- `package.json`, lockfile, env examples, deploy docs

Do not keep:

- large backup json files
- non-Istanbul archive datasets
- research dumps and one-off scrape outputs
- Android project files

### aramabul-depo

This repo should be the long-term storage and pipeline workspace.

Keep:

- `data/non-istanbul/`
- large backup files from `data/`
- research output files
- source snapshots and scrape dumps
- scripts that exist only for data collection, cleanup, merge, or archive work

This repo is not the live app.

It is the warehouse and workshop.

### aramabul-android

This repo should contain only the mobile shell and the web snapshot it embeds.

Keep:

- Flutter app under `android_app/`
- Android-specific assets
- copied web bundle snapshots used by the app
- a simple sync or release process from the web repo

The Android repo should not be the main place where product work starts.

The web repo stays first.

## Source Of Truth Rules

After the split, we should keep these rules strict.

- Live product code starts in `aramabul-istanbul-web`.
- Live venue data comes from PostgreSQL in the web product.
- `data/venues.json` stays an import input, not the runtime source.
- Android does not mirror every web commit right away.
- Android takes stable web snapshots on purpose.

That last point matters the most.

We do not want Android to break every time we tune the web UI.

## Recommended Release Model

Use the second model we discussed.

- Web moves first.
- Android follows after a stable checkpoint.
- Depot is updated only when data work needs it.

That means:

1. Build or improve the feature in `aramabul-istanbul-web`.
2. Verify it on web.
3. Mark a stable snapshot.
4. Copy the needed web assets into `aramabul-android`.
5. Test the mobile shell.
6. Release Android later, on its own pace.

This keeps mobile work calm and predictable.

## What The Current Repo Tells Us

The current repo already points to this split.

- `data/` is very large and includes many backup files.
- `android_app/` is much larger than the web app itself.
- `scripts/sync-shared-web-assets.js` already treats the root web files as the source and Android as a target.

That is a good sign.

It means the codebase already wants this separation.

## Phase Plan

### Phase 1: Freeze the Boundaries

Goal: define what belongs where before moving anything.

Do now:

- list the files that are part of the live Istanbul product
- list the scripts needed for deploy, migrate, import, and photo enrichment
- mark all large backup and archive data for depot
- mark all Android files for the Android repo

Output:

- one keep list for web
- one move list for depot
- one move list for Android

### Phase 2: Create `aramabul-istanbul-web`

Goal: make the web repo small and production-focused.

Move out:

- `android_app/`
- large archive data
- large backup files
- non-Istanbul datasets

Keep only scripts that support:

- `db:migrate`
- `db:import:venues`
- selected Istanbul-only data refresh tasks
- selected admin and Google enrichment flows that still matter in product work

At the end of this phase, deploy should still work exactly as today, but with less weight.

### Phase 3: Create `aramabul-depo`

Goal: preserve all valuable data work without dragging the app repo down.

Move here:

- large `data/*.backup.json` files
- `data/non-istanbul/`
- scrape outputs that are not needed by the live app
- scripts whose only job is archive or research data generation

Add short docs:

- where fresh outputs should be written
- how data gets promoted back into the web repo when needed

### Phase 4: Create `aramabul-android`

Goal: make Android a clean consumer of stable web snapshots.

Move here:

- the Flutter shell
- `android_app/assets/web`
- `android_app/assets/app_web`

Then replace the current sync habit with a small release rule:

- snapshot from a known web commit
- sync the shared web files
- test on device
- release when ready

### Phase 5: Simplify Tooling

Goal: remove cross-repo confusion.

In the web repo:

- remove scripts that write directly into Android folders
- keep only product-facing scripts

In the Android repo:

- add a simple script or doc to import a web snapshot

In the depot repo:

- keep heavy data scripts there
- document how to export a clean `venues.json` back to web when needed

## First File Groups To Move

These are the safest early wins.

Move to `aramabul-depo` first:

- `data/non-istanbul/`
- `data/*.backup.json`
- old preview and report json files
- html page dumps under `data/`

Move to `aramabul-android` first:

- `android_app/`

Keep in `aramabul-istanbul-web`:

- `backend/`
- live root pages
- shared web JS and CSS
- live `assets/`
- `data/venues.json`
- small data helpers that live scripts still read

## Risks And How We Control Them

### Risk: Android falls behind web

This is acceptable if we treat Android as a scheduled snapshot consumer.

The fix is process, not more coupling.

### Risk: a script still writes into Android paths

We already found many scripts that do this.

We should move those scripts with the Android or depot split, or rewrite only the few that still matter.

### Risk: missing runtime data after cleanup

We avoid this by moving files in phases and keeping deploy smoke tests in the web repo.

### Risk: too much work in one cut

Do it in slices.

Do not split all three repos in one day.

## Recommended Order

This is the order I recommend.

1. Write the keep and move manifest.
2. Split out `aramabul-android`.
3. Trim the web repo to Istanbul live product files.
4. Move heavy archive data into `aramabul-depo`.
5. Clean scripts after the repos are stable.

This order lowers risk because Android is the cleanest big boundary.

## Success Criteria

We should call the split successful when:

- web deploy is smaller and easier
- Android no longer sits inside the web repo
- heavy archive data no longer rides along with app work
- product changes start in the web repo first
- Android updates happen only from stable snapshots

## Next Recommended Step

The next practical move is to produce a real file manifest.

That means:

- exact folders to keep in `aramabul-istanbul-web`
- exact folders to move to `aramabul-depo`
- exact folders to move to `aramabul-android`

That manifest should be the next task before we move files.
