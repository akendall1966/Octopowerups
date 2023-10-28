# Octopowerups
Custom components and automations to take advantage of the free electricity period from Octopus energy in Home Assistant.
Octopowerup.yaml package uses the IMAP integration to trigger the update of some custom sensors using the dates and times extracted from the subject line and body of the email recived from the ensergy supplier. The main being a timestamp for the start and end of the period of free electricity.

timers.yaml package creates a sensro containing the current date-time as a timestamp, a sensor of the duration, and one containing the remaining duration effectively a countdown to the end of the free period.

Usage will depend on set up I trigger an automation on a time pattern and use a value template on conditional actions:

value_template: "{{ (states('sensor.octopoweruptimeleft') | float(0)) > 0 }}"

