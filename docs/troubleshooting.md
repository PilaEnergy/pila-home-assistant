# Troubleshooting

## Status stuck on "Disconnected" on the Pila screen

1. Confirm the IP address you entered matches Home Assistant's current LAN IP. If your router assigns dynamic addresses, set a DHCP reservation for Home Assistant.
2. Confirm the username/password are correct. Log into Home Assistant with those credentials in a browser to verify.
3. Confirm the Mosquitto add-on is **running** in Home Assistant (Settings → Add-ons → Mosquitto broker → "Start").
4. Check that port 1883 is reachable. From any device on the LAN: `nc -vz <HA_IP> 1883`.
5. Reboot Pila and watch the status indicator.

## Pila is connected but no entities appear in Home Assistant

1. Go to **Settings → Devices & services → MQTT** and look for a Pila device.
2. If missing, click **Configure** on the MQTT integration and use **Listen to a topic** to subscribe to `homeassistant/device/pila/#`. You should see a config message published shortly after Pila connects.
3. If you see config messages but no device, restart Home Assistant once — discovery occasionally fails to register on the first config push.
4. If you see no messages, the broker isn't receiving from Pila. Recheck network reachability.

## Entities appear but always show "Unknown" or "Unavailable"

1. Subscribe to `pila/state/#` from **Listen to a topic** to confirm state messages are flowing.
2. If state messages are flowing but entities are stale, the value template may not be finding the key. Open an [issue](https://github.com/PilaEnergy/pila-home-assistant/issues) with the raw state message.

## Outlet switch doesn't change state when I toggle it

1. The relay command is fire-and-forget. The state reflects what Pila reports back, not what you commanded. Give it 2–3 seconds.
2. If it never changes, check that no Pila-side automation (timer, schedule) is fighting your command.

## I want to keep the old broker but use a different MQTT user

Re-enter the new credentials on the Pila screen and tap **Save & Connect**. Pila will drop the existing connection and reauthenticate.

## I want to disconnect Pila from Home Assistant

Tap **Disconnect** on the Pila Home Assistant screen. The MQTT device will go offline in Home Assistant; entities remain in HA's registry. To fully remove, delete the device from **Settings → Devices & services → MQTT** in Home Assistant.

## Still stuck?

[Open an issue](https://github.com/PilaEnergy/pila-home-assistant/issues) with:
- Pila firmware version
- Home Assistant version
- MQTT broker (Mosquitto add-on / external)
- A description of what you've tried
