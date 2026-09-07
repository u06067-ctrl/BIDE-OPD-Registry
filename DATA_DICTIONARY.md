# Data dictionary

| Field | Type | Required | Notes |
|---|---|---:|---|
| MR Number | Text | Yes | Patient identifier; unique at patient level |
| Contact Number | Text | Yes | 7–15 digits after formatting characters are removed |
| Visit Date | ISO date | Yes | `YYYY-MM-DD` |
| Visit Type | Dropdown | Yes | Configurable in Settings |
| Next Appointment | ISO date | No | Cannot be earlier than Visit Date |
| Status | Dropdown | Yes | Configurable in Settings |
| Remarks | Text | No | Administrative free text |
| Created At | Timestamp | System | Exported automatically |
| Updated At | Timestamp | System | Exported automatically |

Default visit types: New Patient, Follow-up, Walk-in, Diabetes Clinic, Endocrine Clinic, Teleconsultation, Other.

Default statuses: Scheduled, Checked In, Completed, Cancelled, Missed, Rescheduled.
