# Changelog

All notable changes to the Pila Home Assistant integration.

## Unreleased

### Added
- Initial public documentation.

### Changed
- Per-outlet entity names now prefer the user-assigned appliance name (set in the Pila app) over the orientation-based default.
- Grid mode select simplified to `on_grid` / `off_grid` only.
- Friendlier entity names across the board (e.g. "Aggregated load" → "Total Usage").
- "Battery state" replaced with **Pila Status**, a human-readable summary string.
- "Grid status" + "Grid connection mode" consolidated into a single **Grid Status** entity.

### Removed
- **Power target** number entity (was write-only with no state feedback).
- **Battery full capacity** sensor (rarely useful in Home Assistant).
- `import_target` and `export_target` options on Grid mode select.

### Pending
- **Pila Lifetime Export** sensor — will ship alongside backfeeding support.
- **Lifetime Solar Production** sensor — will ship once solar production reporting is ready.
