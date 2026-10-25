# Source of truth

Checked on 2026-10-25.

## Official sources

- TownPass Flutter host: https://github.com/taipei-doit/TownPass
- Development guideline: https://tpe-guideline.web.app/en/docs/
- Design guideline: https://tpe-guideline.web.app/en/design/
- Figma UI kit, page `1:2`: https://www.figma.com/design/yCpXgoSE0rIhpB7SewpTp3/城市通-Town-Pass-Open-Source-Gov-Mobile-App-UI-kit-and-design-system--Community-?node-id=1-2
- README example, ParkFlow: https://github.com/taipei-doit/townpass2024-parking
- README example, RideFlow: https://github.com/taipei-doit/townpass2025-RideFlow

## Verified facts

The official guideline specifies Node.js 18+, Vue 3 Composition API, Vue Router, Pinia, Tailwind CSS, `v-calendar`, Headless UI Dialog, `pnpm install`, `pnpm dev`, and a default local URL of `http://localhost:5173`.

The inspected official Flutter repo checkout uses `flutter_inappwebview ^6.1.5`. Re-check `pubspec.yaml` instead of assuming this version remains current. Inspect these files when refreshing the contract:

- `lib/util/tp_web_view.dart`
- `lib/util/web_message_handler/tp_web_message_listener.dart`
- `lib/util/web_message_handler/tp_web_message_handler.dart`
- `lib/util/web_message_handler/tp_web_message_reply.dart`
- `lib/util/tp_colors.dart`
- `lib/util/tp_text_styles.dart`
- `pubspec.yaml`

The host registers `flutterObject` with `addWebMessageListener`. Web messages and replies are stringified JSON objects with `name` and `data` keys. The verified method names are `userinfo`, `launch_map`, `phone_call`, `1999agree`, `location`, `deviceinfo`, `open_link`, `notify`, and `qr_code_scan`.

The Figma file has no local variable collections, local text styles, or local paint styles. Published values are represented as canvas frames and text. Re-read these nodes when the file may have changed:

- Page: `1:2`
- Typography: `3:15`
- Main colors: `3:141`
- Semantic colors: `3:390`
- Buttons: `3:4828`
- Text fields: `3:5032` and component set `3:5149`
- Top navigation: `3:5071`

## Conflict handling

Use Figma for web visuals and the Flutter repo for host behavior. Do not silently merge contradictions.

Known example: Figma labels `font-Caption-regular` as 12/18 with weight 400, while the inspected Flutter `TPTextStyles.caption` uses weight 600. A WebView implementation follows Figma unless the user explicitly chooses native-code parity.

The Figma canvas includes misspelled or inconsistent names, including `Font-Familiy`, `text-derection-color-Gray/400`, and two Secondary 900/950 rows whose layer names mention Primary. Preserve the verified visual value while normalizing the project-side token name; document the mapping.

## Refresh procedure

1. Inspect the local repo first. If absent, read or clone the official public repo.
2. Read the guideline pages for project setup, prerequisites, project structure, two-way connection, web connection, method contracts, and accessibility.
3. When Figma values need to be refreshed, use the connected Figma tool to inspect the exact nodes above. Record name, displayed value, node ID, and inspection date. If the tool is unavailable, keep the verified snapshot and mark unknown values instead of guessing.
4. Compare Figma against `tp_colors.dart` and `tp_text_styles.dart`. Report mismatches instead of picking a third value.
