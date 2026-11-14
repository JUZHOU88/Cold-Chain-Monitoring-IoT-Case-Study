# Monitoring and failure-mode considerations

## Observed / reported capabilities

- Temperature reporting from a DS18B20.
- Door-status reporting.
- Buzzer and relay outputs.
- Dashboard-based status and a two-hour trend chart.
- An operating override mode.
- Access-point fallback in connectivity-limited circumstances.

## Issues a production design must address

| Scenario | Engineering consideration |
| --- | --- |
| Wi-Fi unavailable | Device should clearly indicate loss of cloud synchronisation; local sensing and alert behaviour must be tested independently |
| Sensor disconnected or returning invalid data | Detect the fault and avoid silently presenting an ordinary temperature |
| Door left open | Differentiate event detection from policy-based alarm thresholds |
| Power interruption | Determine restart state, missed data and backup-power requirements |
| Firebase authentication or rules failure | Treat cloud access as unavailable and avoid exposing credentials |
| Clock not synchronised | Identify unknown or unreliable timestamps |
| Relay malfunction | Do not assume an output command proves that downstream equipment responded |

These are **recommended validation scenarios**; they do not mean every behaviour has been implemented or tested in the prototype.

## Safety boundary

This portfolio material is **not** a clinical cold-chain operating procedure. Any real vaccine or medicine storage system needs appropriate calibrated sensors, independent alarms, safe electrical design, documented validation, and compliance with applicable policies and regulations.
