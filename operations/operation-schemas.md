# Task 4: Conservation Chamber Operation Schemas

## 1. Identified Operations (12 Items)
1. `AuthenticateOperator`
2. `PerformSelfCheck`
3. `LoadMedicineProfile`
4. `VerifyDoorClosure`
5. `InitiateConservation`
6. `ExecuteThermalCorrection`
7. `VerifySensorReadings`
8. `TriggerProtectionMode`
9. `StabilizeVibration`
10. `SwitchToEmergencyPower`
11. `RecordPowerFailure`
12. `VerifyBatchRemoval`

## 2. Core Operation Schemas

### Operation: `PerformSelfCheck`
*   **Description:** Runs diagnostic checks on all chamber sensors at power-on.
*   **Inputs:** Power-on signal.
*   **Outputs:** Diagnostic status report.
*   **Reads:** Sensor status registers.
*   **Changes:** Chamber operational readiness flag.
*   **Sends/Alerts:** Error alert to Mission Control if self-check fails.
*   **Assumes:** Chamber is powered on.
*   **Result:** Chamber enters monitoring state only if all essential sensors report OK.

### Operation: `LoadMedicineProfile`
*   **Description:** Loads temperature and humidity limits for a newly placed medicine batch.
*   **Inputs:** Batch ID, temperature limits, humidity limits.
*   **Outputs:** Profile confirmation ack.
*   **Reads:** Local configuration cache.
*   **Changes:** Active batch profile parameters.
*   **Sends/Alerts:** Profile loaded event logged.
*   **Assumes:** Batch placed inside chamber and door is closed.
*   **Result:** Limits stored in active memory for conservation monitoring.

### Operation: `InitiateConservation`
*   **Description:** Starts active temperature/humidity conservation for loaded medicines.
*   **Inputs:** Profile loaded confirmation, door closed status.
*   **Outputs:** Conservation active status.
*   **Reads:** Door sensor, profile parameters.
*   **Changes:** Conservation loop state (Active).
*   **Sends/Alerts:** Telemetry update sent to Mission Control.
*   **Assumes:** Door is closed AND profile is loaded AND self-check passed.
*   **Result:** Active cooling/heating regulators are enabled.

### Operation: `ExecuteThermalCorrection`
*   **Description:** Adjusts heating or cooling elements when temperature drifts out of range.
*   **Inputs:** Current temperature reading, target profile range.
*   **Outputs:** Control actuator signals (heater/cooler power level).
*   **Reads:** Thermal sensors.
*   **Changes:** Actuator states.
*   **Sends/Alerts:** Thermal correction event logged.
*   **Assumes:** Chamber is in conservation mode.
*   **Result:** Internal temperature returns toward target range.

### Operation: `TriggerProtectionMode`
*   **Description:** Secures medicine batch if thermal correction fails within recovery period.
*   **Inputs:** Timeout flag from thermal recovery timer.
*   **Outputs:** Protection mode status.
*   **Reads:** Recovery timer, current sensor values.
*   **Changes:** Chamber state to Protection Mode, light exposure reduced.
*   **Sends/Alerts:** High-priority alert sent to Mission Control operator.
*   **Assumes:** Thermal correction attempt exceeded recovery window.
*   **Result:** Reduced light exposure, operator alerted, risky activities suspended.

### Operation: `SwitchToEmergencyPower`
*   **Description:** Migrates chamber power draw to emergency battery reserves upon primary power loss.
*   **Inputs:** Primary power loss interrupt.
*   **Outputs:** Power source switch signal.
*   **Reads:** Battery backup charge level.
*   **Changes:** Power supply channel (Primary $\rightarrow$ Emergency).
*   **Sends/Alerts:** Power loss warning event logged.
*   **Assumes:** Emergency power backup is available.
*   **Result:** Chamber continues critical conservation without interruption.
