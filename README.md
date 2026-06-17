# Pila + Home Assistant

Monitor and control your Pila battery from [Home Assistant](https://www.home-assistant.io/) over MQTT.

> ⚠️ **Unofficial integration.** Pila does not currently have a "Works with Home Assistant" certification. This integration works by publishing MQTT discovery messages to a broker that you run on your Home Assistant instance. Bring your own broker — we recommend the [Mosquitto add-on](https://www.home-assistant.io/integrations/mqtt/#setting-up-a-broker).

> ℹ️ **One Pila per Home Assistant instance.** Each Home Assistant instance can connect to a single Pila device. Mesh-level views (multiple Pilas as one site) are not exposed through this integration today.

## What you get

Once connected, your Pila shows up as a single device in Home Assistant with sensors for power flow, battery state, lifetime energy counters, and switches for each outlet. You can drop these into the Energy Dashboard, build custom Lovelace cards, and trigger automations.

![Pila device in Home Assistant](./images/device-overview.png) <!-- TODO: add screenshot -->

## Contents

- [Setup](./docs/setup.md) — connect Pila to your Home Assistant broker
- [Entity reference](./docs/entities.md) — every sensor, switch, and select Pila publishes
- [Energy Dashboard](./docs/energy-dashboard.md) — wiring Pila into the HA Energy Dashboard
- [Example dashboards](./examples/dashboards/) — Lovelace YAML you can paste in
- [Example automations](./examples/automations/) — common Pila automations
- [Troubleshooting](./docs/troubleshooting.md)
- [Changelog](./CHANGELOG.md)

## Quick links

- Buy a Pila: [pilaenergy.com](https://pilaenergy.com)
- Report a bug: [Issues](https://github.com/PilaEnergy/pila-home-assistant/issues)
- Home Assistant Energy Dashboard docs: [home-assistant.io/docs/energy](https://www.home-assistant.io/docs/energy/)

## Compatibility

| Requirement | Notes |
|---|---|
| Pila firmware | TODO — minimum supported version |
| Home Assistant | 2024.x or newer (MQTT discovery v2 schema) |
| MQTT broker | Any MQTT 3.1.1 broker. Mosquitto add-on recommended. |
| Network | Pila and Home Assistant must be on the same LAN |
| TLS | Plaintext only on port 1883 today. TLS support is planned. |

## License

TODO
