# FINDINGS

Status legend: Confirmed / Likely / Unverified

## Intake (user answers)
- Importer: Kadori (כדורי). VIN prefix: LMELB (WMI meaning not verified). Trim: Pro GT (= ET5 Pro GT in Israel, Likely)
- Head-unit menu: no SIM/4G/connected-services entry (user checked: none). No phone-key. Importer (Kadori) has not answered.
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

## Phase C – Alternatives to the official cloud

1. **Likely**: With no SIM/connectivity menu and no phone key, the Israeli unit most likely has no active T-box. Not proven (importer silent).
2. **Unverified**: Any official/aftermarket T-box retrofit for ET5. Search found nothing. No source.
3. **Likely**: Read-only OBD is realistic (Car Scanner supports ET5/EV6, see phase B). Fits the 200 NIS budget (BLE/WiFi ELM327). Gateway filtering and exact PIDs: Unverified.
4. **Unverified / doubtful**: Starting A/C via OBD/CAN. No public source. Generic finding: modern cars gate actuation behind authenticated modules; aftermarket "smart start" kits are a risky wiring path. Would require writing CAN frames or wiring into the car -> conflicts with the no-modification constraint and warranty. Not recommended.
5. **Unverified**: Public DBC / Home Assistant work for Skywell: none found in English search. Russian/Turkish/Arabic forums (Drive2, 4PDA) and Hebrew Facebook groups not yet searched (blocked/no access).
6. **Not found in manuals (pages blocked)**: whether the ET5 has an in-car A/C timer / scheduled preheat. Needs a 1-minute check by the user in the climate screen and charge settings.
7. Blocked: skywell.ps, manualslib.com.

## Phase D – skipped by agreement
APK analysis not run: phase A indicates the app is a DELTA aftermarket-alarm client, so it cannot bind to a car without DELTA hardware. Can be revisited on request.

## Phase E – Route ranking (no code until user approves)
User answers: no A/C timer, no scheduled-charging option, no remote/key button. Budget 200 NIS.

| # | Route | Remote A/C chance | Cost | Risk | Effort |
|---|-------|------|------|------|--------|
| 1 | Ask Kadori in writing whether a T-box/app exists for Israeli units (and Skywell Israel social pages) | Low (Unverified) | 0 | None | Low |
| 2 | Read-only OBD: ELM327 BLE + Car Scanner (SOC, temps, charge state); optional ESP32 -> Home Assistant | None for A/C; gives monitoring | ~50-150 NIS | Very low (read-only; use a quality dongle) | Low-Med |
| 3 | DELTA alarm hardware retrofit (the app's real target) | Possible but Unverified for Israel | High, over budget | High: wiring, warranty, RU vendor | High |
| 4 | Write CAN frames / aftermarket remote-start wiring | Unverified | Medium | High: safety, warranty, violates constraint | High |
| 5 | Head-unit ADB/sideload | Not relevant to A/C | 0 | Violates constraint | - |

Honest conclusion: remote A/C start is unlikely within the constraints and budget. Realistic deliverable: monitoring (route 2) plus asking the importer (route 1).

## Phase E follow-up – Wiring / aftermarket route (user chose to investigate; budget "depends on the offer")
- **Likely**: Aftermarket remote-start vendors (StarLine, Pandora, iDatalink/Compustar) integrate via the car's CAN bus, but their support is per-vehicle-model. No source lists ET5/EV6 support. https://info.starlinesystems.co.uk/index.php/info/remote-start/ , https://pandorainfo.co.uk/pages/remote-start
- **Unverified**: A generic remote-start kit can start an EV's cabin climate. The only EV precedent found is a user thread on a Chevy Bolt, not this platform: https://www.chevybolt.org/threads/aftermarket-remote-start-for-preconditioning.53577/ . A low-quality blog snippet (alibaba lifetips) quotes $200-500 install; do not rely on it.
- **Unverified**: Skywell Israel / Kadori warranty position on aftermarket electronics. No source found. Must be asked in writing before any wiring.
- **Discarded**: A search summary claimed the ET5's "T-box connects to Skywell Connect". Unsupported: Skywell Connect is a DELTA alarm app (phase A).
- Next concrete step: ask StarLine/Pandora installers in Israel (and Kadori) whether any CAN module supports ET5 climate, with written price and warranty answer.
