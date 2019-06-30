# Thermostats Update

This app updates Z-Wave thermostats entities (e.g. Danfoss 014G0013) state and current temperature from external sensors in the [Home Assistant](https://home-assistant.io/).

This is [AppDaemon](appdaemon.readthedocs.io/) app.

You can install this app via [HACS](https://custom-components.github.io/hacs/) or just download `thermostats_update.py` file and save it in `/config/apps` folder.

Go to [HA community](https://community.home-assistant.io/t/update-current-temperature-for-z-wave-thermostats/32834) for support and help.

## Configuration example
```yaml
thermostats_update:
  module: heating_thermostats_update
  class: HeatingThermostatsUpdate
  rooms:
    kitchen:
      thermostat: climate.thermostat_kitchen
      sensor: sensor.temperature_kitchen
    room:
      thermostat: climate.thermostat_room
      sensor: sensor.temperature_room
    bathroom:
      thermostat: climate.thermostat_bathroom
      sensor: sensor.temperature.bathroom
  heat_state: 'auto'
  idle_state: 'idle'
  idle_heat_temp: 10
  state_only: true
  wait_for_zwave: true
```
## Script arguments
key | optional | type | default | description
-- | -- | -- | -- | --
`rooms` | False | dictionary | | dictionary of rooms it's thermostats and sensors
`thermostat` | False | string | | thermostat `entity_id`
`sensor` | True | string | | sensor `entity_id`
`heat_state` | True | string | `heat` | name of heating state, changing this from default value will broke compatibility with HomeKit
`idle_state` | True | string | `off` | name of idle state, changing this from default value will broke compatibility with HomeKit
`idle_heat_temp` | True | float | `8` | temperature value between `idle` and `heat` states
`state_only` | True | boolean | `false` | with `state_only` set to `true` script will update only state of the thermostat
`wait_to_zwave` | True | boolean | `true` | defines whether the script has to wait for the initialization of the Z-wave component after Home Assistant restart
