# Home Assistant Blueprints Collection

This repository contains a collection of well-documented, production-ready blueprints for Home Assistant automation.

## About Home Assistant & Blueprints

[Home Assistant](https://www.home-assistant.io/) is an amazing home automation platform that gives you full control over all your smart devices and allows you to integrate different platforms seamlessly.

[Blueprints](https://www.home-assistant.io/docs/blueprint/) are reusable automation templates that make it easy to share and implement complex automations without starting from scratch.

## Available Blueprints

### 📱 Low Battery Notification
**File:** `low_battery_notification/low_battery_notification.yaml`

Automatically monitors all battery-powered devices and sends notifications when they reach a user-defined low battery threshold.

**Features:**
- Configurable battery threshold (5-100%)
- Flexible scheduling (select specific weekdays)
- Advanced exclusion system supporting entities, devices, areas, and labels
- Supports both regular battery sensors and binary battery sensors
- Customizable notification actions

### 🔌 MOES Wireless Remote Switch Controller  
**File:** `moes_controler/moes_double_rocker.yaml`

Comprehensive automation for MOES Wireless Remote Switch (Double Rocker) using ZHA events.

**Features:**
- Support for both left and right buttons
- Single and double press detection for each button
- Separate customizable actions for each press type
- ZHA integration with automatic event parsing
- Restart mode for immediate response to new button presses

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
