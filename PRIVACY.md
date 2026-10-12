# LyricLayer privacy policy

Updated 12 October 2026. This policy describes LyricLayer 1.8.4 for Chrome and Edge. Earlier store policies are retained below for installed older versions. Publisher: raccooovl. Privacy contact: [LyricLayer issues](https://github.com/raccooovl/lyriclayer/issues). Issues are public; do not include sensitive information.

LyricLayer has no publisher-operated server, account system, analytics, advertising or payment service. It does not sell data, upload audio or use a cloud recognition/translation API. It searches enabled third-party lyric sources and stores its working data locally. Saved song records, practice phrases and cached queries can reveal songs you searched for or saved even though there is no separate interaction-event log.

## Information used on YouTube

On desktop YouTube and YouTube Music, LyricLayer reads the current video's ID, title, artist/channel, duration, playback position/state and ad state to find lyrics and keep them synchronized. YouTube Music integration can inspect the next queued song's metadata locally. Fresh installations enable automatic lyric lookup/display and applicable timing checks; existing explicit Off choices are preserved.

Playback time and player state are used for subtitles, floating/fullscreen views, seeking, lyric editing, phrase audition and loops. LyricLayer does not record a history of page clicks, typed keys, scrolling, mouse movements or playback actions, monitor other sites' network traffic, or send usage analytics. Its own controls handle input to perform their function. Saving a phrase or tapping a lyric intentionally saves the resulting text/timestamp, rather than a log of the interaction.

## Requests to lyric providers

The default list enables LRCLIB, lrc.red, LyricsPlus, QQ Music, NetEase, Kugou, AMLL Community, Unison, Migu, JOOX, Lyrics.ovh, SongLyrics and Letras, with LRCLIB preferred. Sources and the preferred provider can be changed in Settings, including disabling all lyric providers. Explicit source choices are preserved; lists marked as defaults expand to the current defaults. An exact unmarked LRCLIB-only default from 0.8.0 can migrate to the newer defaults because that older version did not distinguish a default list from an explicit choice.

The preview's default search target is provider-supplied word timing. It can contact additional enabled sources after finding usable line timing, within request/time limits. Normal word searches can consult two enabled sources concurrently. **Find word timing** and **Find a better version** deliberately search enabled alternatives. Disabled sources are excluded from new searches. Changing a setting does not erase information already received by a provider. Library and preference edits are coordinated locally in the extension background; this adds no remote storage or new destination.

| Destination | Information sent | Purpose |
| --- | --- | --- |
| `https://lrclib.net` | Song query, title/artist and recording duration where supported; recording lookup parameters; a LyricLayer client/version header | Find recordings and retrieve lyrics/timing |
| `https://lyrics.kugou.com` | Song query and duration where supported; candidate identifier and provider-supplied access key | Find recordings and retrieve lyrics |
| `https://music.163.com` | Song query and candidate recording identifiers | Find recordings, lyrics and available timing/translation/pronunciation fields |
| `https://c.y.qq.com`, `https://u.y.qq.com` | Song query and candidate recording identifiers | Find QQ Music recordings and retrieve QRC word timing, line lyrics and supplied language layers |
| `https://lrc.red` | Song title/artist, optional album/duration, or manual query; candidate ISRC | Find recording metadata and retrieve TTML lyrics |
| `https://lyricsplus.prjktla.my.id` | Song title/artist and optional album/duration | Retrieve timing through the LyricsPlus aggregation service, which can query upstream providers |
| `https://unison.betterlyrics.org` | Song title/artist or manual query; submission identifier | Find and retrieve community TTML submissions and supplied contributor metadata |
| `https://c.musicapp.migu.cn`, `https://d.musicapp.migu.cn` | Song query and candidate lyric-file paths | Find Migu recordings and retrieve line timing |
| `https://cache.api.joox.com`, `https://api.joox.com` | Song query, candidate identifiers and fixed catalog language/region parameters | Find JOOX recordings and retrieve line timing |
| `https://api.amll.dev` | Song title/artist and candidate identifiers | Search the AMLL community catalog and retrieve TTML timing/language layers |
| `https://api.lyrics.ovh` | Song query and candidate artist/title | Search and retrieve untimed text from Lyrics.ovh's aggregation service |
| `https://www.songlyrics.com` | Song query and candidate page paths | Find and read untimed lyric pages |
| `https://solr.sscdn.co`, `https://www.letras.mus.br` | Song query and candidate page paths | Search Letras and read untimed lyric pages |

Search text comes from the player metadata or what you type. Searches can try cleaned titles, artist/title variants and an underlying song title for a live performance. Avoid including unrelated private information in a lyric search. The extension does not add a separate YouTube video ID or watch URL to lyric-provider requests; query text itself can identify what you are listening to or looking for.

Requests use HTTPS and omit cookies/credentials. Providers still receive ordinary network information, including IP addresses and request headers, and may retain their own logs. LyricLayer does not request GPS/device geolocation or control a provider's retention practices. There is no publisher proxy. Musixmatch and LyricFind are not connected and no paid lyric API is used.

Untimed fallback sources are skipped after a usable timed match unless you explicitly search all enabled sources. Source HTML and fixed JSONP responses are parsed as data, never executed; page scripts, ads, images and tracking resources are not loaded. Download URLs are restricted to approved provider origins and path shapes. Country/language parameters select a catalog response and are not derived from your device location.

**Prepare the next queued song on YouTube Music** is opt-in and off by default. If enabled, the available next song's title, artist and duration may be searched at your enabled sources before you play it. This uses a smaller bounded request budget and the same local response cache. It does not upload or prefetch song audio.

## Local provider-response cache

Provider query URLs and returned lyric/recording data, including fetched page text, are cached in local extension storage so they can survive background-worker restarts. Successful responses are reusable for up to six hours; supported empty/not-found responses have a one-minute reuse period. The cache is bounded to 48 entries and approximately 2 MiB of response data. Individual response bodies are also bounded to 2 MiB. Temporary provider retry/cooldown times are retained locally.

Expired responses are ignored for reuse. Eviction and pruning happen during subsequent cache activity; expiry is not a promise that bytes disappear from disk at that exact time. The cache is separate from deliberately saved songs, is not browser sync, and is not included in full Library backups. Removing a saved song does not independently clear past cached provider responses. Removing the extension clears its local storage.

## YouTube caption timing

When lyrics and automatic timing checks are enabled, LyricLayer can read loaded text tracks and request up to three eligible caption tracks from the current video's `https://www.youtube.com/api/timedtext` URLs. Caption requests use same-origin credentials where applicable, including the normal YouTube session on matching-origin requests. Availability differs by player/site, and caption data may be absent or inaccessible.

Caption responses are size-limited and kept temporarily in memory. Phrase matching runs locally. Raw captions are not sent to lyric providers, the publisher or an AI service. Successful delays and matched source-lyric timelines may be saved for that exact video. A caption match or a compatible catalog recording is not an independently verified audio alignment.

Disabling all lyric providers leaves saved/imported lyrics available and does not by itself disable caption checks. Use the separate automatic timing setting to control those checks.

## Local audio processing

There are five separate local audio-related features:

- **Check edits using local playback audio** can analyze eligible live/acoustic playback and normal music-video edits when suitable caption timing is unavailable. This setting is enabled by default on fresh installations and can be turned off. It processes already-played audio in bounded windows, with at most 12 windows of up to 30 seconds per video visit and one inference job at a time. Supplied words and explicit provider language metadata may be sent to the local worker alongside audio. Consistent evidence can apply and save a provisional global offset; later accepted conflicting evidence removes that estimate and saves a small conflict summary. Separate edit matching retains supported sections. These automatic changes require no review.
- **Audio timing lab · experimental** starts only when you press **Capture passage**. It samples about 20 seconds of normal-speed video playback and compares the model's observed words with the passage you selected. Matching lines can be opened as a Studio draft for review; active lyrics change only after you save that draft.
- **Karaoke** (Library > Practice, or K in Float and Stage) changes the video's sound only after you turn it on. Guide, No vocal and Max use the packaged Spleeter vocal model (Deezer, MIT licence) in a hidden LyricLayer frame inside the same YouTube tab. To prepare each moment before it plays, a small page-world script keeps a rolling copy of the audio YouTube has already downloaded in this tab (at most about 8 MB, never video) and hands it only to LyricLayer's karaoke when karaoke is on (and to the timing check below); the frame accepts it only after the background confirms the tab's own content script registered it. Separated audio stays in memory, the model is loaded only while it prepares the next half minute or so and released seconds after each burst, and nothing is uploaded or stored.
- **Timing from the singing** (on with "Check edits using local playback audio", under Automatic matching): to correct lyric timing for music videos with an intro or a different start, LyricLayer measures where the voice is in the audio YouTube has already downloaded in this tab (the same rolling copy and packaged vocal model as karaoke, in a hidden LyricLayer frame) and compares it with the lyric lines. Only per-moment voice levels are computed; no audio, voice levels or transcripts are stored or sent anywhere. The result (an offset and how well it matched) is saved with the video's lyrics like other automatic timing. The model is released seconds after each check.
- **Local audio assistance** in Studio reads an audio file you choose, up to 60 MB / 20 minutes, for a waveform and nearby energy-rise suggestions. File audio and its waveform stay in the current tab. This feature does not identify vocals or automatically align a song.

Video analysis uses the current video element's exposed audio stream and packaged Whisper Tiny weights in a local browser worker. It does not request a microphone, capture the screen, upload audio or download a remote model. The `offscreen` permission and packaged WebAssembly runtime support local recognition.

Raw audio samples and recognition transcripts are temporary memory, not extension-storage records or backup contents. Matching source lyric text, video-relative timestamps and a small match/provenance summary can be retained in saved timing or Studio drafts. Local audio files are not copied into extension storage or exported in library/project backups. Processing and drafts are guarded against song/recording changes; ads, navigation, Off and cancellation can stop work. The idle model is released. Recognition quality on singing and complete timing coverage are not guaranteed.

Turn off **Check edits using local playback audio** to stop the automatic audio fallback while retaining caption checks. Turn off **Check timing automatically** to stop both automatic types of checks. The explicit Audio timing lab remains a separate action; use its **Cancel** control to stop a requested capture. Turning lyrics off stops pending audio work. Previously saved timing is retained until changed or removed.

## Local library, drafts and practice data

Data is stored with `chrome.storage.local`, not browser sync. Different browser profiles and different extension identities have separate data.

| Local data | Contents and retention |
| --- | --- |
| Preferences | Display/appearance, sources, timing/search settings, optional prefetch choice and preference-version markers. Retained until changed or the extension is removed. |
| Saved songs | Video ID, selected source/recording, lyric text, rich timing/language layers, imported text, delay, repairs, performance matches, video-edit sections/anchors and update time. Automatic recent selections are trimmed to 80 disposable records; imports, manual choices/edits, pins and fixing items are protected from that trimming. Protected records have no automatic age expiry and remain subject to the browser's storage quota. |
| Library flags | Pin/protection state, fixing state and any fixing note for a saved video. |
| Studio drafts | Exact video identity, title/artist, edited lines and words, timing/language/voice layers, selected line, update time and optional provenance. Partial drafts persist until replaced or discarded. Undo/redo history itself stays in memory. |
| Saved practice phrases | Video ID, selected lyric text, optional translation/pronunciation, song title/artist, start/end times and update time. Retained until you remove the phrase. |

The fullscreen and floating views use the same lyrics and player state. Cloze answers, reveal/check actions, temporary playback loops and current listening position are not stored as an exercise-history log. Compact/Scrolling view preferences are saved; scrolling and key events are not logged. These views use local styles/fonts and add no remote service.

**Library → Remove** deletes the selected song's saved lyrics/timing and library flags after its confirmation click. **Forget this video** clears the current video's saved lyric selection/timing. Those actions do not remove independent Studio drafts or saved practice phrases: use **Discard draft** and **Remove phrase** for those. Removing the extension clears its local extension storage; this does not delete exported files or provider-held logs.

## Backups, exports and diagnostics

**Export full backup** creates a local JSON file containing validated saved songs, library flags, practice phrases, Studio drafts and preferences. It includes lyric text and video identities and may reveal your listening interests. It excludes the disposable provider cache, raw audio and recognition transcripts. Invalid records are reported as skipped. Restore keeps existing matching items by default; the explicit replacement option permits valid matching records to overwrite them. Invalid imported records do not delete their existing counterparts.

Studio project exports and Lyricsfile exports contain lyric text, timing and available extra layers. LRC exports contain the supported lyric/timestamp subset. Files are downloaded locally and are not uploaded automatically. You choose whether to share them, and they remain outside extension storage until deleted separately.

The optional diagnostic report contains the current video ID/title/duration, settings, provider recording identifiers, timing coverage and processing/error counts. It excludes lyric text, audio, recognition transcripts, cookies/credentials, current playback position, paused/playing state, playback speed and ad state. Review reports before sharing.

## Permissions and external links

Content scripts operate on desktop `www.youtube.com` and `music.youtube.com` to read song/player information and provide the interface. `storage` holds local data. `activeTab` supports toolbar controls for the current YouTube tab. `offscreen` supports the local model worker. Provider host permissions are limited to the lyric-service origins listed above. Preview 5 adds lrc.red, LyricsPlus and Unison; all use the same cookie-free, bounded search/cache pipeline. No microphone or geolocation permission is requested.

Genius lookup, source, help and store-review links open ordinary websites under their own privacy policies; the Genius lookup includes the current query. YouTube continues handling your playback through its own account/session and policies. This preview adds no remote executable code, publisher tracking, paid service or Cloudflare backend.

Diagnostic downloads additionally include bounded per-source search states, request counts and error summaries. Returned lyrics and captured audio are excluded.

## Chrome Web Store Limited Use

LyricLayer follows the Chrome Web Store User Data Policy and its Limited Use requirements. Data accessed by the extension is used only for the lyric search, display, synchronization, editing, saving and practice features described here. Transfers to enabled lyric providers are limited to the requests described in this policy. The publisher does not sell data, use it for advertising or profiling, or allow people to read it for unrelated purposes. Local audio and captions are not uploaded. Any diagnostic file you choose to share for support is shared only through your own explicit action; review it before sharing.

---

## Earlier releases (retained policies)

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
