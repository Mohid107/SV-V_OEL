# Task 5: Constraints, Formalisation & Violations

## 1. Formalised Constraints (Logical Notation)

1. **Operator Authorization:**
   $$\text{IssueCommand} \rightarrow (\text{Authenticated} \land \text{Authorized})$$
2. **Railway Crossing Safety:**
   $$\text{RobotEnteringCrossing} \rightarrow (\text{BarrierOpen} = \text{False} \land \text{TrainApproaching} = \text{False})$$
3. **Safe Mode Trigger:**
   $$\text{CriticalThermalOrBattery} \rightarrow \text{SafeModeActive} \le 3\text{s}$$
4. **Chamber Conservation Condition:**
   $$\text{ConservationActive} \rightarrow (\text{DoorClosed} = \text{True} \land \text{ProfileLoaded} = \text{True})$$
5. **Vibration Suspension:**
   $$\text{HighVibrationDetected} \rightarrow \text{RiskyActivitiesSuspended}$$
6. **Link Loss Fallback:**
   $$\text{LinkLossTimer} > 30\text{s} \rightarrow \text{FallbackProtocolTriggered}$$
7. **Batch Removal Safety:**
   $$\text{BatchRemovalAllowed} \rightarrow (\text{ChamberSafe} = \text{True} \land \text{ProtectionModeActive} = \text{False})$$
8. **Power Loss Emergency Handling:**
   $$\text{PrimaryPowerLoss} \land \neg\text{BackupPowerAvailable} \rightarrow (\text{IncidentRecorded} \land \text{SafeShutdown})$$

## 2. Realistic Violation Scenarios & Responses

| Constraint | Violation Scenario Variable Values | System Detection & Response |
| :--- | :--- | :--- |
| **C-01** | `IssueCommand = True`, `Authenticated = False`, `Authorized = False` | Detected by API gateway middleware. **Response:** Command rejected, security event logged. |
| **C-02** | `RobotEnteringCrossing = True`, `BarrierOpen = True`, `TrainApproaching = True` | Detected by ARLCCS and LiDAR. **Response:** Emergency brake applied, audible alarm sounded. |
| **C-03** | `CriticalThermalOrBattery = True`, `SafeModeActive = False` (after $4\text{s}$) | Detected by watchdog timer. **Response:** Hardware watchdog triggers hard power cutoff. |
| **C-04** | `ConservationActive = True`, `DoorClosed = False`, `ProfileLoaded = True` | Detected by door reed-switch. **Response:** Conservation actuators halted immediately. |
| **C-05** | `HighVibrationDetected = True`, `RiskyActivitiesSuspended = False` | Detected by accelerometer. **Response:** Robot speed reduced or movement suspended. |
| **C-06** | `LinkLossTimer = 35s`, `FallbackProtocolTriggered = False` | Detected by heartbeat timeout. **Response:** Robot enters autonomous fallback mode. |
| **C-07** | `BatchRemovalAllowed = True`, `ProtectionModeActive = True` | Detected by batch interlock controller. **Response:** Chamber latch remains locked. |
| **C-08** | `PrimaryPowerLoss = True`, `BackupPowerAvailable = False`, `SafeShutdown = False` | Detected by PMIC. **Response:** Non-volatile memory writes last-gasp incident log. |

## 3. Inter-System Constraints
*   **Robot-Chamber Constraint 1:** $\text{RobotState} = \text{DELIVERING} \rightarrow \text{ChamberDoorOpen} = \text{False}$
*   **Robot-Chamber Constraint 2:** $\text{ProtectionModeActive} = \text{True} \rightarrow (\text{RobotSpeed} = 0 \land \text{NavigationSuspended} = \text{True})$
*   **Sensor/Communication Failure Constraint:** $\text{EssentialSensorFailed} \lor \text{LinkLossDuration} > 30\text{s} \rightarrow \text{AutonomousSafeStateTriggered}$
