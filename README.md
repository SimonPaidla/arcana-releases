<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/logo.svg">
    <img src="assets/logo-light.svg" alt="Arcana" width="200">
  </picture>
</p>

# Arcana releases

Installers for two Windows apps around the vendor market of a Ragnarok
Online server. The source code is kept elsewhere; this repository holds
the builds and nothing else.

| App | What it does | Releases |
|---|---|---|
| **Arcana** | follows the market of cards and items, ranks cards, items and monsters by what they are worth and bring, and says what is worth buying now | `v<version>`, the release marked **Latest** |
| **Arcana Crawler** | collects the market every full hour and shares it with every Arcana | `crawler-v<version>`, always a **pre-release** |

**[Download Arcana](https://github.com/SimonPaidla/arcana-releases/releases/latest)**
(`Arcana-Setup-<version>.exe`, Windows 11 x64). Arcana Crawler is the
newest `crawler-v…` pre-release on the
[releases page](https://github.com/SimonPaidla/arcana-releases/releases)
(`Arcana-Crawler-Setup-<version>.exe`). You only need it if you want to
contribute to the shared market.

Once installed, both apps keep themselves up to date from here. There is
nothing to download a second time.

## Install Arcana

| | |
|---|---|
| 1 | Download `Arcana-Setup-<version>.exe` from the [latest release](https://github.com/SimonPaidla/arcana-releases/releases/latest). |
| 2 | Run it. It installs for your Windows user — no wizard, no administrator prompt — and opens. |
| 3 | If Windows says *Windows protected your PC*: the installer is not code-signed. *More info* → *Run anyway*. This happens once. |

**What you need:** Windows 11 x64. Arcana reads the market from a shared
store and needs no account.

## What Arcana does

**Types of goods.** One type at a time — cards, weapons, armor, healing,
usable items, Etc, pet eggs, pet armor and Cash Shop rewards — across the
market, the ranking, the economy and the buying advice. A type without
data is greyed out.

**Market.** What moved in the last hour, day, week or month, and one good
in full:
- its price now, its **fair value** (what it sells for at today's prices), and a rating of the price against the month;
- a price chart over 24 hours, 7 or 30 days or everything, with the confirmed sales in it;
- what to ask when you sell;
- equipment with its variants — refine and cards — and what their parts are worth; goods that stack per unit, with recipes, NPC prices and the monsters that drop them.

**Ranking.** Every card with its price, fair value, rating, sales, farm
spot, hours per card and zeny per hour, and a score weighing value
against hit points, spawn count and drop rate; every item of another type
by the zeny traded; and every monster by what all its drops bring an
hour. Hovering a price opens the individual offers behind it — vendor,
shop, coordinates. It can be saved as Excel or CSV.

**Economy.** The chosen type's market as a whole: merchants online, a
price index that shows whether goods are getting dearer or cheaper, the
zeny traded and its share of all types, when prices are lowest by hour
of day and by weekday, the most traded goods, and unusual events such as
server restarts.

**Buying advice.** Offers below their fair value, stacks below it per
unit, equipment with cards below the worth of its parts, and offers below
what an NPC pays — each with its saving and how much it rests on. NPC
prices count with Overcharge (+24 %) while it is switched on.

**Calculates damage.** A pre-renewal damage calculator is built in, and its
DPS feeds the yield columns.

**Reads a shared market.** Every price check taken with Arcana Crawler
lands in [arcana-snapshots](https://github.com/SimonPaidla/arcana-snapshots).
Arcana reads it at start and every 15 minutes. It keeps the last 31 days
check by check, and every card's and item's daily prices and sales for
good.

## Arcana Crawler

Arcana Crawler collects the market for every Arcana. From **Start** to
**Stop** it takes a price check at every full hour — the cards, and the
item types you choose in its settings — and adds it to the shared store.
It asks for you only to sign in to the game; everything else it handles by
itself, and it carries on by itself after an error.

**What you need:** Windows 10 or 11, a game account, and access to the
shared store — ask the maintainer. The first start sets the crawler up
once; that takes a few minutes and a few hundred megabytes.

Only a current version can contribute. The crawler updates itself and
installs a new version only when no price check is running.

## Updates

Arcana asks this repository for a newer version at start and every six
hours after. At start it waits four seconds at most for the answer.

| What it finds | What happens |
|---|---|
| nothing newer | the app opens as always |
| a newer version | the start screen shows *Update 2.1.0 · 34 %*; when the download is done the app installs it silently and opens again as the new version |
| — and you press **Later** | the app opens at once; the update installs when you close it, or at once with *Restart now* |
| no connection, or no answer in time | the app opens as always; an answer that comes later installs when you close it |

Only the parts of the installer that changed are downloaded — usually a
few megabytes rather than the full installer of about 118 MB. The version
you are running stands beside the name at the top of the window, and
under *Settings → Arcana*, together with *Check for updates*.

Each download is checked against the SHA-512 in the release's
`latest.yml`. The installers are not code-signed, which is why Windows
warns before the first installation and never afterwards.

## Your data

| App | Folder | Holds |
|---|---|---|
| Arcana | `%APPDATA%\arcana` | the price checks of the last 31 days, the daily history, the game data, the settings, the log |
| Arcana Crawler | `%APPDATA%\arcana-crawler` | its price checks, its settings, your sign-in and access — encrypted —, the log |
| Arcana Crawler | `%LOCALAPPDATA%\arcana-crawler` | what it sets up at its first start |

Installing, updating and uninstalling never touch these folders. To
remove an app: *Settings → Apps → Installed apps → Arcana* (or *Arcana
Crawler*) *→ Uninstall*. Its folders stay; delete them by hand if you
want them gone too.

**Coming from Arcana 1.x:** Arcana 2.0 reads only price checks of Arcana
Crawler 1.1.0 and later, and the shared history started over on 24
September 2026. The data folder of 1.x under `%APPDATA%` is no longer
read and can be deleted.

## What a release contains

| File | What it is for |
|---|---|
| `Arcana-Setup-<version>.exe` or `Arcana-Crawler-Setup-<version>.exe` | the installer — the only file you download yourself |
| `….exe.blockmap` | the installer's block list; the next update is computed against it |
| `latest.yml` | the version, file name and SHA-512 the app checks against |

## For the maintainer

Releases are uploaded here as **drafts** from the source repository, by
`npm run release` for Arcana and `npm run release:crawler` for the
crawler. They reach the installations only when they are published by
hand. An Arcana release is published as **Latest** and never as a
pre-release. A crawler release is always a **pre-release**, so it never
takes the Latest mark that every Arcana asks for, and Arcana installs
only a release that carries `Arcana-Setup-<version>.exe`.

Three rules follow from every installation asking this address and no
other:

- **This repository is never renamed, deleted or made private.** A name
  given up can be registered by someone else, and every installation would
  then install whatever they publish.
- **No published release is ever removed.** The next differential download
  needs its `.blockmap`; without it every update is the full installer.
- **The version only goes up.** An installation never installs a lower
  one, so a mistake is corrected by a new release, not by withdrawing one.

Nobody else has write access here. Whoever can publish a release decides
what every installation runs.
