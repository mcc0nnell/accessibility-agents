# media-accessibility — Media Accessibility Specialist

> Audits video, audio, and streaming media for accessibility. Covers captions (WebVTT, SRT, TTML), audio descriptions, transcripts, accessible media player controls, live captioning, sign-language interpretation, and WCAG 1.2.x time-based media criteria.

## Features

- Audits prerecorded video for synchronized captions (WCAG 1.2.2)
- Checks live media for real-time captions (WCAG 1.2.4)
- Validates audio description availability for video content (WCAG 1.2.3, 1.2.5)
- Reviews transcript availability for audio-only and video content (WCAG 1.2.1)
- Audits sign-language interpretation for prerecorded synchronized media when Level AAA is in scope (WCAG 1.2.6)
- Covers extended audio description, media alternatives, and live audio-only alternatives (WCAG 1.2.7–1.2.9)
- Audits media player controls for keyboard accessibility and ARIA patterns
- Validates caption file syntax and quality (WebVTT, SRT, TTML formats)
- Checks caption timing, accuracy, completeness, placement, and speaker identification
- Cross-checks applicable U.S. video-programming and apparatus requirements against FCC 47 CFR Part 79

## When to Use It

- Adding video or audio content to a web page
- Reviewing captions for accuracy, timing, formatting, completeness, and placement
- Checking media player controls for keyboard and screen reader accessibility
- Ensuring audio descriptions are available for visual-only information in videos
- Auditing live streaming for real-time captioning support
- Reviewing Level AAA sign-language or other time-based-media requirements
- Reviewing U.S. media experiences where FCC Part 79 may apply

## How It Works

1. **Media inventory** - Finds all `<video>`, `<audio>`, and embedded media on the page
2. **Caption audit** - Checks for `<track kind="captions">`, validates caption file syntax, and reviews quality
3. **Audio description audit** - Verifies audio descriptions exist for video content with visual-only information
4. **Transcript audit** - Checks for linked or adjacent transcripts for all media
5. **Player controls audit** - Reviews media player for keyboard operation, ARIA labels, and focus management
6. **Live media check** - Validates real-time captioning integration for live streams
7. **Sign-language audit** - Distinguishes WCAG 1.2.6 sign-language interpretation from caption requirements and checks the appropriate sign language for the audience/content
8. **AAA media audit** - Reviews 1.2.7–1.2.9 when Level AAA is in scope
9. **FCC Part 79 cross-check** - When U.S. regulatory scope applies, reviews §§ 79.1–79.4 and §§ 79.100–79.110 without conflating FCC obligations with WCAG conformance

## Standards Notes

- Captions and sign-language interpretation are distinct access modalities. WCAG 1.2.6 adds Level AAA sign-language access; it does not replace caption requirements at Levels A/AA.
- The appropriate sign language depends on the intended audience and content. The specialist does not assume ASL by default.
- Human review is required for sign-language linguistic accuracy, completeness, timing, register, and equivalence.
- A numeric caption target such as 99% can be useful operationally, but it is not a normative WCAG conformance threshold or a fixed FCC legal test.
- Under FCC § 79.1, covered televised captioning is evaluated using accuracy, synchronicity, completeness, and placement.
- FCC regulatory applicability and WCAG conformance are reported separately.

## Handoffs

| Direction | Agent | When |
|-----------|-------|------|
| Receives from | accessibility-lead | When media elements are detected during a web audit |
| Hands off to | accessibility-lead | When media review is complete and a full web audit is needed |
| Hands off to | aria-specialist | When media player ARIA patterns need deeper review |

## Sample Usage

```text
@media-accessibility Audit video captions and player controls on our course page

@media-accessibility Check if our podcast page has transcripts for all episodes

@media-accessibility Review audio description availability for our product demo videos

@media-accessibility Review this prerecorded program for WCAG 1.2.6 sign-language access

@media-accessibility Cross-check this U.S. video experience against FCC Part 79
```

## Related

- [accessibility-lead](accessibility-lead.md) - Coordinates full web accessibility audits
- [aria-specialist](aria-specialist.md) - ARIA patterns for custom media player controls
- [keyboard-navigator](keyboard-navigator.md) - Keyboard interaction for media player controls
- [live-region-controller](live-region-controller.md) - Live region announcements for media state changes
