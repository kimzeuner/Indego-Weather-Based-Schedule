# Indego Weather-Based Schedule Blueprint

This Home Assistant Blueprint automatically generates and updates Bosch Indego mowing calendar slots based on hourly weather forecast data.

The blueprint calculates suitable mowing windows by evaluating precipitation, rain probability, temperature, and dew point conditions. It updates the Bosch Indego weekly mowing schedule only when the calculated plan has changed, reducing unnecessary API calls.

## Features

- Creates up to two mowing slots per day
- Uses hourly weather forecast data
- Configurable mowing time window
- Configurable minimum temperature
- Optional maximum temperature limit
- Configurable precipitation and rain probability thresholds
- Morning dew check based on temperature and dew point difference
- Optional helper to skip mowing for the current day
- Stores the last applied plan to avoid unnecessary updates

## Dependencies

This blueprint requires the Bosch Indego Lawnmower integration:

https://github.com/WhyLev/Indego

You also need a Home Assistant weather entity that supports hourly forecast data via `weather.get_forecasts`.

## Required Helpers

Create the following helpers in Home Assistant before using this blueprint.

### Input Text

Used to store the last applied mowing plan.

```yaml
input_text:
  indego_last_applied_plan:
    name: Indego Last Applied Plan
```

### Input Boolean (Optional)

Used to skip mowing for the current day.

```yaml
input_boolean:
  indego_skip_today:
    name: Indego Skip Today
```

## Installation Methods

### Manual Installation

Download the blueprint YAML file and place it in your Home Assistant configuration directory:

```text
/config/blueprints/automation/indego_weather_based_schedule.yaml
```

After copying the file, reload automations or restart Home Assistant.

### Import from GitHub

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)]([YOUR_RAW_BLUEPRINT_URL](https://raw.githubusercontent.com/kimzeuner/Indego-Weather-Based-Schedule/refs/heads/main/indego_weather_based_schedule.yaml))

Use the raw GitHub URL of the blueprint YAML file when importing it into Home Assistant.

Example:

```text
https://raw.githubusercontent.com/<user>/<repository>/<branch>/indego_weather_based_schedule.yaml
```

In Home Assistant:

```text
Settings → Automations & Scenes → Blueprints → Import Blueprint
```

Paste the raw URL and import the blueprint.

## Configuration

### Weather Entity

Select the weather entity that provides the hourly forecast data.

### Last Applied Plan Storage

Select the `input_text` helper used to store the last generated mowing plan.

### Skip Today's Schedule

Optional `input_boolean` helper. When enabled, mowing slots for the current day will be skipped.

### Earliest Mowing Time

Start of the daily mowing window. Forecast hours before this time are ignored.

**Default:** `08:00`

### Latest Mowing Time

End of the daily mowing window. Forecast hours after this time are ignored.

**Default:** `20:00`

### Minimum Temperature

Minimum outside temperature required for mowing.

**Default:** `8 °C`

### Maximum Temperature

Maximum outside temperature allowed for mowing.

Set this value to `0` to disable the upper temperature limit.

**Default:** `0 °C` (disabled)

### Maximum Precipitation

Maximum hourly precipitation amount allowed for mowing.

**Default:** `0.5 mm`

### Maximum Rain Probability

Maximum rain probability allowed for mowing.

**Default:** `75 %`

### Minimum Temperature / Dew Point Difference

Minimum required difference between air temperature and dew point during the morning dew check period.

A smaller difference usually indicates a higher chance of wet grass.

**Default:** `2 °C`

### Morning Dew Check Until Hour

Morning hours before this time are checked for excessive dew.

Example: `10` means the dew check is active from `00:00` until `09:59`.

**Default:** `10`

## Notes

- The blueprint creates a maximum of two mowing slots per day.
- Each mowing slot must be at least two hours long.
- The weekly Indego calendar is only updated when the calculated plan changes.
- If the selected weather entity does not provide `precipitation`, `precipitation_probability`, `temperature`, or `dew_point`, results may be incomplete.

## Participate 🎉

Ideas, improvements, bug reports, and pull requests are always welcome.

Feel free to fork the repository, improve the blueprint, and create a pull request.
