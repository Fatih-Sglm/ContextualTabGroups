# Contextual Tab Groups


**Forked from [SpookyKipper/ContextualTabGroups](https://github.com/SpookyKipper/ContextualTabGroups)**, the original extension by Spooky Kipper. The original idea, design and code come from that project; this fork builds on top of them.

> **Modified fork.** This repository is a modified version of the original above, distributed under the same license (GPL-3.0, see [LICENSE](LICENSE)).
> Modified on 2026-11-15: security cleanup (no npm dependencies, developer default entries removed, CSP, search-query group names off by default), group-based domain rules with colors, Turkish UI, redesigned options page, tests and a packaging workflow.
> This fork is not published in any extension store; the original extension's store listings do not contain these changes. Install it from this repository (see [Installation](#installation)).

### Group tabs by context for you automatically. Inspired by Opera One.

Features:<br>
- ✅ Automatic Tab Groups Creation (Custom Tab Group Names)<br>
  - Default & Search Engine tabs can be set differently!
  - Supports setting Tab Group names to your search query!
- ✅ Auto Disband Groups with only 1 tabs (togglable)<br>
- ✅ Alt+T Shortcut to quickly create a new group (shortcut changable/deletable)
- ✅ Domain rules: create colored groups and list domains under them; matching tabs move into their group automatically
- ✅ English and Turkish UI

---
## Installation
This fork is distributed only through this repository:
1. Download the zip for your browser (`chrome`, `edge` or `firefox`) from this repository's **Releases**, or build it yourself (see [Building](#building)), and unzip it.
2. Chrome / Edge / other Chromium browsers: open `chrome://extensions` (`edge://extensions`), enable **Developer mode**, click **Load unpacked** and pick the unzipped folder.
3. Firefox: open `about:debugging#/runtime/this-firefox`, click **Load Temporary Add-on** and pick `manifest.json` (temporary until the browser restarts; unsigned add-ons cannot be installed permanently).

---
## ✅ Fully Supported Browsers
- Google Chrome
- \[Ungoogled] Chromium
- Microsoft Edge
- Brave
- Naver Whale
- Firefox 139/+
  
Most Chromium & Firefox forks (aside from the ones below) should work, but may impose limitations or issues.
## ⚠️ Supported Browsers but need additional setup
- Zen Browser
  - Use this userChrome.css: https://github.com/Vertex-Mods/Advanced-Tab-Groups/blob/main/userChrome.css
  - This userChrome.css is not affiliated with this extension, but it does the job!
- Opera One & Opera GX
  - Disable "Automatically create Tab Islands" (let this extension handles it)
    
## ❌ Unsupported Browsers

- Vivaldi
  - Does not support Tab Groups API
- Kiwi, Quetta, Orion or any mobile browsers that allows Chrome Extensions
  - Does not support Tab Groups API

---

⚠️ Using any third-party newtab extensions or a custom newtab page may break extension functionality

---
## 1. Automatic Tab Groups Creation
| No Tab Group Name     | ![](https://github.com/SpookyKipper/TabIslandsForChrome/blob/main/repo_assets/AutoCreateNoName.gif)      | 
| ------------- | ------------- | 
| Custom Tab Group Name          | ![](https://github.com/SpookyKipper/TabIslandsForChrome/blob/main/repo_assets/AutoCreateWithName.gif)         | 
| Search Engine Group Name | ![image](https://github.com/user-attachments/assets/7bd50289-df37-4117-b0f9-3b6bd47615de)



## 2. Auto Disband Groups with only 1 tabs 
Can be toggled via extension options
| ![](https://github.com/SpookyKipper/TabIslandsForChrome/blob/main/repo_assets/AutoDisband.gif) |
| ------------- |

## 3. Alt+T Shortcut 
No Mouse Click is involved <br>
Changable/deletable via `chrome://extensions/shortcuts`
| Active Tab not in group: <br> Create new group | ![](https://github.com/SpookyKipper/TabIslandsForChrome/blob/main/repo_assets/AltPlusT.gif) |
| ------------- | ------------- |
| Active Tab already in group: <br> Add to existing gruop | ![AltPlusT_InGroup](https://github.com/user-attachments/assets/514657e2-44a1-456c-9875-4f14bd333b8d)




## Extension Options
Settings are available via Extension Popup -> "Go to options" button<br>
UI languages: English, Turkish (follows the browser language, see `src/base/_locales/`).<br>
The options page has two tabs: **Behavior** (general settings) and **Groups** (domain rules). Neither opens by default: until you pick one, a short welcome guide explains what the extension does and walks you through your first group ("Create my first group"). The options page opens by itself right after the extension is installed.

| English | Türkçe |
| ------------- | ------------- |
| ![Welcome guide (English)](repo_assets/options-welcome-en.png) | ![Karşılama rehberi (Türkçe)](repo_assets/options-welcome-tr.png) |


| English | Türkçe |
| ------------- | ------------- |
| ![Behavior tab (English)](repo_assets/options-behavior-en.png) | ![Davranış sekmesi (Türkçe)](repo_assets/options-behavior-tr.png) |

### Name for automatically created groups (Default)
This is the name for the Tab Groups being automatically created by the extension. <br>
Available Placeholders: *Experimental*<br>
- `%domain%`
  - `google.com` will return `Google`
  - `web.whatsapp.com` will return `Whatsapp`
  - `www.google.com.hk` will return `Google`
### Name for automatically created groups (Search Engines)
This is the name for the Tab Groups being automatically created by the extension, but the tab you created the new tab on is a search engine.<br>
**Off by default** (empty): group names may sync to your browser account, so search queries are not used unless you set e.g. `%search_query%` here.<br>
Available Placeholders:<br>
- `%search_query%` Your search engine search query
  - You searched `cat pics` on Google, the tab group name will be `cat pics`.

Supported Search Engines: Google, Bing, BraveSearch, Ecosia, DuckDuckGo, Ask.com, Yahoo, Startpage, Baidu, YouTube
### Groups (domain rules)
Options -> "Groups" tab: create a group (name + color), then add domains under it.<br>
A tab navigating to a listed domain (or a subdomain of it) is moved into that group in the same window, created with the group's color if missing. A domain can optionally override the color; the override is used only when a tab from that domain creates the group. A group without color only sets the `%domain%` name (legacy behavior). Rule groups are never auto-disbanded. Pinned tabs and popup windows are ignored. A tab you ungroup manually stays ungrouped until it navigates to a new URL.<br>
Colors are limited to the browser's 9 tab group colors (the tab groups API does not accept custom hex colors).

| English | Türkçe |
| ------------- | ------------- |
| ![Groups tab (English)](repo_assets/options-groups-en.png) | ![Gruplar sekmesi (Türkçe)](repo_assets/options-groups-tr.png) |

### Disband Groups with only 1 tab in it
- A toggle to whether automatically ungroup tab groups with only 1 tab in it (does not apply to rule groups)

## Building
No `npm install` needed, only Node.js (built-in modules).
1. run `node buildExtension.js <browser>`
2. Unpacked extension will be available at `dist/<browser>`
3. Pack the extension as ZIP via your File Manager

Tests (no dependencies): `node tests/rules.check.mjs` runs the domain-rule logic against a mocked browser API and an in-memory IndexedDB.

### Downloadable packages (GitHub Actions)
`.github/workflows/build.yml` runs the tests and builds `contextual-tab-groups-<version>-<chrome|edge|firefox>.zip`:
- on every push to `main`, pull request or manual run: download the zips from the run's **Artifacts**;
- on a tag `vX.Y.Z` (must match the version in `manifest/base.json`): the zips are attached to the GitHub Release.

Supported browsers are `chrome`, `firefox`, `edge`<br>
Any other chromium-based browsers not listed here should also use `chrome` when building.

## Credits
Original extension: [Contextual Tab Groups](https://github.com/SpookyKipper/ContextualTabGroups) by Spooky Kipper (GPL-3.0). This fork keeps that license.<br>
Extension Idea: [Opera One Tab Islands](https://www.opera.com/features/tab-islands)
