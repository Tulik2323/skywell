# FINDINGS

Status legend: Confirmed / Likely / Unverified

## Intake (user answers)
- Trim / VIN prefix / importer: not yet provided (user will write)
- Head-unit menu: no connected-services / SIM / 4G / phone-key that the user knows of
- Phone: Android, needs step-by-step guidance for APK
- Hardware budget: up to 200 NIS

## Phase A – Why the app doesn't connect

1. **Likely**: `ru.skywell.deltaauto` ("Skywell Connect", v1.0.0, Android 6+) is NOT a Skywell factory app. Developer is DELTA (DELTA-SISTEMY BEZOPASNOSTI, OOO), a Russian aftermarket car-alarm company. The Skywell name is a white-label/branding for their alarm-system app (also known as "DELTA Connect").
   - https://play.google.com/store/apps/details?id=ru.skywell.deltaauto
   - https://apps.apple.com/ua/app/skywell-connect/id6449029893
2. **Likely**: The app manages the DELTA security system installed in the car (guard/service mode, remote climate, door open, location, battery/range), plus a security-agreement balance. This means it pairs with DELTA alarm hardware (GSM/BT module), not with the car's own T-box. This is why it cannot bind to an Israeli car with no DELTA module.
   - Search snippets above; Russian installer page mentions DELTA custom alarm for Skywell ET5 with Bluetooth module: https://www.kibercar.com/services/skywell/et5/avtorskie-okhrannye-sistemy/
3. **Unverified**: exact binding mechanism (module ID / IMEI / activation code) and backend hosts. Needs APK analysis (phase D).
4. **Unverified**: geo-restriction of registration.
5. Other Skywell app: `ru.madbrains.deltaauto` ("DELTA Avto") also by the same ecosystem (Unverified relation).

## Blocked sources
play.google.com, apps.apple.com, globalcio.ru, delta.ru blocked by the sandbox egress proxy. Full store text and vendor pages need to be checked by the user or via mirrors (apkcombo/apkpure).

## Implication so far
The official app is very likely a dead end for a car without a DELTA module. Retrofitting DELTA alarm hardware is a possible (but wiring-invasive, Russian-market) path; flag as a risk.
