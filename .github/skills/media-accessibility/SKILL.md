---
name: media-accessibility
description: Video/audio accessibility: WebVTT/SRT/TTML captions, audio descriptions, accessible media player ARIA, and WCAG 1.2.x compliance.
---

# Media Accessibility Skill

Reference data for video, audio, and streaming media accessibility. Used by `media-accessibility` agent and any web agent encountering `<video>` or `<audio>` elements.

---

## WCAG 1.2 Time-Based Media Criteria

| SC | Level | Requirement | Test |
|----|-------|-------------|------|
| 1.2.1 | A | Audio-only/video-only: provide text transcript or audio track | Transcript exists alongside media |
| 1.2.2 | A | Captions for prerecorded audio in video | Synchronized captions present |
| 1.2.3 | A | Audio description OR text alternative for prerecorded video | Description track or full transcript |
| 1.2.4 | AA | Captions for live audio in video | Real-time captioning active |
| 1.2.5 | AA | Audio description for prerecorded video | Description track present |
| 1.2.6 | AAA | Sign language for prerecorded audio | Sign-language interpretation provided |
| 1.2.7 | AAA | Extended audio description | Paused video for long descriptions |
| 1.2.8 | AAA | Media alternative for prerecorded video | Full text alternative document |
| 1.2.9 | AAA | Audio-only (live): text alternative | Real-time text transcript |

## Deaf and Sign-Language Access

- Treat captions and sign-language interpretation as distinct access modalities.
- WCAG 1.2.6 requires sign-language interpretation for prerecorded audio content in synchronized media at Level AAA.
- Use the sign language appropriate to the intended audience and content; do not assume ASL by default.
- Sign-language interpretation is additional Level AAA access and does not replace captions required at Levels A/AA.
- Require human review for linguistic accuracy, completeness, timing, register, and equivalence; do not infer quality from the mere presence of an interpreter window or alternate video.

## U.S. FCC Part 79 Crosswalk

When U.S. FCC jurisdiction is relevant, evaluate FCC obligations separately from WCAG conformance.

### Subpart A — Video Programming Owners, Providers, and Distributors

| Section | Title |
| --- | --- |
| § 79.1 | Closed captioning of televised video programming |
| § 79.2 | Accessibility of programming providing emergency information |
| § 79.3 | Audio description of video programming |
| § 79.4 | Closed captioning of video programming delivered using Internet protocol |

### Subpart B — Apparatus

| Section | Title |
| --- | --- |
| § 79.100 | Incorporation by reference |
| § 79.101 | Closed caption decoder requirements for analog television receivers |
| § 79.102 | Closed caption decoder requirements for digital television receivers and converter boxes |
| § 79.103 | Closed caption decoder and display requirements for apparatus |
| § 79.104 | Closed caption decoder requirements for recording devices |
| § 79.105 | Audio description and emergency information accessibility requirements for all apparatus |
| § 79.106 | Audio description and emergency information accessibility requirements for recording devices |
| § 79.107 | User interfaces provided by digital apparatus |
| § 79.108 | Video programming guides and menus provided by navigation devices |
| § 79.109 | Activating accessibility features |
| § 79.110 | Complaint procedures for user interfaces, menus and guides, and activating accessibility features on digital apparatus and navigation devices |

### FCC Caption Quality

For covered televised programming under § 79.1, evaluate **accuracy, synchronicity, completeness, and placement**. Do not treat a 99% accuracy heuristic as a fixed FCC legal threshold. FCC 14-12 discusses percentage accuracy as a captioning-vendor best-practice metric while expressly declining to adopt accuracy metrics as the Commission's caption-quality standard.

### Caption Settings and Activation

For covered contexts under § 79.103, review proximity, discoverability, previewability, and consistency/persistence of caption display settings. Where applicable, include usability testing with consumers and disability groups, remediation of discovered problems, employee training, OS-level caption settings, and APIs or similar methods.

Under § 79.109, review whether accessibility features can be activated through the required readily operable mechanism.

### Primary U.S. Sources

- FCC 14-12: <https://docs.fcc.gov/public/attachments/FCC-14-12A1_Rcd.pdf>
- FCC 24-79: <https://docs.fcc.gov/public/attachments/FCC-24-79A1.pdf>
- 2025 CFR Part 79: <https://www.govinfo.gov/content/pkg/CFR-2025-title47-vol4/pdf/CFR-2025-title47-vol4-part79.pdf>

## Caption File Formats

### WebVTT (Web Video Text Tracks)

```text
WEBVTT

00:00:01.000 --> 00:00:04.000
Welcome to the accessibility course.

00:00:04.500 --> 00:00:08.000
Today we'll cover caption best practices.

00:00:08.500 --> 00:00:12.000
<v Speaker 2>Let's start with file formats.
```

**Key rules:**

- File must start with `WEBVTT` header
- Timestamps: `HH:MM:SS.mmm --> HH:MM:SS.mmm`
- Speaker identification: `<v Speaker Name>Text`
- Maximum 2 lines per caption, 32 characters per line
- Minimum display time: 1 second
- Maximum display time: 7 seconds

### SRT (SubRip Text)

```text
1
00:00:01,000 --> 00:00:04,000
Welcome to the accessibility course.

2
00:00:04,500 --> 00:00:08.000
Today we'll cover caption best practices.
```

**Key rules:**

- Sequential numbering starting at 1
- Timestamps use comma for milliseconds (not period)
- Blank line between entries
- No styling support (unlike WebVTT)

### TTML (Timed Text Markup Language)

- XML-based, used in broadcast and streaming
- Supports styling, positioning, and region layout
- IMSC (Internet Media Subtitles and Captions) is the web profile

## Caption Quality Guidelines

These are quality-review considerations. Operational style targets must not be presented as universal WCAG pass/fail thresholds or fixed FCC legal thresholds.

| Metric | Guidance |
|--------|----------|
| Accuracy | Review for accurate, equivalent access; 99%+ may be an operational target or vendor metric, not a normative WCAG or fixed FCC threshold |
| Synchronization | Captions should coincide with corresponding speech and sounds; document any operational timing tolerance separately from WCAG/FCC conformance |
| Speaker identification | Identify speakers when needed to understand who is speaking |
| Sound effects | Describe meaningful non-speech audio, for example `[applause]` or `[phone rings]` |
| Music | Describe meaningful music and include lyrics when required for equivalent access |
| Caption rate | Use an audience-appropriate readable rate; document any numeric house style separately from conformance |
| Line length | Use readable line lengths appropriate to the delivery format; do not treat a house limit as a WCAG threshold |
| Lines per caption | Use readable grouping appropriate to the delivery format; do not treat a house limit as a WCAG threshold |
| Placement | Keep captions viewable and avoid obscuring important visual information |

## Audio Description

Audio description narrates visual information during pauses in dialogue.

**Requirements:**

- Describe: actions, scene changes, on-screen text, facial expressions relevant to plot
- Don't describe: obvious audio cues, subjective interpretations
- Timing: fit into natural pauses; for extended descriptions (1.2.7), video pauses automatically
- Voice: distinct from program audio, clear and neutral

**HTML implementation:**

```html
<video controls>
  <source src="video.mp4" type="video/mp4">
  <track kind="captions" src="captions-en.vtt" srclang="en" label="English" default>
  <track kind="descriptions" src="descriptions-en.vtt" srclang="en" label="English Audio Descriptions">
</video>
```

## Accessible Media Player ARIA Patterns

### Minimum Controls

Every media player must have keyboard-accessible controls for:

- Play/Pause (`role="button"`, `aria-label="Play"` / `aria-label="Pause"`)
- Volume (`role="slider"`, `aria-label="Volume"`, `aria-valuemin`, `aria-valuemax`, `aria-valuenow`)
- Seek/Progress (`role="slider"`, `aria-label="Seek"`, `aria-valuetext="2 minutes 30 seconds"`)
- Captions toggle (`role="button"`, `aria-pressed`, `aria-label="Toggle captions"`)
- Fullscreen (`role="button"`, `aria-label="Enter fullscreen"` / `aria-label="Exit fullscreen"`)

### Live Region Announcements

```html
<div aria-live="polite" class="sr-only" id="player-status">
  <!-- Announce: "Playing", "Paused", "Video ended", "Captions on", "Captions off" -->
</div>
```

### Keyboard Shortcuts (Media Player Convention)

| Key | Action |
|-----|--------|
| Space / Enter | Play/Pause |
| Left Arrow | Rewind 5 seconds |
| Right Arrow | Forward 5 seconds |
| Up Arrow | Volume up |
| Down Arrow | Volume down |
| M | Mute/Unmute |
| C | Toggle captions |
| F | Toggle fullscreen |

## Transcript Best Practices

- Provide a full-text transcript adjacent to or linked from the media
- Include speaker identification, timestamps (optional but helpful), and non-speech audio
- Transcripts benefit deaf users, search engines, and users who prefer reading
- Interactive transcripts (click a line to jump to that point) are excellent UX

## Live Captioning

- WCAG 1.2.4 (AA) requires captions for live audio in synchronized media
- Options: human captioner (CART), AI-powered auto-captioning, hybrid
- AI auto-captions can contain material errors; human review or correction is recommended, and any operational accuracy target must be kept separate from WCAG/FCC conformance claims
- WebSocket-based caption delivery for web: push text to a `<div aria-live="polite">` container

## Common Violations

| Issue | WCAG SC | Severity |
|-------|---------|----------|
| No captions on prerecorded video | 1.2.2 | Critical |
| Auto-generated captions without review | 1.2.2 | Serious |
| No audio description for visual-only content | 1.2.5 | Serious |
| Inaccessible media player controls | 2.1.1, 4.1.2 | Critical |
| No keyboard access to play/pause | 2.1.1 | Critical |
| Autoplay without user control | 1.4.2 | Serious |
| Volume slider not keyboard-operable | 2.1.1 | Serious |
| No transcript for audio-only content | 1.2.1 | Critical |
| Captions poorly synchronized | 1.2.2 | Moderate |
| Missing speaker identification in captions | 1.2.2 | Moderate |
