<table>
<tr>
<td width="140">

<img src="https://raw.githubusercontent.com/kimzeuner/Indego-Weather-Based-Schedule/main/images/icon.png" width="140" alt="Bosch Indego Weather Based Schedule">

</td>
<td>

# Bosch Indego Weather Based Schedule Blueprint

Automatically generates and updates Bosch Indego mowing calendar slots based on hourly weather forecasts.

</td>
</tr>
</table>

![GitHub Release](https://img.shields.io/github/v/release/kimzeuner/Indego-Weather-Based-Schedule?style=for-the-badge)
![License](https://img.shields.io/github/license/kimzeuner/Indego-Weather-Based-Schedule?style=for-the-badge)
![Stars](https://img.shields.io/github/stars/kimzeuner/Indego-Weather-Based-Schedule?style=for-the-badge)
[![Donate](https://img.shields.io/badge/Donate-PayPal-00457C?style=for-the-badge&logo=paypal&logoColor=white)](https://www.paypal.me/KZeuner)

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/kimzeuner/Indego-Weather-Based-Schedule/main/indego_weather_based_schedule.yaml)

---

## Features

- **Weather-based scheduling** — generates mowing windows from hourly forecast data
- **Temperature limits** — configurable minimum and maximum thresholds
- **Rain detection** — probability and precipitation thresholds
- **Morning dew detection** — suppresses mowing when dew is likely
- **Two slots per day** — supports up to two mowing windows daily
- **Skip Today helper** — optional boolean to skip a day on demand
- **Auto-updates** — reschedules automatically when forecast conditions change
- **Change notifications** — optional alerts when the schedule is updated
- **Efficient** — skips API calls when the schedule hasn't changed

---

## Dependencies

> **Required**
>
> This blueprint requires the [Bosch Indego Integration](https://github.com/sander1988/Indego) and a weather entity that supports hourly forecasts via `weather.get_forecasts`.

---

## Installation

### One-Click Import (Recommended)

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/kimzeuner/Indego-Weather-Based-Schedule/main/indego_weather_based_schedule.yaml)

### Manual

1. Download `indego_weather_based_schedule.yaml`
2. Copy it to `/config/blueprints/automation/`
3. Restart Home Assistant or reload automations

---

## Required Helpers

### Input Text

Stores the last applied mowing plan — used to detect unchanged schedules and avoid unnecessary updates.

```yaml
input_text:
  indego_last_applied_plan:
    name: Indego Last Applied Plan
```

### Input Boolean *(optional)*

Allows skipping today's mowing slot on demand.

```yaml
input_boolean:
  indego_skip_today:
    name: Indego Skip Today
```

---

## Configuration

| Setting | Description |
|---|---|
| `Weather Entity` | Weather entity providing hourly forecast data |
| `Last Applied Plan Storage` | Input Text helper for storing the generated schedule |
| `Skip Today's Schedule` | Optional Input Boolean helper |
| `Earliest Mowing Time` | Start of the allowed mowing window |
| `Latest Mowing Time` | End of the allowed mowing window |
| `Minimum Temperature` | Minimum temperature required for mowing |
| `Maximum Temperature` | Maximum allowed temperature (`0` = disabled) |
| `Maximum Precipitation` | Maximum hourly precipitation allowed |
| `Maximum Rain Probability` | Maximum forecast rain probability allowed |
| `Min Temp / Dew Point Difference` | Threshold for morning dew detection |
| `Morning Dew Check Until Hour` | Hour until which dew checks are active |
| `Notifications` | Optional — receive alerts when the schedule changes |

---

## How It Works

Each run, the blueprint evaluates the hourly forecast for the next seven days across five criteria — temperature, dew point, rain probability, precipitation amount, and general forecast condition — and generates suitable mowing windows automatically. If the resulting schedule matches the last applied plan, no update is made.

---

## Contributing

Ideas, bug reports and pull requests are always welcome:

- Fork the repository
- Open an [Issue](https://github.com/kimzeuner/Indego-Weather-Based-Schedule/issues)
- Submit a Pull Request

---

## License

Released under the [MIT License](LICENSE).

---

## Disclaimer

This project is not affiliated with or endorsed by Bosch. Bosch, Indego, and related trademarks belong to their respective owners.
