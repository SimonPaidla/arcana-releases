<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/logo.svg">
    <img src="assets/logo-light.svg" alt="Arcana" width="200">
  </picture>
</p>

# Arcana releases

Installers for **Arcana**, a desktop app for Windows 11 that ranks
pre-renewal cards on the uaRO private server by what they are worth and how
long they take to farm. The source code is kept elsewhere; this repository
holds the builds and nothing else.

**[Download the latest version](https://github.com/SimonPaidla/arcana-releases/releases/latest)**
— `Arcana-Setup-<version>.exe`, Windows 11 x64.

Once installed, Arcana keeps itself up to date from here. There is nothing
to download a second time.

## Install

| | |
|---|---|
| 1 | Download `Arcana-Setup-<version>.exe` from the [latest release](https://github.com/SimonPaidla/arcana-releases/releases/latest). |
| 2 | Run it. It installs for your Windows user — no wizard, no administrator prompt — and opens. |
| 3 | If Windows says *Windows protected your PC*: the installer is not code-signed. *More info* → *Run anyway*. This happens once. |

**What you need:** Windows 11 x64, Chrome or Edge (the crawl drives a local
browser), and a uaRO account — the control panel only shows the market to
someone signed in.

## What it does

**Ranks cards.** Price, farm spot, hours per card, zeny per hour, and a
score weighing value against hit points against spawn count. Hovering a
price opens the individual offers behind it — vendor, shop, coordinates.

**Judges prices against their own past.** Every crawl is kept, so a card
has a usual level and today's price can be measured against it.

**Advises on buying.** A short list of what is worth buying now, each
finding carrying its own confidence: what supports it, and what is still
missing.

**Shares crawls.** Several people's crawls live in
[arcana-snapshots](https://github.com/SimonPaidla/arcana-snapshots). A new
installation reads them at startup and has a ranking with history in it
before it has ever crawled anything.

**Calculates damage.** A pre-renewal damage calculator is built in, and its
DPS feeds the yield columns.

## Updates

Arcana asks this repository for a newer version every time it starts.

| What it finds | What happens |
|---|---|
| nothing newer | the app opens as always |
| a newer version | the start screen shows *Update 1.2.0 · 34 %*; when the download is done the app installs it silently and opens again as the new version |
| — and you press **Later** | the app opens at once; the update installs when you close it |
| no connection | the app opens as always and tries again next time |

Only the parts of the installer that changed are downloaded — usually a few
megabytes rather than the full 82 MB. The version you are running stands
beside the name at the top of the window, and under *Settings → Arcana*,
together with *Check for updates*.

Each download is checked against the SHA-512 in the release's
`latest.yml`. The installers are not code-signed, which is why Windows
warns before the first installation and never afterwards.

## Your data

Prices, crawls, settings and the sign-in live in
`%APPDATA%\uaro-card-crawler`, apart from the program. Installing, updating
and uninstalling never touch them.

To remove Arcana: *Settings → Apps → Installed apps → Arcana → Uninstall*.
The data folder stays; delete it by hand if you want it gone too.

## What a release contains

| File | What it is for |
|---|---|
| `Arcana-Setup-<version>.exe` | the installer — the only file you download yourself |
| `Arcana-Setup-<version>.exe.blockmap` | the installer's block list; the next update is computed against it |
| `latest.yml` | the version, file name and SHA-512 the app checks against |

## For the maintainer

Releases are uploaded here as **drafts** by `npm run release` in the source
repository, and reach the installations only when they are published by
hand. Three rules follow from every installation asking this address and
no other:

- **This repository is never renamed, deleted or made private.** A name
  given up can be registered by someone else, and every installation would
  then install whatever they publish.
- **No published release is ever removed.** The next differential download
  needs its `.blockmap`; without it every update is the full installer.
- **The version only goes up.** An installation never installs a lower
  one, so a mistake is corrected by a new release, not by withdrawing one.

Nobody else has write access here. Whoever can publish a release decides
what every installation runs.
