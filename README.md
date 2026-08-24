# Pirate Weather Dynamic Location

Home Assistant custom integration that keeps a Pirate Weather config entry aligned with a moving GPS position.

It watches configurable latitude and longitude sensor entities, measures movement from the last successfully applied location, and updates the selected Pirate Weather integration once the configured distance threshold is exceeded.

## Version

Current release: **1.0.0**

## Requirements

- Home Assistant
- The Pirate Weather integration already configured
- Sensor entities that provide latitude and longitude values

## Installation

1. Create a directory named `pirateweather_dynamic_location` under your Home Assistant `custom_components` directory.
2. Copy the integration files from this repository into:

   `config/custom_components/pirateweather_dynamic_location/`

3. Restart Home Assistant.
4. Go to **Settings → Devices & services → Add integration**.
5. Search for **Pirate Weather Dynamic Location**.

## Configuration

The setup flow allows you to choose:

- GPS latitude sensor
- GPS longitude sensor
- Minimum movement before updating Pirate Weather, in kilometres
- Debounce delay after a GPS sensor update
- The Pirate Weather config entry to update

The default GPS entities are:

- `sensor.rutx50_gps_lat`
- `sensor.rutx50_gps_lon`

The default movement threshold is **25 km** and the default debounce delay is **2 seconds**.

## Sensors

The integration exposes diagnostic sensors for:

- Distance since the last successful location update
- Time of the last successful location update

## How it works

When either GPS sensor changes, the integration waits for the debounce period and reads both coordinates. If the position has moved farther than the configured threshold, it updates only the latitude and longitude fields of the selected Pirate Weather config entry and reloads Pirate Weather.

The last successfully applied coordinates are stored persistently so Home Assistant restarts do not cause unnecessary updates.

## Multiple Pirate Weather instances

If more than one Pirate Weather integration is configured, select the intended target in this integration's options. If no target is selected, the first available Pirate Weather entry is used.

## License

No license has been specified for this repository.
