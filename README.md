## Disclaimer

This project is not affiliated, associated, authorized, endorsed by, or in any way officially connected with Finder S.p.A.
The Finder BLISS name, as well as related names, marks, emblems and images, are registered trademarks of their respective owners.
This integration is provided for **research and interoperability purposes only**.
Use it at your own risk.

# Finder Bliss Thermostats (Home Assistant Custom Component)

A Home Assistant custom integration for **Finder BLISS** thermostats using the unofficial `pyFinderBliss` API client.

### Supported devices

| Model | Tag | Tested |
|---|---|---|
| Bliss WiFi Next (1C.91) | BLISS1 | Yes |
| Bliss 2 | BLISS2 | Partial |

---

## Features

### Climate entity

- **Current & target temperature** monitoring and control
- **HVAC modes**: Off (frost protection), Heat, Cool, Auto
- **Heating / Cooling** — switching between Heat and Cool automatically changes the device season (Winter/Summer)
- **HVAC action** — shows Heating, Cooling, or Idle based on the relay status
- **Schedule presets** — select named schedule programs configured in the Finder Bliss app (e.g. "Estate", "Freddo PT")

### Sensors

| Sensor | Device class | Unit | Category |
|---|---|---|---|
| Temperature | `temperature` | °C | — |
| Humidity | `humidity` | % | — |
| Battery | `battery` | % | Diagnostic |
| WiFi level | `signal_strength` | dBm | Diagnostic |
| Mode | — | — | Diagnostic |
| Set point | `temperature` | °C | — |
| Manual set point | `temperature` | °C | — |
| Season | — | — | Diagnostic |
| Thermal differential | `temperature` | °C | Diagnostic |
| Schedule | — | — | — |

The **Schedule** sensor shows the active preset name as its state and exposes per-day time blocks as attributes (e.g. `Monday: ["06:00-20:00: 19.0°C", "20:00-24:00: 18.0°C"]`).

Battery percentage is calibrated for 4xAA batteries in a 2S2P configuration (2.1V–3.0V range).

### Sync profile (select entity)

An editable select entity to control the device's cloud sync interval:

| Profile | Interval |
|---|---|
| Energy saving | 10 min |
| Normal | 5 min |
| Fast | 2 min |
| Super fast | 1 min |

Categorized as a **Config** entity.

### Credential management

- **Reconfigure** — update username/password from the integration's settings page (three-dot menu)
- **Reauth** — if credentials become invalid, Home Assistant automatically prompts for new ones

---

## Installation (via HACS)

1. Open **HACS** in your Home Assistant UI.
2. Go to **Integrations**.
3. Click the three dots in the top right and select **Custom repositories**.
4. Enter the repository URL: `https://github.com/marl1w/finderblissha`
5. Select category **Integration** and click **ADD**.
6. Search for **"Finder Bliss"** and click **Download**.
7. **Restart Home Assistant**.

## Configuration

1. Go to **Settings > Devices & Services > Integrations**.
2. Click **ADD INTEGRATION**.
3. Search for **"Finder Bliss Thermostats"**.
4. Enter your Finder Bliss app credentials (email and password).
5. The integration validates the credentials and creates climate, sensor, and select entities for each thermostat.

To update credentials later, go to the integration entry, click the three-dot menu, and select **Reconfigure**.

## Manual Installation

1. Download the contents of this repository.
2. Copy the `finderblissha` folder into your Home Assistant `custom_components` directory (e.g. `/config/custom_components/finderblissha/`).
3. Restart Home Assistant.
4. Follow the configuration steps above.

---

## Notes

- The integration communicates via the Finder Bliss cloud API (OAuth2 + SignalR WebSocket). It does **not** use local/Bluetooth communication.
- **Off mode** on BLISS1 devices activates frost protection (anti-freeze), not a full power-off.
- Thermal differential (hysteresis) is exposed as a read-only diagnostic sensor. It can be configured from the Finder Bliss app.
- The API is unofficial and may break if Finder changes their cloud service.

## Acknowledgements

This project is a fork of [condatek/finderblissha](https://github.com/condatek/finderblissha), the original Finder Bliss Home Assistant integration.

## Contributing

Contributions are welcome. Fork the repository and open a pull request.
