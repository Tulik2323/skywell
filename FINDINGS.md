# FINDINGS

Status legend: Confirmed / Likely / Unverified

## Intake (user answers)
- Importer: Kadori (כדורי). VIN prefix: LMELB (WMI meaning not verified). Trim: Pro GT (= ET5 Pro GT in Israel, Likely)
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

## Phase B – The car itself

1. **Confirmed**: Skywell ET5 is imported to Israel by Kadori Group. Runs an Android-based head unit with 12.8" screen and Waze; no Android Auto/CarPlay. Sources: https://cars.walla.co.il/item/3467670 , https://www.automag.co.il/skywell-et5-suv-review-israel/ (snippets only, pages not fetched)
2. **Likely**: Pro GT is an ET5 trim (test drive title "Skywell ET5 Pro GT": https://www.youtube.com/watch?v=b6V26JlzTdE). ET5 = Skyworth EV6, same platform family as BE11 / Elaris / Imperium ET5 (https://en.wikipedia.org/wiki/Skyworth_EV6).
3. **Unverified**: Israeli units have a T-box/4G. Global marketing claims OTA and an app with remote lock/AC/battery, but no source ties it to Israeli units or names the app. Need: head-unit "About/SIM" screen, importer question, fuse-box/part-number check.
4. **Likely**: Head unit is Android; community ADB guide exists (https://github.com/xtcuser/SkywellADBOperations). Enabling ADB / sideloading modifies the head-unit software -> **excluded by the hard constraint**. Not pursued.
5. **Likely (OBD)**: Car Scanner (ELM327 app) added support for Elaris/Imperium/Skywell/Skyworth ET5/EV6/BE11 in v1.112.7 (https://www.carscanner.info/2024/06/ , snippet only, page blocked). Suggests read-only OBD data works with a cheap BLE/WiFi ELM327 dongle. Data set (SOC, temps) not confirmed.
6. **Unverified**: no public DBC or Home Assistant integration found for Skywell.
7. Blocked by sandbox proxy: xdaforums.com, carscanner.info, evm.co.il, play.google.com, apps.apple.com.
