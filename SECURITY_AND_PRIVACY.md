# Security and privacy notes

The app stores MR numbers and contact details, which are identifiable patient information.

Current protections in v1.0.0:

- Local app-private SQLite storage
- No INTERNET permission
- `android:allowBackup="false"`
- Cleartext network traffic disabled
- Staff PIN gate with salted SHA-256 verifier
- No analytics, advertisements, cloud SDKs, or third-party libraries
- Export only through Android's user-selected document location

Operational recommendations before real patient use:

- Use BIDE-owned managed Android devices with screen lock and device encryption enabled.
- Restrict who knows the app PIN; change it after staff turnover.
- Store exported Excel/CSV/JSON files only in approved encrypted locations.
- Establish retention, backup, access, and deletion rules approved by BIDE administration/IT.
- For multiple staff or devices, move to authenticated individual accounts and a central database with an audit trail.
- Consider database-at-rest encryption in a future centrally managed release if institutional policy requires it.
