# Build and production-sign the BIDE OPD Registry

## 1. Create a BIDE-owned signing key (one time only)

Run this on a trusted BIDE-controlled computer and keep both the keystore and passwords securely backed up:

```bash
keytool -genkeypair -v \
  -keystore bide-opd-release.jks \
  -alias bide-opd \
  -keyalg RSA -keysize 4096 \
  -validity 10000
```

Do not place the production keystore or passwords in source control, chat, email, or a public shared folder.

## 2. Configure environment variables

Linux/macOS example:

```bash
export BIDE_KEYSTORE=/secure/path/bide-opd-release.jks
export BIDE_STORE_PASSWORD='your-store-password'
export BIDE_KEY_ALIAS='bide-opd'
export BIDE_KEY_PASSWORD='your-key-password'
```

Windows PowerShell example:

```powershell
$env:BIDE_KEYSTORE='C:\secure\bide-opd-release.jks'
$env:BIDE_STORE_PASSWORD='your-store-password'
$env:BIDE_KEY_ALIAS='bide-opd'
$env:BIDE_KEY_PASSWORD='your-key-password'
```

## 3. Build the signed release APK

From Android Studio use **Build > Generate Signed Bundle / APK**, or from a terminal with a Gradle wrapper installed:

```bash
./gradlew clean assembleRelease
```

Output is normally under:

`app/build/outputs/apk/release/`

## 4. Verify the signature

Using Android Build Tools:

```bash
apksigner verify --verbose --print-certs app-release.apk
```

Record the SHA-256 certificate digest and keep it in BIDE's deployment documentation.

## 5. Recommended staff distribution

For the best Play Protect reputation and update path, publish through a BIDE-controlled Google Play Console account and use Google Play App Signing, preferably Internal or Closed testing if the application is staff-only.

Sideloaded APKs may still generate device-specific warnings even when correctly signed. Do not attempt to bypass or disable Play Protect.

## 6. 2026 Android developer verification

The application package name is `pk.org.bide.opdregistry`. If BIDE distributes the app through Google Play, register/verify this package under the BIDE-controlled developer identity and keep the production signing identity consistent. Google has announced Android developer-verification requirements rolling out in 2026; package registration and verified developer ownership are separate from merely signing an APK.

## GitHub Actions APK build
A workflow is included at `.github/workflows/build-apk.yml`. After pushing the project to a GitHub repository, run **Actions > Build Android APK > Run workflow**. The workflow builds an installable debug-signed APK and uploads it as the `BIDE-OPD-Registry-APK` artifact.

For production deployment, replace debug signing with a BIDE-controlled release keystore and keep the keystore/private passwords in GitHub Secrets. Do not publish the private signing key in the repository.
