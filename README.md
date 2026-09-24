<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/logo.svg">
    <img src="assets/logo-light.svg" alt="Arcana" width="200">
  </picture>
</p>

# Arcana releases

Installers for two Windows apps around the card market of the uaRO private
server. The source code is kept elsewhere; this repository holds the builds
and nothing else.

| App | What it does | Releases |
|---|---|---|
| **Arcana** | follows the card market, ranks pre-renewal cards by what they are worth and how long they take to farm, and says what is worth buying now | `v<version>`, the release marked **Latest** |
| **Arcana Crawler** | takes the market every full hour and shares it with every Arcana | `crawler-v<version>`, always a **pre-release** |

**[Download Arcana](https://github.com/SimonPaidla/arcana-releases/releases/latest)**
(`Arcana-Setup-<version>.exe`, Windows 11 x64). Arcana Crawler is the
newest `crawler-v…` pre-release on the
[releases page](https://github.com/SimonPaidla/arcana-releases/releases)
(`Arcana-Crawler-Setup-<version>.exe`). You only need it if you want to
contribute crawls.

Once installed, both apps keep themselves up to date from here. There is
nothing to download a second time.

## Install Arcana

| | |
|---|---|
| 1 | Download `Arcana-Setup-<version>.exe` from the [latest release](https://github.com/SimonPaidla/arcana-releases/releases/latest). |
| 2 | Run it. It installs for your Windows user — no wizard, no administrator prompt — and opens. |
| 3 | If Windows says *Windows protected your PC*: the installer is not code-signed. *More info* → *Run anyway*. This happens once. |

**What you need:** Windows 11 x64. Arcana reads the market from a shared
store and needs no account, no browser and no token.

## What Arcana does

**Market.** What moved in the last hour, day, week or month, and one card
in full:
- its price now, its **fair value** (what it sells for at today's prices), and a rating of the price against the month;
- median and mean prices over 24 hours, 7 and 30 days, and the confirmed sales;
- a price chart with the sales in it;
- what to ask when you sell, and whether to sell now or wait.

**Economy.** The market as a whole: merchants online, card offers, sales
and zeny traded, and a price index that shows whether cards are getting
dearer or cheaper. It also shows when prices are lowest and sales most
frequent, by hour of day and by weekday, the most traded cards, and
unusual events such as server restarts.

**Ranking.** Every card with its price, fair value, rating, sales, farm
spot, hours per card and zeny per hour, and a score weighing value
against hit points against spawn count. Hovering a price opens the
individual offers behind it — vendor, shop, coordinates. It can be saved
as Excel or CSV.

**Buying advice.** Offers well below their card's fair value, each with
its saving, what reselling would bring, and how much it rests on. Cards
whose price is falling are held back: waiting is the better buy.

**Calculates damage.** A pre-renewal damage calculator is built in, and its
DPS feeds the yield columns.

**Reads a shared market.** Every crawl taken with Arcana Crawler lives in
[arcana-snapshots](https://github.com/SimonPaidla/arcana-snapshots).
Arcana reads it at start and every 15 minutes. It keeps the last 31 days
crawl by crawl, and every card's daily prices and sales for good.

## Arcana Crawler

Arcana Crawler runs a browser in the background from **Start** to
**Stop**. At every full hour it reads every card offer on the server,
keeps the result, and offers it to the shared store as a pull request. A
window opens only when a person is needed: to sign in, or to answer a
Cloudflare check. Everything else it works around by itself.

**What you need:** Windows 10 or 11, a uaRO account (you sign in yourself,
in the crawler's window), and a GitHub token for `arcana-snapshots`. The
token is fine-grained, for that repository only, with *Contents* and *Pull
requests* read and write. The first start fetches the browser, about
470 MB, once.

Only the newest crawler writes the format the store accepts. It updates
itself, and installs a new version in a quiet moment, when no crawl is
running and no sign-in window is open.

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
| Arcana | `%APPDATA%\arcana` | the crawls of the last 31 days, the daily history, the game data, the settings, the log |
| Arcana Crawler | `%APPDATA%\arcana-crawler` | its own crawls, the ones waiting to be offered, the encrypted token and sign-in, the browser profile, the log |
| Arcana Crawler | `%LOCALAPPDATA%\arcana-crawler\camoufox` | the browser |

Installing, updating and uninstalling never touch these folders. To
remove an app: *Settings → Apps → Installed apps → Arcana* (or *Arcana
Crawler*) *→ Uninstall*. Its folders stay; delete them by hand if you
want them gone too.

**Coming from Arcana 1.x:** Arcana 2.0 reads only crawls in the format of
Arcana Crawler 1.1.0, and the shared history started over on 24 September
2026. The folder of 1.x, `%APPDATA%\uaro-card-crawler`, is no longer read
and can be deleted.

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
