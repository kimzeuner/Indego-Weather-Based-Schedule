# Indego Weather-Based Schedule Blueprint

![GitHub release](https://img.shields.io/github/v/release/kimzeuner/Indego-Weather-Based-Schedule)
![GitHub License](https://img.shields.io/github/license/kimzeuner/Indego-Weather-Based-Schedule)
![GitHub Repo stars](https://img.shields.io/github/stars/kimzeuner/Indego-Weather-Based-Schedule)

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/kimzeuner/Indego-Weather-Based-Schedule/main/indego_weather_based_schedule.yaml)

Automatically generates and updates Bosch Indego mowing calendar slots based on hourly weather forecasts.

---

## Features

- 🌦️ Weather-based mowing schedule generation
- 🌡️ Configurable minimum and maximum temperature limits
- 🌧️ Rain probability and precipitation thresholds
- 💧 Morning dew detection
- 📅 Up to two mowing slots per day
- 🚫 Optional "Skip Today" helper
- 🔄 Automatic schedule updates when forecast conditions change
- 📱 Optional notifications when the schedule changes
- ⚡ Avoids unnecessary API calls by detecting unchanged schedules

---

## Dependencies

⚠️ This blueprint requires the Bosch Indego integration:

https://github.com/WhyLev/Indego

You also need a weather entity that supports hourly forecasts via:

```yaml
weather.get_forecasts
```

---

## Installation

### One Click Import

Click the button below:

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/kimzeuner/Indego-Weather-Based-Schedule/main/indego_weather_based_schedule.yaml)

### Manual Installation

Download:

```text
indego_weather_based_schedule.yaml
```

and copy it to:

```text
/config/blueprints/automation/
```

Restart Home Assistant or reload automations afterwards.

---

## Required Helpers

### Input Text

Stores the last applied mowing plan.

```yaml
input_text:
  indego_last_applied_plan:
    name: Indego Last Applied Plan
```

### Input Boolean (Optional)

Allows skipping today's mowing schedule.

```yaml
input_boolean:
  indego_skip_today:
    name: Indego Skip Today
```

---

## Configuration

| Setting | Description |
|----------|-------------|
| Weather Entity | Weather entity providing hourly forecast data |
| Last Applied Plan Storage | Input Text helper used to store the generated schedule |
| Skip Today's Schedule | Optional Input Boolean helper |
| Earliest Mowing Time | Beginning of the allowed mowing window |
| Latest Mowing Time | End of the allowed mowing window |
| Minimum Temperature | Minimum temperature required for mowing |
| Maximum Temperature | Maximum temperature allowed for mowing (0 = disabled) |
| Maximum Precipitation | Maximum hourly precipitation allowed |
| Maximum Rain Probability | Maximum forecast rain probability allowed |
| Minimum Temperature / Dew Point Difference | Used for dew detection |
| Morning Dew Check Until Hour | Time until which dew checks are active |
| Notifications | Optional notifications when schedule changes |

---

## Example

The blueprint evaluates:

- Temperature
- Dew point
- Rain probability
- Precipitation
- Forecast conditions

and automatically generates suitable mowing windows for the next seven days.

---

## Participate 🎉

Ideas, improvements, bug reports and pull requests are always welcome.

Feel free to:

- Fork this repository
- Open an Issue
- Submit a Pull Request

---

## Disclaimer

This project is not affiliated with or endorsed by Bosch.

Bosch, Indego and related trademarks belong to their respective owners.
