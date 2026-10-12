# Task 1: Master Requirements Baseline

## 1. Functional Requirements (FRs)
*   **FR-01:** The system shall authenticate operators and verify role-based permissions before accepting any remote command.
*   **FR-02:** The system shall validate command parameters against robot capability limits and operational states prior to dispatch.
*   **FR-03:** The system shall automatically transition the robot into Safe Mode upon detecting critical battery depletion or thermal thresholds.
*   **FR-04:** The onboard chamber controller shall activate active heating or cooling when internal temperature or humidity drifts outside pre-set medicine profile limits.
*   **FR-05:** The robot shall suspend navigation and enter obstacle avoidance mode immediately upon sensor detection of a physical blockage.
*   **FR-06:** The robot shall automatically resume navigation along its pre-planned route once obstacle sensors confirm the path is clear.
*   **FR-07:** The robot shall securely execute package handover at the designated clinic destination.
*   **FR-08:** The robot shall navigate back to the central warehouse upon completing a delivery or aborting due to low battery.
*   **FR-09:** The robot shall query the Automated Railway Level-Crossing Control System (ARLCCS) and verify barrier status before entering a level-crossing.
*   **FR-10:** The system shall log all operational events, telemetry data, and operator commands with time stamps over the low-bandwidth link.

## 2. Non-Functional Requirements (NFRs)
*   **NFR-01:** Command propagation and telemetry feedback over the low-bandwidth link shall tolerate a network delay of up to $5\text{ seconds}$ without triggering communication fault states.
*   **NFR-02:** All command transmissions between Mission Control and delivery robots shall be encrypted using AES-256 with role-based access control (RBAC).
*   **NFR-03:** Mission Control infrastructure shall support at least $20$ simultaneously connected delivery robots and active conservation chambers without performance degradation.
*   **NFR-04:** The onboard conservation chamber shall maintain internal temperature limits for up to $4\text{ hours}$ using emergency power reserves during primary power loss.
*   **NFR-05:** The static web portal shall present documentation for robots, operators, and project artifacts with page load times under $2\text{ seconds}$.

## 3. High-Risk Requirements
*   **HR-01:** The robot and conservation chamber shall enter Safe Mode within $3\text{ seconds}$ of detecting a critical battery or thermal anomaly.
*   **HR-02:** The robot shall not cross railway tracks unless the ARLCCS confirms barriers are fully closed and no train is approaching.
*   **HR-03:** If communication with Mission Control is lost for more than $30\text{ seconds}$, the robot shall execute an autonomous fallback protocol.
*   **HR-04:** The chamber door shall remain mechanically locked during transit and open only when stationary at verified delivery coordinates.

## 4. Master Requirements Matrix

| Req. ID | Requirement | Type | Priority | Verification Method |
| :--- | :--- | :--- | :--- | :--- |
| **FR-01** | Operator RBAC authentication | FR | High | Integration Testing |
| **FR-02** | Command parameter validation | FR | High | Boundary Testing |
| **FR-03** | Safe mode entry on critical conditions | FR | High | Fault Injection Testing |
| **FR-04** | Active thermal/humidity correction | FR | Medium | Chamber Testing |
| **FR-05** | Obstacle suspension handling | FR | High | Simulation Testing |
| **FR-06** | Navigation resumption post-clearance | FR | Medium | Simulation Testing |
| **FR-07** | Secure package delivery execution | FR | High | End-to-End Testing |
| **FR-08** | Return to warehouse routing | FR | Medium | Integration Testing |
| **FR-09** | ARLCCS level-crossing verification | Safety | Critical | Protocol Testing |
| **FR-10** | Telemetry and event logging | FR | Medium | Log Audit Testing |
| **NFR-01** | Low-bandwidth link delay handling ($5\text{s}$) | NFR | Medium | Network Latency Injection |
| **NFR-02** | AES-256 encryption & RBAC security | NFR | High | Penetration Testing |
| **NFR-03** | Support for $\ge 20$ concurrent robots | NFR | High | Load Testing |
| **NFR-04** | Emergency power backup ($4\text{h}$) | NFR | High | Endurance Testing |
| **NFR-05** | Web portal page load ($< 2\text{s}$) | NFR | Low | Performance Benchmarking |
| **HR-01** | Safe mode trigger within $3\text{ seconds}$ | Safety | Critical | Fault Injection & Timing |
| **HR-02** | Railway crossing interlock verification | Safety | Critical | Safety Assertion Testing |
| **HR-03** | Communication timeout fallback ($30\text{s}$) | Safety | High | Disruption Testing |
| **HR-04** | Chamber door mechanical interlock | Safety | Critical | Mechanical Testing |
