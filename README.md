# Aramabul Depot

This repo stores heavy archive data for Aramabul.

It is not the live product repo.

Use it for:
- backup datasets
- non-Istanbul archive data
- scrape dumps and reports
- large research snapshots

The live product should stay in the web repo.
The Android shell should stay in the Android repo.

## Current Scope

This first version keeps:
- `data/non-istanbul/`
- Istanbul net scrape dumps
- backup json files
- report, cache, preview, and xls files
- split planning docs

## Notes

Do not treat this repo as the runtime source.
Live venue data still comes from PostgreSQL in the web product.
