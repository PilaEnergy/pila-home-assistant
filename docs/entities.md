# Entity reference

Every entity Pila publishes to Home Assistant, what it means, and what unit it's in.

The entity prefix in Home Assistant is `sensor.pila_*` / `switch.pila_*` / `select.pila_*`, depending on the device name you've assigned. If you renamed your Pila, the prefix changes accordingly.

## Sensors

### Power (instantaneous, in watts)

| Entity name | Description |
|---|---|
| Total Usage | Total load currently being powered by the Pila (battery + grid + solar combined). |
| Battery Charge / Discharge Rate | Signed power into/out of the battery pack. Positive = charging, negative = discharging. |
| Total Solar Input | Power currently arriving from solar. |
| Total AC Input | Power currently flowing in from the grid (AC inlet). |

### Battery

| Entity name | Description |
|---|---|
| Battery SOC | State of charge, 0–100 %. |
| Battery energy remaining | Energy left in the pack at the current state of charge, in Wh. |
| Backup Forecast | Estimated hours of backup runtime at current load, in hours. |
| Pila Status | Human-readable summary of what Pila is doing. One of: `Solar powering devices`, `Battery powering devices`, `Charging from solar`, `Charging from utility`, `Utility powering devices`, `Idle`. |

### Grid

| Entity name | Description |
|---|---|
| Grid Status | One of: `on_grid` (connected to and using utility power), `off_grid` (islanded — running on battery/solar), `idle_off_grid` (no grid and no AC output), `unknown`. |

### Lifetime energy totals (for Energy Dashboard)

These are cumulative `total_increasing` counters in Wh. They map to specific tiles on the Home Assistant Energy Dashboard — see the [Energy Dashboard guide](./energy-dashboard.md) for which to wire to which.

| Entity name | Description |
|---|---|
| Pila Lifetime Import | Total energy imported from the grid through Pila over the device's lifetime. |
| Battery Lifetime Charge | Total energy charged into the battery pack over its lifetime. |
| Battery Lifetime Discharge | Total energy discharged from the battery pack over its lifetime. |

> Coming soon: **Pila Lifetime Export** (grid export) and **Lifetime Solar Production**. These will be exposed once the underlying features ship.

## Per-outlet entities

For each AC and USB-C outlet on your Pila, you get:

| Entity | Type | Description |
|---|---|---|
| `{outlet name}` | switch | Turn the outlet on or off. State reflects current relay state. |
| `{outlet name} power` | sensor (W) | Power currently flowing through the outlet. |
| `{outlet name} Lifetime Energy` | sensor (Wh) | Cumulative energy delivered through the outlet. |

**Outlet naming.** If you've assigned an appliance name to an outlet in the Pila app (e.g. "Fridge"), Home Assistant uses that name. Otherwise it falls back to the orientation-based default ("USB Left", "USB Middle", "USB Right", "AC 1", etc.).

If you rename an outlet in the Pila app, the underlying entity_id in Home Assistant **does not change** — only the friendly name updates. To rename the entity_id itself, edit it in **Settings → Devices & services → MQTT → Pila → entity**.

## Controls

| Entity | Type | Values | Description |
|---|---|---|---|
| Grid mode | select | `on_grid`, `off_grid` | Switch Pila between on-grid and manual off-grid (island) mode. Selecting `off_grid` puts Pila into MANUAL_OFF_GRID_MODE; selecting `on_grid` returns to normal grid-connected operation. |

## Update cadence

Sensor values are pushed by Pila every TODO seconds. The state topic is `pila/state/{device_id}`; the config topic is `homeassistant/device/pila/{device_id}/config`.

## Notes for advanced users

- All entities are published via Home Assistant's [MQTT discovery](https://www.home-assistant.io/integrations/mqtt/#mqtt-discovery) protocol on the `homeassistant/` prefix.
- The discovery payload is republished on every (re)connect, so Pila will re-appear if you delete the device in HA and disconnect/reconnect.
- QoS for state messages is 2. Retained messages are used for connection-status topics only.
