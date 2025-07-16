# HVAC Health Monitor - Troubleshooting Guide

## Why Your Blueprint Might Not Be Triggering

### 1. **Missing hvac_action Attribute**
- **Blueprint now triggers on**: `hvac_action` attribute changing to 'heating' or 'cooling'
- **Required**: Your thermostat MUST have an `hvac_action` attribute that reports actual system operation

**Check your thermostat's hvac_action:**
```yaml
# In Developer Tools > States, look for your thermostat
# Example entity: climate.your_thermostat
# Required attribute:
#   hvac_action: heating/cooling/idle  <- Blueprint monitors this
#
# Also check state for reference:
#   state: heat/cool/auto/off  <- Blueprint no longer uses this
```

### 2. **Missing Helper Entities**
The blueprint REQUIRES these 4 entities to exist:
- `input_number.hvac_monitor_start_temp`
- `input_datetime.hvac_monitor_start_time` 
- `counter.hvac_cooling_failures`
- `counter.hvac_heating_failures`

**Create them manually before using the blueprint!**

### 3. **Thermostat Entity Domain**
Blueprint selector limits to `domain: climate`. Ensure your thermostat is:
- A `climate.` entity (not `sensor.` or `switch.`)
- Available (not unavailable/unknown)
- Has the `hvac_action` attribute

### 4. **HVAC Action Transition Issues**
Blueprint only triggers on hvac_action CHANGES to heating/cooling:
- ❌ Won't trigger if already in heating/cooling mode
- ✅ Only triggers when hvac_action transitions FROM 'idle' TO 'heating'/'cooling'

## Testing Steps

### Step 1: Verify Helper Entities
```bash
# In Home Assistant, go to Developer Tools > States
# Search for these entities:
input_number.hvac_monitor_start_temp
input_datetime.hvac_monitor_start_time
counter.hvac_cooling_failures
counter.hvac_heating_failures
```

**If these entities don't exist, create them using one of these methods:**

#### Method 1: Add to configuration.yaml
```yaml
input_number:
  hvac_monitor_start_temp:
    name: "HVAC Monitor Start Temperature"
    min: -50
    max: 50
    step: 0.1
    unit_of_measurement: "°C"
    icon: mdi:thermometer

input_datetime:
  hvac_monitor_start_time:
    name: "HVAC Monitor Start Time"
    has_date: true
    has_time: true
    icon: mdi:clock-start

counter:
  hvac_cooling_failures:
    name: "HVAC Cooling Failures"
    step: 1
    icon: mdi:snowflake-alert
    
  hvac_heating_failures:
    name: "HVAC Heating Failures"
    step: 1
    icon: mdi:fire-alert
```

#### Method 2: Create via UI
1. Go to Settings > Devices & Services > Helpers > Create Helper
2. Create "Number" helper: `input_number.hvac_monitor_start_temp`
   - Name: "HVAC Monitor Start Temperature"
   - Min: -50, Max: 50, Step: 0.1
   - Unit: °C
3. Create "Date and/or time" helper: `input_datetime.hvac_monitor_start_time`
   - Name: "HVAC Monitor Start Time"
   - Enable both date and time
4. Create "Counter" helper: `counter.hvac_cooling_failures`
   - Name: "HVAC Cooling Failures"
5. Create "Counter" helper: `counter.hvac_heating_failures`
   - Name: "HVAC Heating Failures"

### Step 2: Check Thermostat HVAC Action
```bash
# In Developer Tools > States, find your thermostat
# CRITICAL: Verify the hvac_action attribute exists and reports:
# - 'idle' when system is off
# - 'heating' when heater is running
# - 'cooling' when AC is running
#
# If hvac_action is missing or reports different values, 
# this blueprint will NOT work with your thermostat!
```

### Step 3: Test the Trigger
```bash
# Method 1: Force hvac_action change by adjusting thermostat setpoint
# Method 2: Use the debug automation provided
# Method 3: Check automation traces in Settings > Automations > [Your Blueprint] > Traces
# Method 4: Watch for hvac_action changes in Developer Tools > Events (state_changed events)
```

### Step 4: Manual Test Template
Go to Developer Tools > Template and test:
```yaml
# Replace 'climate.your_thermostat' with your actual entity
{{ states('climate.your_thermostat') }}
{{ state_attr('climate.your_thermostat', 'hvac_action') }}
{{ state_attr('climate.your_thermostat', 'current_temperature') }}
{{ state_attr('climate.your_thermostat', 'temperature') }}
```

## Common Fixes

### ⚠️ IMPORTANT: Blueprint Now Uses hvac_action
The blueprint has been updated to monitor `hvac_action` attribute changes instead of `state` changes. The fixes below are for reference only - **most users should not need to modify the blueprint**.

### Fix 1: If hvac_action Reports Different Values
If your thermostat's hvac_action uses different values (rare), modify the blueprint trigger:
```yaml
trigger:
  - platform: state
    entity_id: !input thermostat
    attribute: hvac_action
    to:
      - 'heating'     # Standard value
      - 'cooling'     # Standard value  
      - 'heat'        # If your thermostat uses this instead
      - 'cool'        # If your thermostat uses this instead
```

### Fix 2: Thermostat Missing hvac_action (NOT RECOMMENDED)
If your thermostat doesn't have hvac_action, you could try using state instead (less reliable):
```yaml
trigger:
  - platform: state
    entity_id: !input thermostat
    to:
      - 'heat'
      - 'cool'
      - 'heating'
      - 'cooling'
```
**Note**: This approach is less reliable and may cause false triggers.

### Fix 3: Alternative Trigger for Unusual Thermostats
For thermostats with non-standard behavior:
```yaml
trigger:
  - platform: state
    entity_id: !input thermostat
    attribute: hvac_action
    from: 'idle'
    to:
      - 'heating'
      - 'cooling'
```

## Verification Commands

After setup, verify everything works:
1. Check automation traces: Settings > Automations > [Blueprint Name] > Traces
2. Watch logbook: Settings > System > Logs > Filter for "HVAC"
3. Monitor helper entities for value changes during HVAC operation
4. Test by adjusting thermostat setpoint to trigger hvac_action changes
5. Verify hvac_action changes from 'idle' to 'heating'/'cooling' in Developer Tools > States

## Compatibility Check

**Before using this blueprint, verify your thermostat compatibility:**

✅ **Compatible thermostats have:**
- `hvac_action` attribute that reports 'heating', 'cooling', 'idle'
- Reliable state changes when system starts/stops

❌ **Incompatible thermostats:**
- Missing `hvac_action` attribute
- `hvac_action` that doesn't change or reports unexpected values
- Thermostats that only report mode changes, not actual operation

**Quick compatibility test:**
1. Go to Developer Tools > States
2. Find your thermostat entity
3. Change setpoint to trigger heating/cooling
4. Watch if `hvac_action` changes from 'idle' to 'heating'/'cooling'

## Still Not Working?

1. **First**: Verify hvac_action compatibility (most common issue)
2. Enable debug logging for automations
3. Check Home Assistant logs for errors  
4. Verify thermostat integration is working properly
5. Test with a simple automation monitoring hvac_action changes first
6. Consider using a different HVAC monitoring approach if hvac_action is unreliable
