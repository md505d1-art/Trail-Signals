# Trail Signals

A mobile app for casual outdoor explorers. It finds a nearby walk, park, viewpoint or picnic spot, shows what recent visitors noticed, and gets you there by bus, train, tram or ferry, final walk included. It works in any country.

## The app

- **Open on your phone (Claude app):** https://claude.ai/artifact/TbWcUSnZczmkCFMdb2nC3z (private until shared from its Share menu)
- **Web version:** [`index.html`](index.html) at the repo root. To host it, turn on GitHub Pages for this branch (Settings → Pages → deploy from branch, root folder). The page must be served over HTTPS for location to work.
- **Source:** [`app/trail-signals.html`](app/trail-signals.html). This is the page body; `index.html` is the same content wrapped in a standalone HTML document.

### Install on a phone

Scan [`qr/trail-signals-qr-card.png`](qr/trail-signals-qr-card.png), open the link in Safari (iPhone) or Chrome (Android), then choose **Add to Home Screen**. The web QR points to a fixed commit served through raw.githack.com; regenerate it after big changes, or switch it to a GitHub Pages address once Pages is turned on.

### How it finds places

| Where it runs | Your location | Places and stops | Travel times |
|---|---|---|---|
| Web version (`index.html`) | Device GPS, or type any town | Live from OpenStreetMap (Overpass API), with Nominatim for place names | Estimated from distance and stop type, clearly labelled |
| Claude app artifact | Type any town, area or station (the app sandbox blocks GPS and outside map data) | Suggested by Claude, labelled "Suggested by Claude · check details" | Typical times from Claude, labelled as such |
| Anywhere | Demo city | Made-up sample places | Made up |

Sunrise, sunset and dusk are calculated on the device for the starting point, so the daylight warnings work anywhere. Every spot links to Google Maps transit directions and OpenStreetMap for live times.

### Screens

- **Explore:** brand header, a location pill, place search, a daylight bar and compact filter chips. Below that is the **Signal radar**: you're in the middle, the rings are minutes door to door, and each spot sits in its real compass direction. Spots pulse green or amber when visitors have reported something in the last 3 days. A marker shows where the sun sets. There's also a featured-spot card, "Surprise me", and the full list.
- **Place details:** illustration (generated per place and time of day), stats, latest-update banner, daylight advice, public transport options, lines at the stop, visitor updates with "Still true" / "Not now", and tips.
- **Plan your trip:** leave now, later or "Catch the sunset". You get an outbound timeline with a final-walk sketch and directions. A return-journey toggle lets you choose how long to stay and checks whether you'll walk back in daylight. Trips can be saved.
- **Add an update:** pick what you noticed, where and when, then add a note and an optional photo. In the Claude artifact, updates are shared with everyone who can use the page; elsewhere they stay on the device.
- **Saved, Trips, Updates** tabs.

## Earlier design canvas

The first static design (four interactive artboards): https://claude.ai/artifact/6i7kFvX62BcfV5mNAHgcPd (private until shared from its Share menu)

The design source is in [`design/project/`](design/project). Each screen is a self-contained, interactive `.dc.html` artboard at 390 px phone width, laid out by `design/project/canvas.json`.

## Screens

| # | Screen | File | What you can try |
|---|--------|------|------------------|
| 1 | Explore | `Main.dc.html` | Filter by travel time, activity and effort; the map pins and results list update together. Includes an empty state. |
| 2 | Place details | `PlaceDetails.dc.html` | Photo, difficulty, visit time, path and daylight facts, the "route last checked" banner, visitor updates you can confirm, and a choice of bus or train. |
| 3 | Trip planner | `TripPlanner.dc.html` | Switch between a quicker route (one change) and a direct bus, follow the timeline down to the final walk with a mini map, then switch to **Getting back** to pick a return bus with daylight guidance and a reminder. |
| 4 | Share an update | `AddUpdate.dc.html` | Pick what you noticed, where and when, add a note, see the posted result, then undo it. |

Screens link to each other in Play mode: card → details → plan, and "Update" → share.

## Design principles

- **Spontaneous, then certain.** Explore leads with door-to-door minutes, so "what can I reach this afternoon?" is answered first. The details screen and the planner then add the specifics.
- **The last kilometre is part of the trip.** Every option shows the final walk from the stop as its own leg, with distance, time and climb. The planner gives step-by-step directions and a mini map for it.
- **Honest about uncertainty.**
  - Visitor reports are always labelled as visitor reports, with when they were *seen*. They fade after 3 days ("may be out of date") and anyone can mark them "Still true" or "Not now".
  - Curated info carries a "last checked" date (route checked 12 Oct; directions checked 12 Oct).
  - Transit times say whether they are **Live** (with an "updated N min ago" age) or **Timetabled**, and explain when live data will appear.
  - Each transfer offers a backup departure in case a connection is missed.
- **Safety without alarm.** Sunset time, when to start back and an unlit-path warning sit next to the return options, as plain guidance rather than red alerts.

## Visual system

| Token | Hex | Use |
|-------|-----|-----|
| Forest | `#2E5B3B` | Primary actions, selected states |
| Forest deep | `#1F4029` | Headings, train line, summary card |
| Sky | `#2C6E95` | Bus line, links, info |
| Sky tint | `#DDEBF3` | Info and "last checked" notes |
| Cream | `#F8F3E6` | App background |
| Card | `#FFFDF8` | Surfaces |
| Ink / Muted | `#1D2620` / `#55625A` | Body / secondary text (both pass 4.5:1 on cream) |
| Caution | `#7A4E00` on `#FBECC8` | Mud, closures, dusk warnings |

- **Type:** Bricolage Grotesque for display headings and key numbers; Figtree for UI and body text.
- **Transit modes** are told apart by colour, icon *and* label. Bus is a sky-blue badge, train is a deep-green badge, and walking is a dotted grey rail. Colour is never the only signal.
- **Difficulty** combines a three-bar meter with a word (Easy / Moderate / Hilly) and a plain description of the climb.
- **Accessibility:** touch targets are at least 44 px. Controls are real buttons and links with `aria-pressed` states, icon-only buttons have labels, and focus rings are visible.

## Notes

All places, routes, times and stops are fictional sample content for the design.
