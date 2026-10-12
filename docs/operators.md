# Operator Roles & RBAC Documentation

Mission Control supervisors oversee the delivery fleet under strict Role-Based Access Control (RBAC).

## Operator Roles & Permissions
*   **System Viewer:** Read-only access to telemetry logs, robot locations, and chamber environmental dashboards.
*   **Mission Controller:** Authorized to dispatch delivery routes, monitor live transit, and handle standard exceptions.
*   **Safety Officer:** Authorized to override routes, trigger emergency Safe Mode, and manage railway crossing overrides.
*   **System Administrator:** Full access to manage operator credentials, configure RBAC profiles, and perform system maintenance.

## Command Authorization Rule
All remote commands issued from Mission Control must include valid cryptographic tokens and verified role permissions before execution.
