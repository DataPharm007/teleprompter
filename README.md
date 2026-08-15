# Teleprompter

A voice-activated teleprompter that runs entirely in the browser. No build step, no
dependencies, no server — a single static `index.html`. Nothing you type or upload
ever leaves your device.

Live at: `https://datapharm007.github.io/teleprompter/`

## Features

**Voice activation** — turn on the microphone and just start reading. The script follows
your speech, keeping the line you are speaking on the eye line, and holds still when you
pause to think. Words you've already said dim behind you. Three modes: follow my speech,
commands only, or both.

Voice commands: *start / go / resume*, *stop / pause*, *faster*, *slower*, *bigger*,
*smaller*, *back to the top*, *mirror*.

**Script input** — upload `.txt`, `.md`, `.html`, `.rtf`, `.srt`, `.vtt` or `.docx`;
drag and drop a file anywhere on the page; paste from the clipboard; or type directly in
the built-in editor, which updates the prompter live while it scrolls. Word files are
parsed in the browser with no external library. Scripts can be saved to a named library
and exported back out as `.txt`.

**Display** — text size, line height, letter spacing, font family, bold, all-caps,
alignment (left / centre / right / justified), text-column width, side padding,
background and text colours with eight presets, horizontal and vertical mirroring for
beam-splitter rigs, adjustable eye-line position, and edge fade masks.

**Scrolling** — the script holds still by default and you drive it: arrow keys,
PgUp/PgDn, a clicker, the wheel or a drag. Tick *Auto-scroll* for a constant speed, or
turn on voice tracking, and the status bar shows which of the three is in charge.
Adjustable speed with a live words-per-minute estimate, lead-in countdown before the
first line, hold countdown after the last one, optional beeps, loop mode, elapsed /
remaining / estimated run time, and a progress bar.

**Markup** — a line beginning with `#` becomes a section heading and appears in the
"Jump to…" menu. A line reading `[pause]` stops the scroll at that point until you
resume.

**Also** — screen wake lock so a phone or tablet doesn't sleep mid-take, a synced
second-screen window for camera setups, fullscreen, a zen mode that hides every control,
and mouse-wheel or touch-drag scrubbing. All settings and the current script persist
between sessions.

## Keyboard and remotes

| Key | Action |
| --- | --- |
| `Space` | play / pause |
| `↑` `↓` | scroll speed |
| `PgUp` `PgDn` | jump a screen |
| `←` `→` | nudge a line |
| `+` `−` | text size |
| `M` | mirror |
| `V` | voice |
| `F` | fullscreen |
| `E` | edit |
| `S` | settings |
| `Z` | hide all controls |
| `R` / `Home` | back to top |
| `Esc` | close / exit |

Most Bluetooth presenter clickers send `PgUp` / `PgDn` or arrow keys, so they work as
remotes with no setup.

## Browser support

Everything works in any current browser. Voice activation uses the Web Speech API, which
means Chrome or Edge (desktop and Android); the page detects this and says so instead of
failing silently.

**Serve it over https or localhost if you want voice.** Chrome cannot remember a
microphone grant for a page opened as a `file://` path, so it re-asks every time
listening restarts — which, during a take, is constantly. GitHub Pages solves this; so
does `python3 -m http.server` and opening `http://localhost:8000/teleprompter/`. The
page detects the situation and says so. Everything except voice works fine from a file.
