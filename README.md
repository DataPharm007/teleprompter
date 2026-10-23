# Teleprompter

A voice-activated teleprompter that **records with your own phone or tablet camera** and
runs entirely in the browser. No build step, no dependencies, no server — a single static
`index.html` (plus a small web-app manifest). Your script and your footage stay on your
device. The one exception is Google Drive, which you connect only if you want to.

Live at: `https://datapharm007.github.io/teleprompter/`

## Film and read on the same device

Turn the camera on and the live view sits **behind your script**, so you read straight down
the lens while the words float on the glass. Hit **Record** and the camera captures a clean
take — the teleprompter text is only on your screen, never burned into the video.

- **Front or back camera**, with a one-tap flip, plus a camera picker for external/USB cams.
- **One-tap take** — Record runs the lead-in countdown, then rolls the camera and the scroll
  together. Stop ends both. (Turn this off in settings to drive recording and scroll
  separately.)
- **Quality** up to 720p / 1080p / 4K where the device supports it.
- **Readability scrim** behind the text, adjustable, so words stay legible over any backdrop.
- **Framing grid** (rule of thirds) to line up your shot.
- **Mirror preview** shows you a natural selfie view while the recording stays correct.
- **Live mic meter** so you can see audio is being captured.
- **Review, then keep or bin** — play the take back, then **Save** (on desktop, a location
  picker so you can write straight to an **external SSD/USB drive** or any folder), **Share /
  Save to Photos** (phones — into your camera roll, or Save to Files to reach a plugged-in
  drive), **Save to Drive**, or **Discard**. Files are named from your script title and date.

> Recording uses the browser's `MediaRecorder`. On iPhone/iPad use **Safari**; on Android use
> **Chrome**. The page tells you if a browser can't record. Output is `.mp4` where supported,
> otherwise `.webm`.

## Load scripts from Google Drive — no setup

**Open from Google Drive** with zero sign-in and zero keys: on iPhone/iPad the button opens
the **Files** app, where **Google Drive** appears as a location (the Drive app registers as a
document provider). Pick your script there — `.txt`, `.md`, `.docx`, `.rtf`, `.html`, or a
Google Doc saved/downloaded as text — and it loads. On a computer, install **Drive for
Desktop** and Drive shows up in the file dialog the same way.

> **Why no OAuth here?** Google does not allow a web page to read your private Drive files
> without an authorized token — there's no keyless *programmatic* route. The OS file picker
> sidesteps that entirely: *you* hand the file to the app through the system, so nothing needs
> to sign in. It's the simplest path and it's the default.

**Optional — browse and save inside the app.** If you'd rather pick files in an in-app Google
Picker, save scripts back to Drive, or upload finished takes to Drive, that uses the Google
Drive API and needs a free, one-time key. It's tucked under the Drive buttons and is handy on
desktop. See [Setting up Google Drive (optional)](#setting-up-google-drive-optional).

## Voice activation

Turn on the microphone and just start reading. The script follows your speech, keeping the
line you are speaking on the eye line, and holds still when you pause to think. Words you've
already said dim behind you. Three modes: follow my speech, commands only, or both.

Voice commands: *start / go / resume*, *stop / pause*, *faster*, *slower*, *bigger*,
*smaller*, *back to the top*, *mirror*.

> Voice tracking uses the Web Speech API. It works in **Chrome/Edge** (desktop and Android)
> **and Safari on iOS 14.5+ / macOS**. Safari stops listening after each phrase, so the app
> restarts it automatically — brief pauses are normal, and continuous mode is less reliable
> than on Chrome. Two iOS notes: voice may be disabled inside a home-screen-installed app (open
> it in a normal Safari tab if so), and the microphone can serve *either* voice tracking *or*
> the camera's audio recording, not both at once — for a voice-driven take, turn off "Record
> audio with the video" and capture sound separately. The page detects your browser and says so.

## Script input

Upload `.txt`, `.md`, `.html`, `.rtf`, `.srt`, `.vtt` or `.docx`; load from Google Drive;
drag and drop a file anywhere on the page; paste from the clipboard; or type directly in the
built-in editor, which updates the prompter live while it scrolls. Word files are parsed in
the browser with no external library. Scripts can be saved to a named library, saved to
Drive, and exported back out as `.txt`.

## Display

Text size, line height, letter spacing, font family, bold, all-caps, alignment
(left / center / right / justified), text-column width, side padding, background and text
colors with eight presets, horizontal and vertical mirroring for beam-splitter rigs,
adjustable eye-line position, and edge fade masks.

## Scrolling

The script holds still by default and you drive it: arrow keys, PgUp/PgDn, a clicker, the
wheel or a drag. Tick *Auto-scroll* for a constant speed, or turn on voice tracking, and the
status bar shows which of the three is in charge. Adjustable speed with a live words-per-minute
estimate, lead-in countdown before the first line, hold countdown after the last one, optional
beeps, loop mode, elapsed / remaining / estimated run time, and a progress bar.

## Markup

A line beginning with `#` becomes a section heading and appears in the "Jump to…" menu. A line
reading `[pause]` stops the scroll at that point until you resume.

## Install it like an app

The page ships a web manifest, so you can **Add to Home Screen** on iPad/iPhone (Safari share
sheet) or **Install** on Android/desktop Chrome. It then runs full-screen with no browser
chrome — the best way to film on a tablet.

## Also

Screen wake lock so a phone or tablet doesn't sleep mid-take, a synced second-screen window
for camera setups, fullscreen, a zen mode that hides every control, and mouse-wheel or
touch-drag scrubbing. All settings and the current script persist between sessions.

## Keyboard and remotes

| Key | Action |
| --- | --- |
| `Space` | play / pause |
| `↑` `↓` | scroll speed |
| `PgUp` `PgDn` | jump a screen |
| `←` `→` | nudge a line |
| `+` `−` | text size |
| `C` | camera on / off |
| `G` | start / stop recording |
| `M` | mirror |
| `V` | voice |
| `F` | fullscreen |
| `E` | edit |
| `S` | settings |
| `Z` | hide all controls |
| `R` / `Home` | back to top |
| `Esc` | close / exit |

Most Bluetooth presenter clickers send `PgUp` / `PgDn` or arrow keys, so they work as remotes
with no setup — handy for driving the scroll while you record.

## Setting up Google Drive (optional)

This is only for the **in-app** Picker, saving scripts to Drive, and uploading takes to Drive.
To just *open* a script from Drive you don't need any of this — use **Open from Google Drive**,
which goes through the OS file picker. For the in-app API path, do this once:

1. Open the [Google Cloud Console](https://console.cloud.google.com/), create a project, and
   enable the **Google Drive API** and the **Google Picker API**.
2. Under **APIs & Services → OAuth consent screen**, configure the consent screen (External is
   fine) and add your Google account as a test user.
3. Under **APIs & Services → Credentials**, create:
   - an **API key**, and
   - an **OAuth 2.0 Client ID** (application type: **Web application**). In its *Authorized
     JavaScript origins*, add the exact address the page is served from — for this build that
     is `https://datapharm007.github.io` (the setup card inside the app also shows you the
     exact origin to paste).
4. In the teleprompter, open **Settings → Script → Load from Drive** (or the *one-time setup*
   link) and paste the **Client ID** and **API key**. They're stored only on this device
   (`localStorage`) and used only to talk to Google.

The app requests the minimal **`drive.file`** scope, so it can only ever touch files you pick
with the Picker or that it creates — never your whole Drive.

**To bake the keys into the build** (so Drive works with no per-device setup), fill
`DRIVE_CONFIG` near the top of the script in `index.html`:

```js
var DRIVE_CONFIG = { clientId:'…apps.googleusercontent.com', apiKey:'AIza…' };
```

A per-device key pasted in the setup card always overrides the baked-in one.

## Privacy

Your script and your recordings never leave the device — recording happens locally and files
save to your own storage. The **only** time anything is sent off-device is when you explicitly
use **Google Drive** (your files go to your own Google account) or the system **Share** sheet
(you choose where). Nothing is sent to us or to any third party; there is no server.

## Browser support

| Feature | Chrome / Edge (desktop, Android) | Safari (iPhone / iPad / Mac) |
| --- | --- | --- |
| Prompter, display, scrolling, files | ✅ | ✅ |
| Camera preview + recording | ✅ | ✅ (iOS 14.3+) |
| Voice activation | ✅ | ✅ (iOS 14.5+; flakier, restarts itself) |
| Open from Drive (OS picker, no setup) | ✅ (with Drive for Desktop) | ✅ |
| In-app Drive Picker / save (optional key) | ✅ | ✅ |
| Save to external drive | ✅ (location picker) | ✅ (Share → Save to Files) |
| Install to home screen | ✅ | ✅ (Add to Home Screen) |

**Serve it over https or localhost.** The camera, voice, and Drive all require a secure
context. GitHub Pages provides this; so does `python3 -m http.server` opened via
`http://localhost:8000/teleprompter/`. Opened as a bare `file://` path, the camera, voice, and
Drive are disabled and the page says so — everything else still works.
