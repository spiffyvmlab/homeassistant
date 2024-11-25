# Rivian Efficiency Tracker

This package is designed to track the power efficiency of your Rivian vehicle. It calculates the efficiency in miles per kilowatt-hour (mi/kWh) based on the odometer readings and state of charge of the battery. Please note, this is still a work in progress, and therefor may not be 100% accurate.

## Description

The `rivian_efficiency.yaml` package includes:
- Input numbers for the last recorded odometer and state of charge.
- Template sensors to calculate the efficiency.
- Automations to update the last recorded values.

## Installation

1. Copy the `rivian_efficiency.yaml` file to your Home Assistant configuration directory.
2. Include the package in your `configuration.yaml` file:
    ```yaml
    homeassistant:
      packages: !include_dir_named packages
    ```

## Configuration

### Input Numbers

- `last_r1t_odometer`: Stores the last recorded odometer reading.
- `last_r1t_state_of_charge`: Stores the last recorded state of charge.

### Template Sensors

- `Rivian Efficiency`: Calculates the efficiency in mi/kWh.

### Automations

- `Update Last Rivian Odometer and State of Charge`: Updates the input numbers with the latest sensor values.

## Usage

1. Ensure your Rivian vehicle's odometer and battery state of charge sensors are available in Home Assistant.
2. The efficiency will be calculated automatically and can be viewed in the `Rivian Efficiency` sensor.

## Troubleshooting

- Ensure the sensor entities `sensor.r1t_odometer`, `sensor.r1t_battery_state_of_charge`, and `sensor.r1t_battery_capacity` are correctly configured and available.
- Verify that the automations are triggering correctly by checking the Home Assistant logs.

## License

This project is licensed under the MIT License.