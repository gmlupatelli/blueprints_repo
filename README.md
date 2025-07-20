# Home Assistant Blueprints Collection

This repository contains a collection of well-documented, production-ready blueprints for Home Assistant automation.

## About Home Assistant & Blueprints

[Home Assistant](https://www.home-assistant.io/) is an amazing home automation platform that gives you full control over all your smart devices and allows you to integrate different platforms seamlessly.

[Blueprints](https://www.home-assistant.io/docs/blueprint/) are reusable automation templates that make it easy to share and implement complex automations without starting from scratch.

## Available Blueprints

### 🎛️ MOES Wireless Remote Switch Controller  
**File:** `moes_controler/moes_double_rocker.yaml`

Comprehensive automation for MOES Wireless Remote Switch (Double Rocker) using ZHA events.

**Features:**
- Support for both left and right buttons
- Single and double press detection for each button
- Separate customizable actions for each press type
- ZHA integration with automatic event parsing
- Restart mode for immediate response to new button presses

### 🎛️ IKEA Five Button Remote for Lights
**File:** `ikea_five_button_remote/ikea_five_button_remote.yaml`

Advanced automation for IKEA TRADFRI 5-button remote controls with comprehensive light management capabilities.

**Features:**
- Center button toggle with optional forced brightness setting
- Smooth brightness control with up/down buttons (single press and hold)
- Customizable left/right button actions for short and long press
- ZHA integration with detailed event parameter documentation
- Supports single lights, light groups, or areas
- Transition effects for smooth light changes
- Restart mode for immediate response to button presses

### 🎛️ Tuya 2-Button Scene Switch
**File:** `tuya_2button_scene_switch/tuya_2button_scene_switch.yaml`

Simple and reliable automation for Tuya TS0042 2-button scene switches using ZHA events.

**Features:**
- Support for both left and right buttons
- Single and double press detection for each button
- Four separate customizable action configurations
- ZHA integration with endpoint-based button identification
- Compatible with Tuya TS0042 model scene switches
- No long press functionality (simplified design)
- Restart mode for immediate response to button presses

### 🔍 Low Battery Notification
**File:** `low_battery_notification/low_battery_notification.yaml`

Automatically monitors all battery-powered devices and sends notifications when they reach a user-defined low battery threshold.

**Features:**
- Configurable battery threshold (5-100%)
- Flexible scheduling (select specific weekdays)
- Advanced exclusion system supporting entities, devices, areas, and labels
- Supports both regular battery sensors and binary battery sensors
- Customizable notification actions

### 🔍 Unavailable Entity Detection & Notification
**File:** `unavailable_entities_notification/unavailable_entities_notification.yaml`

Monitors your Home Assistant entities and alerts you when devices become unavailable, helping maintain system health.

**Features:**
- Daily scanning for unavailable entities
- Weekday scheduling flexibility
- Comprehensive exclusion system (entities, devices, areas, labels)
- Automatically excludes disabled devices
- Customizable notification actions

### 🌡️ HVAC Health Monitor
**File:** `hvac_health_monitor/hvac_health_monitor.yaml`

Advanced HVAC system performance monitoring that detects when your heating or cooling isn't working effectively.

**Features:**
- Monitors thermostat heating and cooling effectiveness by measuring temperature changes
- Intelligent deadband detection with user warnings for optimal configuration
- Tracks consecutive failures using helper entities (counters)
- Configurable runtime monitoring and temperature tolerances
- Persistent notifications and detailed logbook entries
- Separate customizable actions for heating and cooling issues
- Designed for central HVAC systems (inspired by Nest Thermostat health checks)
- **Requirements:** 4 helper entities must be created manually:
  - `input_number.hvac_monitor_start_temp`
  - `input_datetime.hvac_monitor_start_time` 
  - `counter.hvac_cooling_failures`
  - `counter.hvac_heating_failures`

### 🔐 Xfinity Keypad and Alarmo Synchronization
**File:** `xfinity_keypad_and_alarmo_syncronization/xfinity_keypad_and_alarmo_syncronization.yaml`

Integrates a Xfinity xhk1-ue ZigBee Wireless Keypad from Comcast with the Alarmo HACS addon for seamless security system control.

**Features:**
- Full bidirectional synchronization between keypad and Alarmo
- Arm and disarm Alarmo using keypad with Alarmo passwords (not ZHA keypad password)
- Keypad display automatically reflects Alarmo state changes from Home Assistant
- Support for all Alarmo modes: Home, Away, Night, Vacation, and Custom Bypass
- MQTT communication for reliable command transmission
- Error handling for invalid codes and failed arming attempts
- Customizable additional actions for each alarm state change
- Parallel execution mode for responsive keypad interaction
- **Requirements:** 
  - Xfinity xhk1-ue ZigBee keypad paired with ZHA
  - Alarmo HACS integration installed and configured
  - MQTT broker configured

## Blueprint Features

All blueprints in this collection include:

- ✅ **Comprehensive Documentation** - Extensive inline comments explaining logic and configuration
- ✅ **Flexible Configuration** - Multiple input options to customize behavior
- ✅ **Production Ready** - Tested and designed for reliability
- ✅ **Exclusion Systems** - Advanced filtering capabilities where applicable
- ✅ **Error Handling** - Graceful handling of edge cases and failures

## Installation

1. Copy the desired blueprint YAML file to your Home Assistant `config/blueprints/automation/` directory
2. Restart Home Assistant or reload automations
3. Navigate to **Settings** → **Automations & Scenes** → **Blueprints**
4. Find your blueprint and click **Create Automation**
5. Configure the blueprint inputs according to your needs

## Contributing

Feel free to submit issues, feature requests, or pull requests to improve these blueprints!
