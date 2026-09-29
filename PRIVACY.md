# LyricLayer privacy policy

Last updated: 29 September 2026. Applies to LyricLayer version 0.5.1.

**Publisher:** raccooovl

**Privacy contact:** [LyricLayer GitHub issues](https://github.com/raccooovl/lyriclayer/issues). Issues are public; do not include passwords, private account information or other sensitive personal information.

**Policy location:** [LyricLayer privacy policy](https://github.com/raccooovl/lyriclayer/blob/main/PRIVACY.md)

## What this policy covers

LyricLayer is a Microsoft Edge extension that displays timed song lyrics on desktop YouTube watch pages. This policy describes the extension's handling of information. YouTube, Microsoft Edge, lyric services and any websites you open have their own data practices.

## Information used on your device

On a YouTube watch page, LyricLayer reads the current video's identifier, public title and channel/author name. It reads playback position, duration, playback state and whether the player is showing an advertisement to match and display lyrics. These playback values are used locally; video duration can also be included in lyric searches as described below. LyricLayer does not capture or upload the song's audio or video.

When you open the extension popup, it checks the active tab's URL to determine whether it is a supported YouTube watch page and to control that tab. It does not read your browser's full browsing-history database.

The extension also uses the text you enter in its search, lyric import, translation and timing controls. A file is read only after you choose it in the import control. Imported text and line timings are processed locally; the extension does not upload those documents to a server.

## Information sent to lyric services

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

## Translations and word timing

Original lyrics are displayed by default. A provider response can include translation or word-timing data even when the display option is off. That data may be kept with the selected recording locally. Turning translation display off hides the second line; it does not prevent the provider from returning translation data with a lyric request.

A translated LRC you import is saved locally with that video's selected lyrics. LyricLayer does not send it to a translation service or generate a translation.

## Local storage and retention

LyricLayer uses Microsoft Edge's local extension storage, not its sync storage, for:

- Display, position, translation, word-highlighting, transition and automatic-search preferences, including whether lyrics are shown.
- Saved selections for up to 40 videos, identified by YouTube video ID. Each saved entry can include recording metadata, source identifiers, lyrics, source translations and word timing, imported lyrics or translation, your timing delay, whether the recording was automatically selected, and an update timestamp.

When a saved entry is written, older saved video entries are removed so the 40 most recently updated entries remain. Entries do not otherwise have a time-based expiry. Preferences remain until changed or extension data is removed. These saved IDs and selections are a local record of videos for which lyrics were saved.

Recent lyric API responses are also cached temporarily in the extension's background memory, for reuse for up to 15 minutes. The cache is limited to 48 entries and an estimated 4 MiB. It is not a persistent lyric-history database and is lost when that background context is discarded. Expired responses are not reused, although an expired entry can remain in memory until it is accessed, evicted or the context ends.

If you use Export LRC, the browser saves a text file to your chosen download location. Its filename includes the YouTube video ID. Exported files are outside the extension's local storage and remain until you delete them yourself.

## Your controls

- **Forget this video** removes that video's saved lyrics and timing entry. It does not erase preferences, other saved videos, exported files or provider-side logs.
- **Use source translation** removes an imported translation from the saved selection and returns to a source translation when one exists.
- **Show source translation underneath** controls translation display. Original-only display is the default.
- Disable **Find lyrics automatically on new videos** to stop future automatic new-video lookups. Opening lyric settings or pressing Find can still start a lookup. Changing this preference does not cancel requests already underway.
- The **Lyrics** button controls the overlay. Hiding lyrics alone does not turn off the separate automatic-search preference.
- Disable or remove LyricLayer through Microsoft Edge's extension management to stop the extension running. Removing it also removes its local extension storage. Downloaded LRC files must be deleted separately.

Saved lyrics can be viewed when you revisit their video, and the selected original line lyrics can be exported as LRC. The extension has no bulk history viewer, full-data export or dedicated clear-all button. For questions about information handled by the publisher, use the privacy contact above; information already sent to independent lyric services is subject to those services' controls.

## Links you choose to open

**Find lyrics on Genius** opens a normal Genius search page with the current song query. It does not fetch or scrape Genius lyrics inside the extension. Source links open the service's website. These sites can receive normal navigation information and use their own cookies or accounts under their policies. Omitting credentials on lyric API requests does not apply to a website you open normally.

## Other uses and policy changes

The extension contains no analytics, advertising, payment or account system, and does not sell information or use it for credit decisions. Its information handling supports lyric search, display, customization and local saving. It does not request passwords, financial information, health information or precise device location.

This policy will be updated when the extension's data practices change. The last-updated date above identifies the policy version. Contact the publisher using the privacy contact at the top of this page. GitHub handles visits and public issue submissions under its own policies.

## Interaction handling

LyricLayer uses the current media playback position transiently to choose the lyric line to display and to create timing adjustments you request. Its controls respond locally to clicks, keyboard commands and subtitle dragging. It saves the resulting lyric choices, timing edits, subtitle position and other preferences; it does not keep an interaction history, clickstream, keystroke or scroll log, pointer trail, or a record of network traffic. Playback positions and control events are not sent to the publisher or lyric services.

Saved video identifiers remain a local browsing-related record, lyric metadata and text remain website content, and online lyric services receive normal connection information including IP addresses. These practices remain disclosed even though ordinary local controls are not classified as collection of behavioral activity.
