# Wiring Pila into the Energy Dashboard

Home Assistant's [Energy Dashboard](https://www.home-assistant.io/docs/energy/) is the easiest way to visualize where your power is coming from and going.

## What you can wire up today

| Energy Dashboard tile | Pila entity |
|---|---|
| **Grid consumption** | `Pila Lifetime Import` |
| **Battery in** (charge) | `Battery Lifetime Charge` |
| **Battery out** (discharge) | `Battery Lifetime Discharge` |

## Coming soon

These tiles will be supported once the underlying Pila features ship:

| Energy Dashboard tile | Status |
|---|---|
| **Return to grid** (export) | Waiting on backfeeding support |
| **Solar production** | Waiting on solar production reporting |

## Step-by-step

1. In Home Assistant, go to **Settings → Dashboards → Energy**
2. Under **Electricity grid**, click **Add consumption** and pick `Pila Lifetime Import`
3. Under **Home battery storage**, click **Add battery system**, then:
   - **Energy going into the battery**: `Battery Lifetime Charge`
   - **Energy coming out of the battery**: `Battery Lifetime Discharge`
4. (Optional) Add your electricity tariff if you want cost data alongside

After a few hours of data flowing in, the dashboard will start showing daily energy summaries.

## Tips

- The Energy Dashboard uses **cumulative** (`total_increasing`) counters, not instantaneous power. The lifetime counters Pila publishes are designed for this — don't try to wire instantaneous `Battery Charge / Discharge Rate` here.
- If a tile shows "Unknown" for more than a few hours, Pila probably hasn't published the entity yet. Check the [troubleshooting guide](./troubleshooting.md).
