# Track M: Mobile AQA toolsets (Weeks 9–13)

**Depth:** Literacy (choose, set up with an agent, direct an agent). **Time:** ~2–3 h/week for 5 weeks.
**Out of scope:** building native apps (Swift/Kotlin).

## Goal
She knows the mobile testing landscape well enough to pick a toolset for a product, get an agent to set it up, run a small agent-built suite on an emulator in CI, and diagnose mobile-specific failures.

## M1: Mobile platform concepts

### What to learn
- [ ] App types: native, hybrid, web/PWA, cross-platform (React Native, Flutter) and what each means for automation
- [ ] Artifacts: APK / AAB (Android), IPA (iOS); debug vs release; signing and provisioning (concept only)
- [ ] Android vs iOS: OS versions, device and screen fragmentation
- [ ] **Mobile risk areas** for strategy: permissions, interruptions (calls, notifications), backgrounding, network changes / offline, gestures, deep links, push notifications, upgrades and data migration, battery and performance, accessibility, localization

### Resources (pick one primary)
- **A.** 📖 Android "Fundamentals of testing" — https://developer.android.com/training/testing/fundamentals
- **B.** 📖 Apple "Testing" overview in Xcode docs — https://developer.apple.com/documentation/xcode/testing
- **C.** 📖 Ministry of Testing mobile testing articles — https://www.ministryoftesting.com/articles
- 📖 Android accessibility testing — https://developer.android.com/guide/topics/ui/accessibility/testing

## M2: Devices and environments

### What to learn
- [ ] Emulators (Android AVD) and simulators (iOS): what they reproduce and what they don't
- [ ] Real devices vs emulators: trade-offs
- [ ] `adb`: list devices, install an app, `logcat`, screenshot, screen recording
- [ ] `xcrun simctl`: boot, install, launch, screenshot, record
- [ ] Reading a crash log / `logcat` for the first relevant error
- [ ] Device clouds: what they offer, cost drivers, CI integration (use only approved vendors)
- [ ] Why mobile CI is slower and flakier (emulator boot, macOS runners for iOS)

### Resources
- **Android emulator:** 📖 https://developer.android.com/studio/run/emulator
- **adb:** 📖 https://developer.android.com/tools/adb
- **Logcat:** 📖 https://developer.android.com/tools/logcat
- **iOS simulator:** 📖 https://developer.apple.com/documentation/xcode/running-your-app-in-simulator-or-on-a-device (and run `xcrun simctl help`)
- **Android in CI (GitHub Actions emulator action):** 📖 https://github.com/ReactiveCircus/android-emulator-runner
- **Device clouds (free docs/trials, if approved):** 📖 BrowserStack App Automate docs — https://www.browserstack.com/docs/app-automate ; Sauce Labs docs — https://docs.saucelabs.com

> If she has no Mac, start with Android. iOS simulators need macOS.

## M3: Automation frameworks (know the options, direct the agent)

### The landscape

| Tool | Notes | Docs |
|---|---|---|
| **Appium** | Cross-platform standard; WebDriver-based; flexible, slower, can be flaky | https://appium.io/docs/en/latest/ |
| **Maestro** | YAML flows, simple setup, quick for smoke tests, agent-friendly | https://docs.maestro.dev |
| **Espresso** (Android) | Native, fast, stable; needs app project access | https://developer.android.com/training/testing/espresso |
| **XCUITest** (iOS) | Native, fast, stable; needs Xcode project | https://developer.apple.com/documentation/xctest/user_interface_tests |
| **Detox** | React Native gray-box | https://wix.github.io/Detox/ |
| **Flutter integration tests** | For Flutter apps | https://docs.flutter.dev/testing/integration-tests |
| **Playwright mobile emulation** | Responsive web only; not real mobile | https://playwright.dev/python/docs/emulation |

### What to learn
- [ ] Architecture of Appium (client → server → driver → device) at diagram level
- [ ] Locators: accessibility IDs vs XPath; why developer cooperation on IDs matters
- [ ] Flows vs code-based tests (Maestro vs Appium trade-offs)
- [ ] Native frameworks: faster and more stable, but tied to the app and platform
- [ ] **Selection criteria:** platforms, app type, team skills, CI constraints, flake tolerance, maintenance cost
- [ ] Mobile MCPs for agent-driven exploration, and their limits (slow, screenshot-driven, non-deterministic)

### Resources (pick one framework to go hands-on; skim the rest)
- **Hands-on A (recommended for beginners):** Maestro — "Getting started" and "Android/iOS" quickstarts — https://docs.maestro.dev
- **Hands-on B:** Appium — introduction and quickstart — https://appium.io/docs/en/latest/intro/ and https://appium.io/docs/en/latest/quickstart/
- 📚 Test Automation University, Appium / mobile courses (free) — https://testautomationu.applitools.com
- **Mobile MCPs (only if allowlisted):** mobile-mcp — https://github.com/mobile-next/mobile-mcp ; Appium MCP — https://github.com/appium/appium-mcp

## M4: Verification layer and diagnosis on mobile

### What to learn
- [ ] Apply Phase 2 ideas: planted bugs in the app, repeat runs to detect flakes, no weakened assertions
- [ ] Artifacts the agent can read: screen recordings, `logcat`, screenshots, Appium logs
- [ ] Classifying mobile failures: app bug, test bug, emulator/device issue, OS-version issue, network issue, permission/interruption
- [ ] Why real devices catch things emulators don't

### Practice
- Run the suite 10–20 times on an emulator; record failures and classify them.
- Seeded failures (mentor): emulator won't boot, permission dialog blocks the flow, stale locator, a real bug on one OS version.

## Practical project: Mobile smoke suite

**Demo apps (pick one):**
- **Android + iOS native demo (WebdriverIO):** https://github.com/webdriverio/native-demo-app
- **Wikipedia Android:** https://github.com/wikimedia/apps-android-wikipedia
- **Wikipedia iOS:** https://github.com/wikimedia/wikipedia-ios
- **Sample from the chosen framework docs** (Maestro and Appium both provide examples)

**Steps**
1. She writes 5–8 smoke cases in plain language (login/launch, search, navigation, permission prompt, offline state, deep link).
2. With the agent, set up the emulator/simulator and the chosen framework. The agent installs; she asks it to explain each step.
3. The agent builds the suite from her specs. She does not edit code by hand.
4. Run it from the terminal with one documented command.
5. Add a CI job (emulator on GitHub Actions or an approved device cloud).
6. Plant 2–3 bugs in the app (or a modified build) and check the suite catches them.
7. Write a one-page **framework recommendation** for a hypothetical product (native iOS + Android, or React Native) with reasons.

## Agent exercises
- "Compare Appium, Maestro and Espresso for this product. Ask me questions that decide the choice."
- "Write a Maestro flow for these steps. List what could make it flaky."
- "Here is `adb logcat` output from a crash. What is the first relevant error and what are three hypotheses?"
- "How would you test offline behavior and an incoming call interruption?"

## Mentor drills
- **Framework pick:** a product description → she picks a framework, defends it, and names the risks.
- **Seeded failure:** classify an emulator boot failure vs a stale locator vs a real bug using logs or a recording only.
- **Interruptions:** design tests for permissions, backgrounding and network loss; mentor challenges the priorities.

## Done when
- [ ] She can explain to a stakeholder which mobile framework fits their product, and why
- [ ] An agent-built suite runs from the terminal **and** in CI
- [ ] She classified a seeded mobile failure with evidence from logs/recordings
- [ ] The suite caught at least one planted bug, and she documented what it missed
- [ ] The recommendation memo is written

## Pitfalls
- Spending weeks on setup. Let the agent do the SDK and emulator work; ask for help after 30 minutes stuck.
- Assuming an emulator equals a device. Note what you can't verify without real devices.
- Big mobile suites. Keep it smoke-level; mobile tests are slower and flakier.
- XPath everywhere. Ask for accessibility IDs and note them as an app improvement.
- Picking a tool by trend. Start from the product and team constraints.
