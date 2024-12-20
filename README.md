# Custom Component DalyBMS for ESPHome

This repository is a collection of my custom components for [ESPHome](https://esphome.io/).
Just tried on Wemos D1 Mini.

Add sensors (measurements):
```
    on_failure_status:
    power:
    bms_watchdog:
    cycle:
    cell_voltage_difference:
```
Add binary_sensors:
```
    cell_1_balance_active:
    ...
    cell_16_balance_active:
```
Add sensors (level 1 + 2 setup - just reading):
```
    cell_level_1_alarm_high_voltage:
    cell_level_2_alarm_high_voltage:
    cell_level_1_alarm_low_voltage:
    cell_level_2_alarm_low_voltage:

    battpack_level_1_alarm_high_voltage:
    battpack_level_2_alarm_high_voltage:
    battpack_level_1_alarm_low_voltage:
    battpack_level_2_alarm_low_voltage:

    cell_level_1_alarm_difference_temperature:
    cell_level_2_alarm_difference_temperature:

    cell_level_1_alarm_difference_voltage:
    cell_level_2_alarm_difference_voltage:

    cell_nominal_capacity:
    cell_nominal_voltage:
```
## Usage

To use the components provided by this repository, simply add this to your `.yaml` definition:

```yaml
external_components:
  - source: github://SirUlbrich/
    components: [DalyBMS]
```

More information can be found [here](https://esphome.io/components/external_components.html).

## Components

### [daly_bms](components/daly_bms)


## How to use / example ESPHome configuration

configuration like original [ESPHome-Daly_BMS](https://esphome.io/components/sensor/daly_bms.html)

you can use more than one daly:
```
uart:
  - id: uart1
    tx_pin: GPIO17
    rx_pin: GPIO16
    baud_rate: 9600
  - id: uart2
    tx_pin: GPIO22
    rx_pin: GPIO21
    baud_rate: 9600

daly_bms:
  - uart_id: uart1
    id: bms1
    update_interval: 20s
  - uart_id: uart2
    id: bms2
    update_interval: 20s
```
you can get failure status code: 
change "template_sens" to your template sensor.

More information can be found [here](https://esphome.io/components/sensor/template.html).

```daly_bms:
  - uart_id: uart1
    id: bms1
    update_interval: 20s
    on_failure_status:
    - lambda: id(fault_code).publish_state(x[7]);
    ...
    ...
sensor:
  - platform: template
    name: Fehlercode
    id: fault_code
```


Many thanks to ssieb for helping me.