# Gecko Home Assistant


[![GitHub Release][releases-shield]][releases]
[![GitHub Activity][commits-shield]][commits]

[![License][license-shield]](LICENSE)

[![hacs][hacsbadge]][hacs]
![Project Maintenance][maintenance-shield]

![installation_badge](https://img.shields.io/badge/dynamic/json?color=41BDF5&logo=home-assistant&label=integration%20usage&suffix=%20installs&cacheSeconds=15600&url=https://analytics.home-assistant.io/custom_integrations.json&query=$.gecko.total)
![Validate](https://github.com/gazoodle/gecko-home-assistant/actions/workflows/validate.yml/badge.svg)
![Lint](https://github.com/gazoodle/gecko-home-assistant/actions/workflows/lint.yml/badge.svg)


## Version History

v0.1.15
 - During the tidy and delint phase, constants were imported from HA 2025 locations, so this
   is now a minimum requirement. hacs.json updated accordingly.

v0.1.14
- Get validation & lint workflows running
- Expose temperature sensors for current temperature, set point temperature and real setpoint
  temperature which takes economy mode into consideration. These allow various automations to
  be written that otherwise would have to dig into the attributes of the climate control object
- Added 'Snapshot' button to dump data that might be useful in getting new spa features implemented

v0.1.13
- Bump the version number!

v0.1.12
- Removed warnings about light color modes
- Added French string table, thanks @claudegel
- Fixed ConfigType, thanks @grahamcraqer
- Use geckolib 0.4.16, it fixes some other HA warnings and issues
- Use Fan modes correctly, thanks @sicarriere
- Update docker container to use latest version from blueprint ... phew, that was 2 years of updates

_Component to integrate with [Gecko Spas](https://geckoalliance.com)._

**This component will set up the following platforms.**

Platform | Description
-- | --
`button` | Reconnect & snapshot buttons.
`binary_sensor` | Various on/off spa sensors.
`sensor` | Text/Enum spa sensors.
`switch` | Waterfalls
`fan` | Spa pumps, fans.
`light`  | Spa lights
`climate` | Spa water heater

## Example screen shot

![Screenshots][screenshotimg]

## Installation (HACS)

The preferred method to install is to use HACS.

## Installation (No HACS)

If you don't have/want HACS installed, you will need to manually install the integration

1. Using the tool of choice open the directory (folder) for your HA configuration (where you find `configuration.yaml`).
2. If you do not have a `custom_components` directory (folder) there, you need to create it.
3. In the `custom_components` directory (folder) create a new folder called `gecko`.
4. Download _all_ the files from the `custom_components/gecko/` directory (folder) in this repository.
5. Place the files you downloaded in the new directory (folder) you created.
6. Restart Home Assistant
7. In the HA UI go to "Configuration" -> "Integrations" click "+" and search for "Gecko"

Using your HA configuration directory (folder) as a starting point you should now also have this:

```text
custom_components/gecko/.translations/en.json
custom_components/gecko/__init__.py
custom_components/gecko/binary_sensor.py
custom_components/gecko/button.py
custom_components/gecko/climate.py
custom_components/gecko/config_flow.py
custom_components/gecko/const.py
custom_components/gecko/fan.py
custom_components/gecko/light.py
custom_components/gecko/manifest.json
custom_components/gecko/sensor.py
custom_components/gecko/spa_manager.py
custom_components/gecko/switch.py
```

## Using the snapshot functionality

The snapshot function allows you to generate a datablock that can be used during development and testing
to support new SPA features. To use, please open an issue on Github outlining what your requirements are.

Then, switch to the integration device page where you should find a "Snapshot" button in the "Diagnostics"
panel.

1. Place your spa into default state, i.e. powered up, but idle.
2. Press the "Snapshot" button
3. Activate whatever feature you are trying to provide functionality for.
4. Press the "Snapshot" button again.

Repeat steps 3 & 4 for as many times as necessary to capture all the states that your spa goes through
during you exercising the feature.

You should find this data in your log file but, for convenience, it's also in the persistent notification
panel on lovelace. Select the snapshot notification, expand the data block behind the "Click to expand"
label, and copy the data block (which begins ```{'Integration Version ...'```}). 

Add this data as a reply to your issue on Github. One snapshot per reply please otherwise it might get
too busy. Annotate the reply with a statement of what your spa was doing at the snapshot time, e.g.
"Idle" or "After turning RGB light to Red".
