# Task 2: Version-Controlled Change Log & RTM

## 1. Version-Controlled Change Log

| CR ID | Original Requirement Text | Changed Requirement Text | Reason for Change |
| :--- | :--- | :--- | :--- |
| **CR-01** | The robot shall enter Safe Mode when a critical battery or thermal condition is detected. | The robot shall enter Safe Mode within $3\text{ seconds}$ when chamber or battery temperature exceeds the critical threshold or battery capacity falls below the emergency level. | Adds precise timing bounds and specific operational triggers to make the requirement testable. |
| **CR-02** | The system shall support communication with multiple robots simultaneously. | The system shall support at least $20$ simultaneously connected robots. | Replaces vague scalability wording with a quantified pilot target. |
| **CR-03** | Only authenticated operators shall be permitted to issue robot commands. | The system shall require authenticated and role-authorised operators before accepting any robot command. | Explicitly mandates role-authorization alongside authentication for compliance. |

## 2. Multi-Layer Requirements Traceability Matrix (RTM)

| Req. ID | State / Transition | Operation Schema | Constraint ID | Test Case ID | Risk Level |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **FR-01** | IDLE → IDLE | `AuthenticateOperator` | C-01 | TC-01 | High |
| **FR-02** | IDLE → NAVIGATING | `ValidateAndDispatchCommand` | C-02 | TC-02 | Medium |
| **FR-03** | ANY → SAFE_MODE | `TriggerSafeMode` | C-03 | TC-03 | Critical |
| **FR-04** | MONITORING → CORRECTING | `ExecuteThermalCorrection` | C-04 | TC-04 | High |
| **FR-05** | NAVIGATING → AVOIDING | `SuspendNavigation` | C-05 | TC-05 | Medium |
| **HR-02** | NAVIGATING → CROSSING | `VerifyRailwayCrossing` | C-06 | TC-06 | Critical |
| **NFR-03** | ANY (Fleet-wide) | `BroadcastTelemetry` | C-07 | TC-07 | Medium |
| **HR-03** | LINKED → LINK_LOST | `ExecuteTimeoutFallback` | C-08 | TC-08 | High |
