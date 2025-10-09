# Octopowerups AI Agent Instructions

## Project Overview
Octopowerups is a Home Assistant integration that helps users take advantage of free electricity periods from Octopus Energy. The system processes email notifications from Octopus Energy to create automated triggers and sensors.

## Core Components

### Email Processing (`octopowerup.yaml`)
- Uses Home Assistant's IMAP integration to process Octopus Energy emails
- Extracts dates and times from email subject lines and body
- Creates sensors for:
  - Email content (`sensor.OctopusPowerUp`)
  - Embedded links (`sensor.octopoweruplink`)
  - Power-up date (`sensor.OctoPowerUpDate`)
  - Start time (`sensor.OctoPowerUpStart`, `sensor.octopowerupstartts`)
  - End time (`sensor.OctoPowerUpEnd`, `sensor.octopowerupendts`)

### Time Management (`timers.yaml`)
- Tracks current time and free electricity period status
- Key sensors:
  - Current timestamp (`sensor.currentTS`)
  - Duration of power-up (`sensor.OctoPowerupDuration`)
  - Remaining time (`sensor.OctoPowerupTimeLeft`)

### Miscellaneous Features (`octomisc.yaml`)
- Automated Wheel of Fortune spinning for both gas and electricity accounts
- Uses numeric state triggers based on available spins

## Development Patterns

### Sensor State Templates
- Time calculations use timestamp conversions for reliable comparisons
- Date formats follow `YYYY-MM-DD` pattern
- Time formats include AM/PM markers: `HH:MM:SS[AM|PM]`

### Automation Triggers
Use value templates for conditional actions based on remaining time:
```yaml
value_template: "{{ (states('sensor.octopoweruptimeleft') | float(0)) > 0 }}"
```

### Testing Guidelines
1. Verify email parsing with different subject line formats
2. Check timestamp calculations around midnight and DST changes
3. Ensure proper handling of missing or malformed email data

## Integration Points
- IMAP email integration for notifications
- Home Assistant calendar integration for duration tracking
- Octopus Energy integration for Wheel of Fortune functionality

## Common Operations
1. Adding new sensors: Follow the template pattern in `octopowerup.yaml`
2. Time calculations: Convert to timestamps for comparisons
3. Error handling: Use default values with `| float(0)` or similar