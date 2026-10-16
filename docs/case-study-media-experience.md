# Case Study: Engineering a Streaming Experience on a Self-Hosted Media Stack

> Scope: media client experience · Dates: October 2026 · Status: live in production

## Problem

By October 2026 the media pipeline itself was fully automated and verified:
a request interface fed an indexer search layer, which fed movie and TV
managers, a VPN-bound download client, automatic import, and a media server.
Six titles auto-imported end to end in one day.

But the *client* experience was bare. Watching anything meant:

- manually enabling English subtitles every session
- no skip-intro or skip-credits
- no scrub previews while seeking
- no trailers anywhere
- no recommendations ("what should I watch" had no answer)
- no playback analytics

The system worked; the product did not. This case study covers turning a
working pipeline into a working *service*, driven entirely through APIs and
version-aware plugin management, with every change verified against the live
runtime.

## Approach

1. **Recover the original design intent.** The owner's media vision had been
   written down months earlier (a four-tier plan: polish, automation,
   intelligence, integration). The automation tier was done; everything else
   was untouched. That document became the checklist.
2. **Research the ecosystem with the version in mind.** Community plugin
   catalogs, maintenance status, and compatibility were checked against the
   running server version before anything was installed. One release had
   just shipped with known migration breakage; the decision was to stay on
   the current stable version and revisit later.
3. **Drive everything through the server API.** No dashboard clicking for
   repeatable work: repositories, plugins, user policies, library options,
   scheduled tasks, and metadata refreshes were all configured
   programmatically so each change could be scripted, verified, and replayed.
4. **Verify each claim against the live system.** Several "done" steps turned
   out not to be. Reading logs and querying state directly caught them.

## What was built

### Skip intro and credits

Installed a community audio-fingerprinting analyzer (the same fingerprinting
family used by music identification services) and pointed it at the TV
library. It compares audio across episodes of a season, finds the repeated
opening and closing segments, and writes them into the server's native
media-segment API so every client that understands segments renders its own
skip button. Scheduled daily off-peak; the initial analysis pass runs
incrementally as new episodes arrive.

Also enabled a chapter-name segment provider as a fallback for files that
ship with chapter markers.

### Scrub previews (trickplay) and chapter images

Both are native server features that were simply off. Enabling them required
per-library option updates through the API (the endpoint shape is not
obvious: options are posted per library, not globally). Generation runs on a
schedule and pauses during playback.

### Hover trailers, powered by real identification

The hover-preview plugin was installed and configured, and then it did
nothing. Diagnosis found the actual blocker: the library had **zero provider
IDs**. No title was linked to a metadata database, so no trailer could ever
be looked up. The library had been imported during the manual era without
identification ever running.

The fix sequence:

1. Obtained and wired a free metadata API key (validated with a live call
   before writing it anywhere).
2. Discovered that a normal refresh does **not** re-identify items that
   already have local metadata. The mode that works is a replace-all
   metadata refresh, and it must be run per item.
3. First batch attempt: 49 items queued back to back. Result: zero
   identifications, and previously identified items reverted. Logs showed no
   rate-limit responses, disproving the initial theory. The reliable method
   turned out to be **serial with per-item verification**: refresh one item,
   poll until its provider ID lands (10 to 30 seconds), move to the next.

Result: all 29 films identified; 24 carry trailer links (the five without
are brand-new releases the metadata provider has not indexed trailers for).
18 of 20 series carry trailers. Hover previews then worked after a client
cache refresh.

### Always-on, best-quality subtitles

Two layers:

- **User policy**: subtitles set to always play, English preferred, so the
  client never starts without them when a track exists.
- **Automation**: the subtitle manager had credentials but no operating
  policy. Enabled English as the only wanted language with a strict quality
  score, default-on for all movies and series, automatic upgrades of
  image-based subtitles to text (image subtitles force full video
  transcoding; text streams direct-play), and a six-hour search schedule.

Remaining gap recorded honestly: a handful of niche titles have no English
subtitles published anywhere. A local speech-to-text fallback is a possible
future lane, not something silently claimed as done.

### A recommendation layer from real watch history

Three engines, layered:

- **Trakt integration** (already installed): scrobbling and watched-state
  sync verified live, with token self-refresh confirmed.
- **Virtual recommendation libraries**: a plugin pulls per-user
  recommendations from the scrobble history and exposes them as real
  library shelves inside the media server. Standing up these libraries was
  the hardest part: the plugin does not create them, its expected folder
  layout is exacting (user-id format, path casing), and the manual setup
  step is only hinted at in the README. Registering the three libraries
  against the plugin's actual on-disk layout made 50 movie recommendations
  and 50 show recommendations appear as browsable shelves, plus a
  next-seasons shelf that fills in as shows are finished.
- **Local recommendations**: a privacy-first engine that scores from local
  watch history with no external service.
- **Ratings and diary plugin**: per-user ratings, watchlists, and diary with
  optional sync to external tracking services.

The scrobble provider was also configured to exclude the virtual shelves so
browsing them never pollutes watch history.

### Playback analytics

Deployed a statistics dashboard (app plus its own database) that ingests the
server's playback-reporting data: watch time, most-played titles, device
mix, and live sessions. Local-only exposure. The deployment surfaced a nice
quirk: the app's default database name differs from its own documentation,
which cost a false "setup failed" verdict until checked directly against the
database.

### Dashboard media cards and notifications

- Added continue-watching and recently-added cards to the main dashboard,
  fed by a deterministic status writer that flattens array data into text
  fields (an earlier rendering crash ruled out mapping arrays of objects
  directly).
- Wired new-media notifications into the owner's Discord surface with poster
  art, matching how the rest of her automation already communicates.

## Debugging and operations lessons

| Symptom | Root cause | What this taught |
|---|---|---|
| Hover previews never fire | Library had no provider IDs at all | Working plugins need working data; check the data layer before blaming the plugin |
| Bulk metadata refresh produced zero results | Refresh jobs queued in bulk are silently dropped; a normal refresh does not re-identify | Verify per item, serially; scale only after one path is proven |
| A plugin catalog install "succeeded" but produced no files | The catalog route silently no-ops for that package | Confirm files on disk, not HTTP 204s |
| Recommendation shelves invisible | The plugin requires manually registered libraries at an exacting path | Read the plugin source when the README is thin |
| Analytics dashboard "empty" | Wrong database name in my check, not a failed setup | Read the system's actual state before declaring failure |

## Sanitization note

This page describes the work without publishing the private source,
credentials, internal addresses, library contents, or personal data.
Verification counts refer to the owner's private library and are reported
here as evidence of the method, not as a content catalog.
