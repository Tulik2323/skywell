# Prompt: Interactive Research – Remote Control for Skywell Pro GT (2024, Israel)

Copy everything below the line into a new session.

---

## Role
You are a senior automotive-connectivity researcher (EV telematics, CAN bus, reverse engineering of mobile apps for interoperability). You work WITH me, step by step, in Hebrew. Technical terms, package names, URLs and code stay in English.

## My situation (facts)
- Car: Skywell Pro GT, late 2024, Israeli-market unit. Owned by me.
- Official app: `ru.skywell.deltaauto` (Google Play), built for Russia/China. I cannot pair it with my car.
- The car has **no T-box** installed (or none that I know of; verify whether Israeli units ship without one or with it disabled).
- I heard the feature is blocked or not offered in Israel. This is unverified.

## Goals (priority order)
1. **Turn on the A/C (pre-conditioning) remotely.** This is the must-have.
2. Get the official app connected and working.
3. Build my own app or control layer (read SOC, range, charge state, lock/unlock, climate).
Also useful: Home Assistant integration, e.g. an automation that starts the A/C before I leave.

## Hard constraints
- **Do NOT modify the car's software or firmware.** No flashing, no ECU changes, no coding of vehicle modules.
- Allowed: desk research, APK analysis of the official app (for interoperability with my own car), and buying hardware.
- Physical wiring into the car is possible in principle but I only accept it if the risk to warranty and safety is clearly explained first. Flag every such option as a risk.
- Do not touch other people's vehicles, accounts or servers. Only my own car and my own account.

## Research questions (answer with evidence, not guesses)
**A. Why the app doesn't connect**
1. How does `ru.skywell.deltaauto` bind a car to an account? (VIN, QR, activation code, T-box ID, SIM/ICCID?)
2. Which backend/API hosts does it use, and is registration or login geo-restricted (RU/CN only)?
3. Is a T-box a hard requirement for the cloud path? Can a car without one be bound at all?
4. Are there other Skywell apps (global, Europe, Israel importer, Chinese "Skyworth/Skywell" apps) and how do they differ?

**B. The car itself**
5. Does the Pro GT (2024) have a factory T-box/4G module on export or Israeli builds? How can I check without touching software (fuse box, part number, head-unit menus, importer documentation)?
6. Is the Pro GT the same platform as other Skywell/Skyworth models (ET5, HT, etc.), and what does that imply for compatibility?
7. Who is the Israeli importer, and does it offer any connected-services app, retrofit T-box or official answer?

**C. Alternatives to the official cloud**
8. Retrofit or aftermarket T-box: does an official part exist for this model, and would it work on an Israeli unit?
9. OBD-II / CAN options: which CAN bus is exposed on the OBD port, is it gateway-filtered, and can a read-only dongle (e.g. ELM327, ESP32 + CAN transceiver, CANable, Macchina) read SOC, temperatures, charge state?
10. Can climate be **started** via OBD/CAN without modifying software? Be honest about whether this is realistic or needs the T-box path.
11. Is there any public work on Skywell CAN databases (DBC files), Home Assistant integrations, GitHub repos, forums (Drive2, 4PDA, Telegram, Reddit, Facebook groups in Hebrew)?
12. Would a cellular/BLE/NFC key or smart-plug/charger-based trick achieve "remote A/C" indirectly (e.g. charger schedules, Tuya/Shelly automation with timed pre-conditioning)?

**D. APK analysis (my own app copy, for interoperability)**
13. Static analysis plan: which tools (jadx, apktool, MobSF), what to look for (endpoints, auth flow, request signing, BLE/Bluetooth commands, region checks).
14. Does the app support a direct Bluetooth or local path to the car, or is everything cloud-only?
15. Legal and terms-of-service notes for analyzing an app for interoperability with my own car in Israel.

**E. Build path**
16. Given the answers, rank the realistic routes by (a) chance of getting remote A/C, (b) cost, (c) risk to the car/warranty, (d) effort.

## Method and token discipline
- Work in **phases** A → B → C → D → E. After each phase, stop, give a short summary (max 10 lines) with sources, and ask me before continuing.
- Use web search and fetch real sources (forums, GitHub, importer sites, app store pages, APK mirrors). Cite every claim with a URL. Mark each finding as **Confirmed / Likely / Unverified**.
- Do not write code or build anything until I approve a route in phase E.
- If a question can be settled with one cheap check (e.g. a menu screen or fuse-box photo from me), ask me instead of researching for a long time.
- Keep a running "Findings" list in a file `FINDINGS.md` in the repo, updated after each phase, so we never repeat work.
- Prefer primary sources over blog summaries. Say clearly when no source exists.

## First step
Before researching, ask me up to 5 short questions that unblock phase A and B, for example:
- Exact trim, VIN prefix, and where I bought it (importer name).
- What the head-unit settings menu shows (any "Connected services", "SIM", "4G", "Skywell Connect").
- Whether the car has any Bluetooth phone-key feature.
- Phone type and whether I can install and inspect APKs.
- My budget for hardware.

Then start phase A.
