# Architecture and data flow

## Prototype components

1. **Microcontroller:** ESP8266 during earlier development, with ESP32 used later.
2. **Temperature input:** DS18B20 digital temperature sensor.
3. **Door input:** Sensor signaling the storage door's state.
4. **Local outputs:** Relay and buzzer for configured device responses.
5. **Cloud state:** Firebase Realtime Database for synchronising readings and control/state fields.
6. **User interface:** Browser-based dashboard showing current state and a two-hour temperature trend.
7. **Network support:** NTP synchronisation when online and local access-point fallback.

## Conceptual data flow

```text
Temperature + door signals
    ↓
Embedded firmware (sampling, state, alarms)
    ├──→ Local buzzer/relay response
    ├──→ Firebase Realtime Database ←── Web dashboard
    └──→ Connectivity / AP fallback
```

This is a **logical diagram**, not a wiring guide or assertion about the precise timing, retry, authentication or payload schema of the implementation.

## Engineering considerations

**Cloud communication:** A remote dashboard adds visibility but must not be considered a safety-critical control without independent validation.

**Local actions:** Local alarm paths can reduce reliance on cloud connectivity, subject to adequate power and firmware behaviour.

**Timekeeping:** Time obtained from NTP depends on network availability. Clock reset and missing timestamp scenarios should be accounted for in analysis.

**Security:** Production deployments should use narrowly scoped access rules, secure device provisioning and credential rotation. No credentials or endpoint identifiers are included in this public case study.

**Persistence:** The availability of a two-hour chart is not proof that data is retained or recoverable for longer periods.

## Scope note

The described modules come from development milestones for a functioning prototype. No quantitative accuracy, latency, availability or endurance benchmarks are claimed.
