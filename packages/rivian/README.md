# Home Assistant Vampire Drain Tracking Package

This package provides a comprehensive setup for tracking the vampire drain of an electric vehicle (EV) using Home Assistant. It includes input helpers, template sensors, and automations to calculate and display the amount of battery lost to vampire drain since the last charge.

## Installation

1. **Create the `packages` Directory**:
   - Navigate to the directory where your `configuration.yaml` file is located.
   - Create a new directory named `packages`.

2. **Add the Package File**:
   - Inside the `packages` directory, create a new file named `vampire_drain.yaml`.
   - Copy the contents of the provided `vampire_drain.yaml` file into this new file.

3. **Include the Packages Directory**:
   - Add the following line to your `configuration.yaml` file to include the `packages` directory:

   ```yaml
   homeassistant:
     packages: !include_dir_named packages
   ```

4. **Validate and Restart Home Assistant**:
   - Validate the configuration in Home Assistant.
   - Restart Home Assistant for the changes to take effect.

## Configuration

### Input Helpers

The following input helpers are created to store the initial and last charge state of charge, as well as the vampire drain in kWh:

- `input_number.ev_initial_range`
- `input_number.ev_initial_state_of_charge`
- `input_number.ev_last_charge_state_of_charge`
- `input_number.ev_vampire_drain_kwh_lost`

### Template Sensors

The following template sensors are created to calculate and display the vampire drain:

- `sensor.ev_vampire_drain_kwh_lost`: Calculates the kWh lost to vampire drain.
- `sensor.ev_vampire_drain_since_last_charge`: Displays the kWh lost to vampire drain since the last charge.
- `sensor.ev_vampire_drain_percentage`: Displays the percentage of battery lost to vampire drain since the last charge.

### Automations

The following automations are created to capture the state of charge and calculate the vampire drain:

- `Capture Last Charge State of Charge`: Captures the state of charge when the vehicle finishes charging.
- `Capture Initial State of Charge`: Captures the initial state of charge when the vehicle shifts to Park.
- `Calculate Vampire Drain`: Calculates the vampire drain since the last charge.

## Dashboard Card

To display the vampire drain information on your Home Assistant dashboard, add the following configuration to your Lovelace dashboard:

```yaml
type: entities
entities:
  - entity: sensor.ev_vampire_drain_since_last_charge
    name: Vampire Drain (kWh)
  - entity: sensor.ev_vampire_drain_percentage
    name: Vampire Drain (%)
title: Vampire Drain Since Last Charge
```

## Dependencies:

- [Rivian Integration](https://github.com/bretterer/home-assistant-rivian)

## Notes

The vampire drain statistics are calculated by comparing the state of charge (SOC) of the vehicle between charges and between drives. The SOC is not a perfect measure of the battery capacity, and the vampire drain statistics are not perfect measures of the actual vampire drain. The statistics are meant to give a rough idea of the vampire drain, and should not be taken as exact measurements.

The statistics are calculated by comparing the SOC of the vehicle at the start of a drive to the SOC at the end of the drive, and by comparing the SOC at the end of a drive to the SOC at the start of the next drive. The difference in SOC is used to calculate the vampire drain in kWh and as a percentage of the battery capacity.

The vampire drain statistics are calculated for each drive, and for the total vampire drain since the last charge. The statistics are reset to zero when the vehicle is charged.

The statistics are calculated using the data from the Rivian Integration, which provides the SOC of the vehicle at the start and end of each drive. The SOC is used to calculate the vampire drain in kWh and as a percentage of the battery capacity.

The statistics are displayed in the Home Assistant dashboard as two sensors: `sensor.ev_vampire_drain_since_last_charge` and `sensor.ev_vampire_drain_percentage`. The sensors show the total vampire drain since the last charge in kWh and as a percentage of the battery capacity, respectively.

Statistics are updated every time the SOC of the vehicle is updated in the Rivian Integration. The statistics are updated in real-time, and are always up-to-date with the latest data from the vehicle.

Although it may be possible to fix in future versions, this package and the resulting statistics are only from the time the package is installed. It does not have any historical data from before the package was installed.


## Disclaimers:

1. I am not responsible if you break something in your Home Assistant configuration by using this package. Use at your own risk, and always have backups of your configuration files.
2. This package is not affiliated with Rivian, and is not an official integration. It is a custom package that uses the data from the Rivian Integration to calculate vampire drain statistics.
3. I do not own, maintain, or support the Rivian Integration. If you have issues with the Rivian Integration, please contact the maintainer of that integration.
4. This is still a work in progress, and there may be bugs or issues with the package. If you encounter any issues, please let me know so that I can fix them.