# Blueprints for Home Assistant

This repository contains some blueprints for Home Assistant. 

Home Assistant is an amazing home automation software that gives you full control over all your smart devices and allows you to integrate different platforms. To learn more about it check the [Home Assistant Website](https://www.home-assistant.io/) .

Blueprints are used, in Home Assistant, as templates for building automation quickly. If you want to learn more about it and start writing your own automation check the [Creating blueprints page](https://www.home-assistant.io/docs/blueprint/).

## Low Battery Notification

### Description

This is a template for creating an automation that will check all [battery class sensors](https://www.home-assistant.io/integrations/sensor/) for a low-battery condition, and then excute one or more [actions](https://www.home-assistant.io/docs/automation/action/), e.g. send a message with every sensor that has a low-battery condition to your phone.

The following types of battery sensors are supported:
* The regular percentage-type battery sensor (e.g. sensor.low_battery with a value representing the battery status in percentages)
* A binary sensor that indicates a low-battery condition when its state is 'on' (e.g. sensor_low_battery with a value of either 'on' or 'off', with 'on' representing a low-battery status)
* A regular sensor that uses fixed values to represent the battery status (e.g. sensor_low_battery with a value of 'high', 'medium', 'low' or some other values with one of them representing a low-battery state). The latter is commonly used by [Tuya](https://www.tuya.com/)-type devices.

Note that only battery sensors with the device class 'battery' will be checked. It's pretty common for [Tuya](https://www.tuya.com/)-type battery sensors not to set the device class to 'battery',  for such sensors you can use [customize](https://www.home-assistant.io/docs/configuration/customizing-devices/) to set the device class to the correct type.
```
customize:
  sensor.my_tuya_device_battery_state
    device_class: battery
```

The blueprint will let you set a treshold value for when precentage-type battery sensors should be considered to be in a low-battery state. It will also let you enable support for fixed-value type battery sensors, and to customize the string that represent a low-battery state for such sensors (e.g. 'low'). There are no further options for binary-type battery sensors, such sensors will automatically be checked if they exist.

You can also set the time of the day and days of the week when the automation should be executed.

You can use `{{sensors}}` in your [actions](https://www.home-assistant.io/docs/automation/action/), this will be substituted with a string that is acomma-separated list of all sensors with a low-battery status and their values.

You can also exclude one or more sensors from being checked, that is usefull to exclude for instance phones, tablets, and similar devices.

Notice: There is a bug in Home Assistant that causes boolean selectors not to be saved properly when an automation based on a blueprint is later being edited in the GUI, so any changes to your automation(s) based on this blueprint that involves changing the on/off selectors in the blueprint will not be saved. Their states will be saved correctly when you first create the automation, but for subsequent changes their states will not be saved/updated correctly. This bug is still present in HA version 2022.10.5, and a description of the bug can be found [here](https://github.com/home-assistant/frontend/issues/13206).

There are two possible workarounds:
1. Delete and re-create the automation.
2. Manually edit automations.yaml (remember to reload your automation by calling the service [automation.reload](https://www.home-assistant.io/docs/automation/services/)).


This blueprint is based on work by [@sbyx](https://gist.github.com/sbyx) and [@gmlupatelli](https://github.com/gmlupatelli/).

### Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/chjohans/blueprints_repo/master/low_battery_notification/low_battery_notification.yaml)

Just click on `IMPORT BLUEPRINT` above to add this blueprint to your [Home Assistant](https://www.home-assistant.io/) installation.

### Usage

After installing this blueprint you will find it in your [Home Assistant](https://www.home-assistant.io/) installation under `Settings` -> `Automations & Scenes` -> `Blueprints`. Just click on `CREATE AUTOMATION` and follow the instructions in the blueprint and the description above.

## Simple Weekly Scheduler

## Unavailable Entities Notification