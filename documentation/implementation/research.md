# Implementation Research

## Decisions

- **Story generation:** Owner-authored scripts only. No runtime LLM/API, so story-generation token usage is zero. A repository agent and skill may guide implementation, but neither is part of the production pipeline.
- **Story input:** Keep each story in `stories/<slug>/`, with separately authored `short.md` and `long.md` files. Either file can be rendered independently; a `both` request requires both. Use a deliberately small Markdown subset (`# Title`, `## Scene heading`, plain-text paragraphs) so input stays readable and validation needs no general-purpose parser or extra dependency. Do not derive one version from the other.
- **Narration:** Use a local TTS engine/voice only after a sample passes quality and license review. No paid hosted fallback without owner approval. The TTS candidate is intentionally left for the first implementation spike because voice-model licenses may differ from the engine license.
- **Rendering:** Use FFmpeg/ffprobe as command-line tools rather than adding a video framework. Verify the selected binary build's license options before packaging it.
- **Publishing:** Use the official YouTube Data API OAuth upload flow after explicit per-video owner approval. Test privately first.
- **State and output:** Local JSON/files; no database, web app, cloud service, custom agent, or skill.

## Evidence and Alternatives

- The [Piper TTS repository](https://github.com/OHF-Voice/piper1-gpl) describes a local TTS engine and identifies its code as GPL-3.0. Voice models have their own licensing; the engine license alone does not clear a voice for the intended use. Select and record a specific English voice license before use.
- [FFmpeg licensing guidance](https://ffmpeg.org/legal.html) notes that licensing depends on enabled components/build options. Use a known build and preserve applicable notices.
- Google's [YouTube video upload guide](https://developers.google.com/youtube/data/guides/uploading_a_video) documents Python client libraries, OAuth desktop credentials, and upload privacy settings.
- YouTube's [scheduled publishing guide](https://support.google.com/youtube/answer/1270709?hl=en) supports scheduling a private video to go public at a selected date/time.

**Alternatives considered:** Hosted TTS or LLM generation can add service cost, token use, and terms/privacy concerns. Owner-recorded narration is a fallback if no suitable local voice is cleared, but is less automated. A web app, database, agent framework, or runtime agent/skill integration adds scope without helping the MVP; a small development-time agent and skill are documented separately to help execute the plan.
