# Robot Fleet Documentation

Each autonomous delivery robot in the SACDCS fleet is engineered for safety-critical medical transport.

## Robot Specifications
*   **Chamber Type:** Sealed active-conservation thermal chamber (supports heating/cooling).
*   **Power System:** Dual-tier power supply with primary lithium-ion battery pack and $4\text{-hour}$ emergency backup reserve.
*   **Sensors:** Internal temperature, relative humidity, vibration accelerometer, door reed-switch, power monitor, LiDAR, and obstacle avoidance cameras.
*   **Communication:** Low-bandwidth satellite/cellular link with built-in $30\text{-second}$ timeout fallback protocol.

## Operational States
1. **IDLE:** Docked at central warehouse awaiting dispatch.
2. **NAVIGATING:** En route to remote clinic along pre-planned route.
3. **AVOIDING_OBSTACLE:** Temporarily paused to clear physical blockages.
4. **DELIVERING:** Handing over medical packages at clinic destination.
5. **RETURNING:** Travelling back to warehouse after completion or abort.
6. **SAFE_MODE:** Secured emergency state triggered by critical thermal/battery faults.
