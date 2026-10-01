# LyricLayer privacy policy

Updated 1 October 2026. This page covers releases 0.9.3 and 0.9.4 and retains the prior 0.5.1 policy for users who still have that version installed. Version 0.9.4 changes only the extension name and store description; the data practices described for 0.9.3 remain the same. Use the section matching your installed version.

## Versions 0.9.3 and 0.9.4

Updated 1 October 2026. This policy describes LyricLayer 0.9.3 and its metadata-only 0.9.4 update for Google Chrome and Microsoft Edge. Publisher: raccooovl. Privacy contact: [LyricLayer issues](https://github.com/raccooovl/lyriclayer/issues). Issues are public, so do not include sensitive information.

LyricLayer reads the current YouTube video's ID, title, artist/channel, playback position, duration and ad state to find and display lyrics. Fresh installations automatically find and display matching lyrics. Existing explicit Off preferences remain off. Automatic searching, timing checks and local audio matching have separate settings.

Playback position and state are used in memory for synchronization, timing edits, seeking and practice loops. LyricLayer does not retain a playback or interaction history. It does not log page clicks, typed keys, scroll activity or mouse movements, monitor other websites' network traffic, or send usage analytics. Its own buttons, text fields, keyboard shortcuts and subtitle-position controls handle your actions only to perform the requested function. Position controls save the resulting subtitle placement, rather than a pointer-movement log.

### Chrome Web Store Limited Use

LyricLayer follows the Chrome Web Store User Data Policy and its Limited Use requirements. Data accessed by the extension is used only for the lyric search, display, synchronization, editing and saving features described in this policy. Transfers to enabled lyric providers are limited to the requests described below. The publisher does not sell data, use it for advertising or profiling, or allow people to read it for unrelated purposes. Local audio and captions are not uploaded. Any diagnostic file you choose to share for support is shared only through your own explicit action; review it first and avoid posting sensitive information in public issues.

### Lyrics requests

LyricLayer checks the current video's saved lyrics before starting an automatic provider search. LRCLIB and NetEase are enabled by default, with LRCLIB tried first. Kugou is disabled until you enable it in the source settings. The exact unmarked LRCLIB-only list saved by 0.8.0 is migrated to the new defaults; other legacy lists and all-off choices are preserved. Preferences now mark whether a source list is a default or an explicit choice. You can choose a preferred enabled source and disable individual sources, including all of them. Disabling all lyric sources leaves saved lyrics and local imports available; it does not disable the separate YouTube caption timing feature.

Searches contact the preferred enabled source first. Other enabled sources are used only if a suitable match is unavailable, unless you explicitly request results from all enabled sources. Disabled sources are not contacted for new lyric searches. Changing source settings governs new searches; it cannot erase information already received by a service. Source availability and lyric accuracy vary.

Requests go directly to enabled services over HTTPS:

| Service | Information sent | Purpose |
| --- | --- | --- |
| LRCLIB at lrclib.net | Song query, artist/title and video duration where supported; recording lookup parameters | Find recordings and retrieve lyrics |
| Kugou at lyrics.kugou.com | Song query and video duration where supported; candidate recording identifier and provider-supplied access key | Find recordings and retrieve lyrics |
| NetEase at music.163.com | Song query and candidate recording identifiers | Find recordings and retrieve lyrics, available translations and word timing |

Search text can come from the video's public title and artist/channel, or from what you type. For live/acoustic videos, the extension may search both the performance title and the underlying song. Avoid including unrelated private information in a search. LyricLayer does not add a separate YouTube video ID or watch URL to lyric-provider requests. Text entered into the query is still transmitted as query text and may reveal music you are viewing or looking for.

Lyric-provider requests omit cookies. Providers receive normal network information such as IP addresses and request headers and may retain logs under their own policies. LyricLayer does not request GPS or device geolocation and does not control providers' retention or processing. There is no publisher-operated proxy or lyric server.

### Caption timing

With lyrics and automatic timing enabled, the extension can read loaded caption tracks and request up to three tracks from the current video's https://www.youtube.com/api/timedtext URLs. These requests use the normal same-origin YouTube session, including applicable YouTube cookies.

Caption responses are size-limited and held temporarily in page memory. Phrase matching happens locally. Raw caption text is not sent to lyric providers, the publisher or an AI service. Successful delays and matched original lyric timelines can be saved for the current video.

When an exact timed performance recording is unavailable, a similar-length original recording of the same song and artist may supply its existing timestamps. The interface identifies this fallback. The timestamps are not stretched or presented as independently verified performance alignment. This matching adds no new data destination or behavioral log.

### Local audio matching

When an identified live/acoustic performance has eligible lyrics but no established caption timing, normal playback can start local audio matching. This is enabled by default and can be disabled under **Live & acoustic matching → Prepare replay timing from audio**.

The extension reads the current video element's audio stream, converts bounded windows to mono samples and processes them using packaged Whisper Tiny model weights in a local browser worker. It does not use the microphone, record the screen, upload audio or fetch a remote model. It has no cloud recognition service. The offscreen permission supports this local worker, and the extension policy permits its bundled WebAssembly runtime.

Audio samples and model transcripts remain in temporary memory. They are not written to extension storage. Only matching source lyric text, video-relative timestamps and a small match summary are saved. Processing is bounded to 12 windows per visit with one job at a time. Navigation, Off, manual timing, seeking or pausing cancels stale work. Idle model memory is released. Recognition of singing and complete timelines are not guaranteed.

Turn off **Prepare replay timing from audio** to stop audio analysis while retaining caption checks. Turn off **Check timing automatically** to stop both kinds of new checks. Turning lyrics off stops pending work. Saved timing remains until you change it or use **Forget this video**.

### Local storage and controls

Floating lyrics use the same current lyrics and YouTube playback state in memory. Play, pause and seeking control the existing player. Only the resulting Compact/Scrolling view preference and its migration-version marker are saved; opening, closing, scrolling, keyboard events and playback positions are not logged. Version 0.9.1 changes unmarked view settings to Compact once and retains subsequent explicit choices. The marker is configuration metadata, not an event log. The floating window uses native Document Picture-in-Picture and adds no permissions, remote service or analytics. Its keyboard shortcuts operate only while the lyric list is focused. The modern style uses local CSS, system fonts and icons.

Preferences and up to 40 selected-video entries are saved in local extension storage, not browser sync. Preferences include display/appearance, automatic-search and matching settings, enabled lyric sources, the preferred source and a version/origin marker distinguishing source defaults from explicit choices. This marker is configuration metadata, not an interaction-event log. Entries can include video ID, selected recording/lyrics, source word timings/translations, imports, delay, individual-line or section timing corrections, matched performance timing, a match summary and update time. These entries are a limited local record of videos for which lyrics were saved. Old entries are pruned when saving keeps the 40 most recently updated entries; there is no separate age expiry. Raw captions, audio and recognition transcripts are not persisted.

The timing editor saves the resulting lyric timeline corrections, rather than a history of clicks or timing-edit commands. Undo history stays in memory. Reading mode uses lyric lines for display and optional seeking. Practice selections, loop endpoints and playback-speed controls remain in memory and are not added to saved video entries or transmitted to lyric providers. YouTube handles playback through its own player and policies.

Recent lyric-provider responses are cached in the extension's background memory for reuse for up to 15 minutes, subject to 48 entries and an estimated 4 MiB limit. This is not browser sync or a persistent search-history database. The cache is lost when the background context is discarded; expired responses can remain in memory until accessed, evicted or that context ends.

**Forget this video** removes its saved selection and timing. Removing the extension clears local storage. Exported LRC files remain in the download location until removed separately.

Original lyrics are displayed by default. Providers may return optional translations while display is off. Imports stay local. Explicit Genius and source links open ordinary websites, with their own cookies and privacy practices; the Genius link includes the current search query. The toolbar uses activeTab to control the current YouTube tab, and storage holds local preferences.

LyricLayer has no publisher server, accounts, analytics, advertising, payments or remote executable code. Its data handling supports lyric search, display, customization, timing and local saving. It does not sell data or use it for credit decisions. It does not request passwords, financial or health information, personal communications, or precise device location. The policy is updated when these practices change.

### Diagnostic report

The optional diagnostic download contains the current video ID/title and duration, settings, provider selection identifiers, timing coverage and processing/error counts. It excludes the current playback position, paused/playing state, playback speed and ad state. It contains no interaction-event history, lyric text, recognition transcript, audio, cookies or credentials. It is saved to your download location and is never uploaded automatically. Review it before sharing it. Diagnostic downloads and exported LRC files remain outside extension storage until you delete them separately.

---

## Version 0.5.1 (retained policy)

Last updated: 29 September 2026. Applies to LyricLayer version 0.5.1.

**Publisher:** raccooovl

**Privacy contact:** [LyricLayer GitHub issues](https://github.com/raccooovl/lyriclayer/issues). Issues are public; do not include passwords, private account information or other sensitive personal information.

**Policy location:** [LyricLayer privacy policy](https://github.com/raccooovl/lyriclayer/blob/main/PRIVACY.md)

### What this policy covers

LyricLayer is a Microsoft Edge extension that displays timed song lyrics on desktop YouTube watch pages. This policy describes the extension's handling of information. YouTube, Microsoft Edge, lyric services and any websites you open have their own data practices.

### Information used on your device

On a YouTube watch page, LyricLayer reads the current video's identifier, public title and channel/author name. It reads playback position, duration, playback state and whether the player is showing an advertisement to match and display lyrics. These playback values are used locally; video duration can also be included in lyric searches as described below. LyricLayer does not capture or upload the song's audio or video.

When you open the extension popup, it checks the active tab's URL to determine whether it is a supported YouTube watch page and to control that tab. It does not read your browser's full browsing-history database.

The extension also uses the text you enter in its search, lyric import, translation and timing controls. A file is read only after you choose it in the import control. Imported text and line timings are processed locally; the extension does not upload those documents to a server.

### Information sent to lyric services

A lyric lookup can start when you open lyric settings or turn lyrics on without a loaded recording, when you press Find, or on new videos if you enable automatic searching. Automatic searching on new videos is off by default.

The extension sends requests directly from your browser to:

| Service | Information sent by the extension | Purpose |
| --- | --- | --- |
| LRCLIB at lrclib.net | Detected or entered song query, and artist, track name and video duration where available | Find recordings and retrieve lyric data |
| Kugou at lyrics.kugou.com | Song query and video duration where available; then the provider's recording identifier and download access key | Find recordings and retrieve lyric data |
| NetEase at music.163.com | Song query; then the provider's recording identifier | Find recordings and retrieve lyrics, available translations and word timing |

Search text may be derived from the video's public title and author, or from what you type. Avoid putting unrelated private information in a song search. The extension does not include your YouTube video identifier or full watch URL as an API request parameter. Search terms can still reveal which music you are viewing or looking for.

These are HTTPS requests. The lyric API requests omit browser credentials such as cookies. The services still receive the network information needed to handle the requests, such as your IP address and ordinary request headers, and may retain logs under their own policies. LyricLayer does not control their retention, processing locations or response content.

The extension has no publisher-operated server, analytics endpoint or advertising endpoint in version 0.5.1. It does not transmit these requests through a publisher server.

### Translations and word timing

Original lyrics are displayed by default. A provider response can include translation or word-timing data even when the display option is off. That data may be kept with the selected recording locally. Turning translation display off hides the second line; it does not prevent the provider from returning translation data with a lyric request.

A translated LRC you import is saved locally with that video's selected lyrics. LyricLayer does not send it to a translation service or generate a translation.

### Local storage and retention

LyricLayer uses Microsoft Edge's local extension storage, not its sync storage, for:

- Display, position, translation, word-highlighting, transition and automatic-search preferences, including whether lyrics are shown.
- Saved selections for up to 40 videos, identified by YouTube video ID. Each saved entry can include recording metadata, source identifiers, lyrics, source translations and word timing, imported lyrics or translation, your timing delay, whether the recording was automatically selected, and an update timestamp.

When a saved entry is written, older saved video entries are removed so the 40 most recently updated entries remain. Entries do not otherwise have a time-based expiry. Preferences remain until changed or extension data is removed. These saved IDs and selections are a local record of videos for which lyrics were saved.

Recent lyric API responses are also cached temporarily in the extension's background memory, for reuse for up to 15 minutes. The cache is limited to 48 entries and an estimated 4 MiB. It is not a persistent lyric-history database and is lost when that background context is discarded. Expired responses are not reused, although an expired entry can remain in memory until it is accessed, evicted or the context ends.

If you use Export LRC, the browser saves a text file to your chosen download location. Its filename includes the YouTube video ID. Exported files are outside the extension's local storage and remain until you delete them yourself.

### Your controls

- **Forget this video** removes that video's saved lyrics and timing entry. It does not erase preferences, other saved videos, exported files or provider-side logs.
- **Use source translation** removes an imported translation from the saved selection and returns to a source translation when one exists.
- **Show source translation underneath** controls translation display. Original-only display is the default.
- Disable **Find lyrics automatically on new videos** to stop future automatic new-video lookups. Opening lyric settings or pressing Find can still start a lookup. Changing this preference does not cancel requests already underway.
- The **Lyrics** button controls the overlay. Hiding lyrics alone does not turn off the separate automatic-search preference.
- Disable or remove LyricLayer through Microsoft Edge's extension management to stop the extension running. Removing it also removes its local extension storage. Downloaded LRC files must be deleted separately.

Saved lyrics can be viewed when you revisit their video, and the selected original line lyrics can be exported as LRC. The extension has no bulk history viewer, full-data export or dedicated clear-all button. For questions about information handled by the publisher, use the privacy contact above; information already sent to independent lyric services is subject to those services' controls.

### Links you choose to open

**Find lyrics on Genius** opens a normal Genius search page with the current song query. It does not fetch or scrape Genius lyrics inside the extension. Source links open the service's website. These sites can receive normal navigation information and use their own cookies or accounts under their policies. Omitting credentials on lyric API requests does not apply to a website you open normally.

### Other uses and policy changes

The extension contains no analytics, advertising, payment or account system, and does not sell information or use it for credit decisions. Its information handling supports lyric search, display, customization and local saving. It does not request passwords, financial information, health information or precise device location.

This policy will be updated when the extension's data practices change. The last-updated date above identifies the policy version. Contact the publisher using the privacy contact at the top of this page. GitHub handles visits and public issue submissions under its own policies.

### Interaction handling

LyricLayer uses the current media playback position transiently to choose the lyric line to display and to create timing adjustments you request. Its controls respond locally to clicks, keyboard commands and subtitle dragging. It saves the resulting lyric choices, timing edits, subtitle position and other preferences; it does not keep an interaction history, clickstream, keystroke or scroll log, pointer trail, or a record of network traffic. Playback positions and control events are not sent to the publisher or lyric services.

Saved video identifiers remain a local browsing-related record, lyric metadata and text remain website content, and online lyric services receive normal connection information including IP addresses. These practices remain disclosed even though ordinary local controls are not classified as collection of behavioral activity.
