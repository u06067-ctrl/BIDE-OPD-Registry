# BIDE Karachi OPD Registry — Android

Version 1.0.0

An offline-first Android application for BIDE Karachi OPD administrative staff to register and manage patient visits and appointments by MR number.

## Core fields

- MR number
- Contact number
- Visit date
- Visit type (configurable dropdown)
- Next appointment date
- Status (configurable dropdown)
- Remarks

## Main capabilities

- MR-based patient database with multiple visit/appointment records per patient
- Automatic contact lookup when a known MR number is entered
- Dashboard: unique patients, total visits, today's visits, appointments due in 7 days, scheduled/completed/missed counts
- Search by MR number, contact number, or remarks
- Filters by visit type, status, date range, and upcoming appointments
- Sort by newest/oldest visit, next appointment, or MR number
- Edit and delete visits
- Quick “Add follow-up” from an existing visit
- Configurable Visit Type and Status dropdown values
- True Excel `.xlsx` export with **OPD Records** and **Summary** worksheets
- Export scopes: all records, current filter, custom date/status/type, next 30 days, or today's visits
- CSV export
- Full JSON backup/restore
- Local 4–8 digit staff PIN
- No INTERNET permission; Android cloud backup disabled

## Workflow inspiration

The workflow follows established EMR/HMIS ideas used by OpenMRS and Bahmni: patient registration/search, appointment status management, visit types, and offline-friendly point-of-care/registration workflows. This project is intentionally much smaller and focuses only on OPD administrative registration and appointments.

## Data model

The app uses two local SQLite tables:

1. `patients`: one row per MR number and current contact number
2. `visits`: multiple dated visit/appointment records linked to the patient

Excel export flattens this into the requested columns for reporting.

## Build

Requirements:

- Android Studio (current stable recommended)
- Android SDK Platform 35
- JDK 17 or newer supported by the selected Android Gradle Plugin

Open this folder as an Android Studio project and allow Gradle to sync. Build > Build APK(s) creates a debug APK.

## Release signing

Do **not** publish a hospital app using a shared example/private key from a third party. BIDE should own the production signing key.

The project already reads release signing credentials from environment variables:

- `BIDE_KEYSTORE`
- `BIDE_STORE_PASSWORD`
- `BIDE_KEY_ALIAS`
- `BIDE_KEY_PASSWORD`

See `BUILD_AND_SIGN.md` for exact commands.

## Play Protect / Play distribution

A cryptographic APK signature is required, but it does not by itself guarantee that Google Play Protect will never show a warning. For the strongest distribution trust, use BIDE's own developer account and Google Play App Signing (for example, Internal/Closed testing for a staff-only app), keep the target SDK current, request only necessary permissions, and preserve the same signing identity for updates.

This application intentionally requests **zero runtime permissions** and does not request Internet access.

## Important deployment note

Version 1.0.0 is a **single-device local registry**. If several reception desks need to enter records at the same time, deploy a central authenticated backend and staff-specific accounts/audit logs rather than using independent copies of the local database.
