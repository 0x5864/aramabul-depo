# Berber and Kuafor Archive

Generated from the live PostgreSQL database on 2026-09-01.

## Scope

- Domain: `hizmetler`
- Removed memberships: `berber`, `kuafor`
- Selected venues: 5,761
- Venues removed from the live database: 5,754
- Venues kept because they also have an active membership: 7
- Removed Berber and Kuafor memberships: 5,764

`venues.json` contains the full venue rows and the venue-owned related rows needed for a controlled restore. User favorite rows are excluded. The selected venues had no favorite rows at archive time.

## Files

| File | Bytes | SHA-256 |
| --- | ---: | --- |
| `venues.json` | 13,041,420 | `869a023dad3607d3d958e11d151964fb6e056581cb91f5e1916fe3594fa0c4a7` |
| `source-berber.json` | 293,772 | `15dbbb1a00a72dd8d7cbc87fcf3102e9ae12c93b644560a62c1cc808b69475d4` |
| `source-kuafor.json` | 297,138 | `e3193334d70c825b14bba44eb36ec7091528310d9fa97a715f828d68073a7488` |

## Restore Notes

1. Verify every file checksum before use.
2. Restore `records.venues` first.
3. Restore the rows under `records.related` after their venue rows exist.
4. Review the seven `preservedVenueIds` before restoring hairdresser memberships. They stayed live under another active category.
5. Do not restore user favorites from this archive; they were intentionally excluded.
