# UI-GPS

A React Native app built with [Expo](https://expo.dev) (SDK 57) and [Expo Router](https://docs.expo.dev/router/introduction).
Bootstrapped with [`create-expo-app`](https://www.npmjs.com/package/create-expo-app).

## Prerequisites

| Tool | Version | Notes |
| --- | --- | --- |
| [Node.js](https://nodejs.org) | 20 LTS or newer | `node -v` to check. Expo SDK 57 / RN 0.86 need Node ≥ 20. |
| npm | 10+ (ships with Node 20) | This repo uses npm and commits `package-lock.json`. |
| [Git](https://git-scm.com) | any recent | |
| [Expo Go](https://expo.dev/go) app | latest | Install on your phone to run without a native build. |
| Android Studio | optional | Only needed for the Android emulator. |
| Xcode | optional, macOS only | Only needed for the iOS simulator. |

No global `expo-cli` install is required — this project uses the local CLI via `npx expo`.

## Setup (cloning from GitHub)

```bash
# 1. Clone
git clone <your-repo-url> ui-gps
cd ui-gps

# 2. Install dependencies (exact versions from package-lock.json)
npm ci

# 3. Verify the toolchain is healthy
npx expo-doctor

# 4. Start the dev server
npx expo start
```

`node_modules/` is **not** committed — it is listed in `.gitignore` and recreated by step 2.
Use `npm ci` for a clean, lockfile-exact install; use `npm install` only when you intend to add or change dependencies (it may update `package-lock.json`).

### Running the app

With the dev server running (`npx expo start`), press one of:

| Key | Target | Also runnable as |
| --- | --- | --- |
| `a` | Android emulator / connected device | `npm run android` |
| `i` | iOS simulator (macOS only) | `npm run ios` |
| `w` | Web browser (`http://localhost:8081`) | `npm run web` |
| scan QR | Physical device via Expo Go (same Wi‑Fi) | — |

If your phone can't reach the dev server over the LAN, use a tunnel:

```bash
npx expo start --tunnel
```

### Available scripts

| Script | Purpose |
| --- | --- |
| `npm run start` | Start the Expo dev server |
| `npm run android` | Start and open on Android |
| `npm run ios` | Start and open on iOS |
| `npm run web` | Start and open in the browser |
| `npm run lint` | Run `expo lint` |
| `npm run reset-project` | Move the starter code aside and scaffold a blank `src/app` |

## Project structure

```
src/
  app/            file-based routes (index.tsx = Home, explore.tsx, _layout.tsx = tab layout)
  components/     shared UI (themed text/view, tab bar, animated icon, ...)
  constants/      theme.ts — colors, spacing, fonts
  hooks/          color-scheme / theme hooks
assets/           icons, splash, images
```

Routing uses [file-based routing](https://docs.expo.dev/router/introduction): add a file under `src/app/` to add a screen.

## Troubleshooting

**`npm ci` / `npm install` fails with `ECONNRESET` or is extremely slow**
Network/registry hiccup. Retry, and check your proxy/registry config:

```bash
npm config get registry   # expect https://registry.npmjs.org/
npm config get proxy      # expect null unless you are behind a corporate proxy
npm ping
```

**`EPERM: operation not permitted, rmdir ...\node_modules\expo\...` on Windows**
A process is locking files in `node_modules`. Stop the Metro/Expo dev server, close editors/terminals using the folder, pause antivirus real-time scanning for the project folder, then:

```powershell
Remove-Item -Recurse -Force node_modules
npm ci
```

**Metro serves stale code or a bundling error after changing deps**

```bash
npx expo start -c   # clears the Metro cache
```

**`expo-doctor` reports issues**
Follow its output; `npx expo install --check` fixes dependency version mismatches against the installed SDK.

## Learn more

- [Expo documentation](https://docs.expo.dev/) and [guides](https://docs.expo.dev/guides)
- [Expo Router](https://docs.expo.dev/router/introduction)
- [SDK 57 API reference](https://docs.expo.dev/versions/v57.0.0/)
