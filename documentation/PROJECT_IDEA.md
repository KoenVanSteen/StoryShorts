# Project Idea - StoryShorts

## 1. Overview

- **Working name:** StoryShorts
- **Concept name (working):** The Unsent Archive
- **Description:** An English-language YouTube story channel featuring original fiction presented as recovered messages, notes, voice memos, and other fictional artifacts. Each story centers on a consequential choice and ends with a reveal or a question for the audience.
- **Status:** Concept / validation

## 2. Problem and Opportunity

- The owner wants to build a YouTube story channel without spending the time required to write, produce, and publish every video entirely by hand alongside a day job.
- Reddit readings and reused streamer/game clips depend on other people's work and carry rights and monetization risks. Original fiction can give the channel its own identity and a more direct path to distinctive storytelling.
- The owner hopes the channel could become a second income, but audience demand and earnings are unproven. Validate the concept with a small pilot before investing substantial time.
- Existing hardware is covered. Avoid new subscriptions or other spending unless the owner approves it.

## 3. Goals and Outcomes

- **Primary outcome:** Establish a recognizable story format based on original, English-language fiction.
- **Production outcome:** The owner writes the stories; a repeatable, locally run workflow automates narration, captions, video rendering, and upload preparation without turning episodes into interchangeable templates.
- **Initial channel:** StoryShorts. Focus on this one channel; streamer clips and GTA VI are deferred.
- **Publishing ambition:** Work toward one release per day, starting with a pilot cadence that can be sustained without sacrificing story quality.
- **Budget:** No new subscriptions or spending without the owner's approval.
- **Approval:** The owner reviews and approves every video before upload or scheduling. Consult the owner when rights or costs are unclear.

## 4. Proposed Solution

### Channel concept: The Unsent Archive (working title)

An imagined archivist opens a fictional archive of things people almost sent: a voicemail never delivered, a note tucked into a library book, a message saved as a draft, or a receipt that reveals a hidden choice. Each episode follows an original character facing a human dilemma. The artifact is the entry point, not the whole story; a later detail changes how the audience understands the choice.

- **Promise to viewers:** A compact, emotionally engaging original story with a reveal worth reconsidering.
- **Distinctive device:** Stories unfold through original fictional artifacts, narration, and scene-specific visuals. A recurring archivist gives the channel a recognizable frame, while characters, situations, genres, and endings vary substantially from episode to episode.
- **Signature framing:** Each episode opens with an artifact marked "UNSENT" and ends with the archivist filing it under a changing label such as "Sent," "Returned," or "Still Unanswered." The labels can evolve with the story rather than forcing every ending into the same pattern.
- **Shorts:** Around 60 seconds. Open on an artifact or urgent line, establish the character and dilemma, reveal a meaningful turn, and end with a thought-provoking question. Each Short should work as a complete story.
- **Long-form:** Around 10-20 minutes. Tell a fuller original story with developed characters, motivation, complications, and consequences. Do not pad a Short or simply stitch several Shorts together.
- **Paired scripts:** Store each story in its own folder with `short.md` and/or `long.md`. The owner writes each version separately; the app can render either or both as separate videos and never auto-shorten or pad one into the other.
- **Markdown convention:** Use `# Title`, `## Scene heading`, and plain-text paragraphs. Scene headings guide the artifact visuals and narration segments. Keep the supported Markdown subset intentionally small.
- **Visual and audio identity:** Create original or properly licensed document/scene visuals, captions, sound cues, and narration. Avoid relying on unrelated gameplay footage as the main creative element. Clearly label fiction as fiction.
- **Story creation:** The owner writes original stories from scratch in Markdown. The MVP does not call an LLM to generate scripts, reducing token use and avoiding a story-generation service cost. The automation starts from the finished `short.md` and/or `long.md` files.
- **Production workflow:** Add a story folder with one or both Markdown versions -> validate and render each selected version -> review the complete video -> owner approves -> upload and optionally schedule -> record outcome.
- **Release approach:** Batch production can reduce daily workload, but publish only after each video is individually reviewed. Build toward daily releases only if quality and workload remain sustainable.

### Illustrative pilot story seeds

These are starting points to develop into original scripts, not finished stories:

- **Short - "The Voice Note Set to Send":** On moving day, a woman finds a scheduled voice note to her estranged brother. A reply saved beside it changes what she thinks she needs to say.
- **Short - "Two Copies of the Same Receipt":** Two strangers bring the same old dinner receipt to the archive, each convinced it records a different promise.
- **Long - "Room 12":** A hotel cleaner finds a bundle of letters addressed to guests who never checked in and must decide whether to deliver the final one before the building closes.

## 5. Scope

### In scope

- One English-language YouTube story channel, starting with the existing StoryShorts channel.
- Original fictional stories written for the channel, in roughly 60-second Shorts and 10-20-minute long-form episodes.
- One folder per story with separate `short.md` and `long.md` scripts; either version can be rendered independently, and both can be supplied for a story.
- A recognizable archive/artifact framing with varied stories and meaningful original narration, writing, and editing.
- A manually invoked command-line production workflow, Dockerized where practical.
- Free/local tools and batch production where practical; manual owner approval before every upload or scheduled release.
- Rights tracking for any third-party music, images, fonts, sound effects, or other assets used in a video.

### Out of scope

- Streamer clips and GTA VI content for this phase.
- Reading or lightly rewriting Reddit posts as the main content format; scraping posts or treating public availability as permission.
- Publishing real people's stories or audience submissions without appropriate permission and privacy safeguards.
- Unapproved subscriptions or costs, or rotating accounts to bypass free-tier limits.
- Fully autonomous publishing without owner review.

### Possible future work

- Invite audience-submitted story prompts or stories under clear submission and permission terms.
- Build a larger fictional world with recurring characters or connected episodes if viewers respond to the pilot.
- Add other formats or channels only after validating the story channel and reviewing rights.
- Consider paid tools only if the owner explicitly approves the cost.

## 6. Requirements and Acceptance

### Functional requirements

- [ ] Story text is written by the owner; the MVP does not use an LLM to generate or expand scripts.
- [ ] The app reads stories from `stories/<slug>/` in Markdown, using `short.md` for a Short and `long.md` for long-form.
- [ ] A story may contain either or both versions; when both exist, each is rendered as its own video from its own script. The app does not automatically summarize or pad between versions.
- [ ] A story can be prepared as an approximately 60-second vertical Short or a 10-20-minute landscape video, with current YouTube specifications verified before implementation.
- [ ] Each story has an original, owner-authored script with a distinct character, dilemma, development, and resolution or reveal.
- [ ] Each episode uses the archive/artifact frame while varying its substantive story and scene-specific creative elements; the frame is not a substitute for original story content.
- [ ] Each video includes captions and narration, using a local/free narration option whose terms allow the intended use.
- [ ] Third-party assets have a recorded source and license/permission status. Assets with unclear rights are excluded until cleared.
- [ ] Each finished video is presented for owner review and approval before upload or scheduling.
- [ ] The manually started workflow reports whether production completed, needs approval, or failed.
- [ ] Before using a service or step that may incur a cost, the workflow pauses and asks the owner.

### Quality requirements

- [ ] No paid subscription, service, or infrastructure is required unless the owner approves it first.
- [ ] The CLI uses concise status/error output and makes no story-generation LLM calls.
- [ ] Reusable production steps do not result in interchangeable scripts or minimally varied videos.
- [ ] Captions are readable and synchronized; narration is intelligible and matched to the final script.
- [ ] A failed or paused run is not reported as a successful upload.
- [ ] Credentials and private account data are not exposed in logs or project files.
- [ ] Free-tier quotas are used according to the provider's terms; the workflow does not rely on account rotation to bypass them.

### Acceptance criteria

- [ ] Produce a small pilot set of original Shorts and at least one original long-form story using the proposed concept.
- [ ] Every pilot script and final video is reviewed by the owner before publication.
- [ ] No unlicensed third-party story, music, footage, or image is included in a published pilot.
- [ ] The owner can distinguish a completed, failed, and approval-pending production run.
- [ ] Videos can be batch-prepared and, after individual approval, scheduled for chosen release times.
- [ ] The pilot uses existing hardware and no new subscription or unapproved spending.

## 7. Experience and Content

- **Tone:** Human, emotionally grounded, and intriguing; do not present fictional stories as true events.
- **Story rhythm:** Artifact/hook -> character and context -> difficult choice -> consequence or recontextualizing reveal -> optional audience question.
- **Variation:** Rotate genres and emotional stakes (for example, mystery, bittersweet drama, suspense, or hopeful resolution) so the series has a signature without making episodes feel templated.
- **Shorts:** Around 60 seconds, vertical 9:16; each is a complete story rather than a context-free teaser.
- **Long-form:** Around 10-20 minutes, landscape 16:9; allow room for character motivation and consequences instead of padding shorter material.
- **Story files:** Put each story under `stories/<slug>/`. Use `short.md` for its Short script and `long.md` for its long-form script. Each file starts with `# Title`; `## Scene heading` sections divide narration/artifact scenes; paragraphs contain owner-written text. The files are independent and may be rendered separately or together.
- **Visual identity:** Original animated/illustrated artifacts, typography, and scene-specific visuals. Use original or properly licensed assets; no gameplay footage as a default background.
- **Audio:** Narration and captions are desired. Exact narrator voice, sound palette, and caption style remain open. Use a free tool only if its terms permit the intended use; do not evade free-tier limits.
- **Production UI:** A manually started command-line app, Dockerized where practical. The CLI should expose script/video previews, production status, asset-rights notes, per-video approval, and upload/scheduling results.

## 8. Data and Integrations

- Inputs are owner-created story folders containing `short.md` and/or `long.md`, channel settings, and any properly licensed production assets. Outputs include narrated/captioned videos for each supplied version, publishing metadata, and upload/schedule status.
- Original stories should be created for the channel, not copied or lightly rewritten from Reddit or other people's work. Reddit and streamer content are not sources for this phase.
- If audience submissions are added later, obtain clear permission for adaptation, publication, and any intended monetization before using them; handle personal or sensitive details carefully.
- Track the source and license/permission for every third-party music, image, font, sound effect, or other asset. Prefer original assets or licenses that explicitly cover the intended YouTube and commercial use.
- YouTube publishing and scheduling are desired integrations. Choose an upload method only after verifying current terms, costs, and account requirements.
- Retain only needed scripts, project files, and outputs, and delete them when no longer required.
- If an integration is unavailable or returns unexpected results, stop that run, report the issue, and do not claim publication succeeded.

## 9. Technical Context

- Build a manually invoked command-line app; Dockerize it where practical. The owner is a software engineer, so the solution can assume technical familiarity.
- The repository currently contains this project-idea document but no application code or technical design. Host operating system, language, and framework are still open.
- Use automation for repetitive production tasks (for example, captions, rendering, and project setup), while keeping story decisions, script editing, and final approval human-led.
- Prefer local tools and legitimately free options. Investigate free narration and caption tools first, verifying their licenses, privacy, quotas, and usage terms.
- Do not create/rotate accounts to evade a service's free-tier limits. If no suitable option is genuinely free within its terms, stop and ask before considering a subscription.
- Use a private/draft or otherwise non-public test flow where possible. Do not upload or schedule a video until the owner approves that specific video.
- Open choices include the writing/review workflow, visual production tools, narration/caption generation, storage, and the YouTube upload mechanism.

## 10. Security, Privacy, and Compliance

- The owner is the only known operator. YouTube account access will be needed if uploads are automated; the authentication approach is undecided.
- Protect account credentials and tokens: do not commit them to the repository, include them in videos, or print them in logs. Prefer the least access needed.
- Story content is fictional and authored for the channel. Do not imply it is a true personal account; avoid using real names or identifiable details without permission.
- Track rights for third-party production assets and follow YouTube policies and applicable law. This document is not a legal determination; get permission or qualified legal advice when needed.
- YouTube's monetization policy distinguishes copyright from reused-content and inauthentic-content eligibility. Original scripts reduce dependence on other creators' work, but monetization is not guaranteed: mass-produced, repetitive, or minimally varied videos may still be ineligible. Make each episode materially distinct and viewer-focused rather than relying on a fixed script template with superficial changes.
- Risks include account compromise, third-party asset claims, repetitive-content monetization ineligibility, and accidentally using a paid service. Use private credentials, asset records, per-video approval, and clear run status to reduce these risks.

## 11. Delivery and Operations

- The owner will operate the workflow manually through the CLI; no target release date is specified.
- Pilot on StoryShorts with a small set of fully original Shorts and at least one long-form story. Validate story quality and production effort before ramping up.
- The long-term ambition is one release per day. Set the initial publishing cadence from measured writing/editing capacity so daily output does not force repetitive scripts or lower quality.
- Batch-preparing original stories and scheduling each approved video can reduce day-to-day work. YouTube supports scheduling private videos for a chosen release time; this does not imply any recommendation-system advantage.
- The owner approves every specific video before upload or scheduling. Test with private/draft outputs before public release.
- Keep a modest run history with script version, asset licenses, owner approval, scheduled time, outcome, and actionable errors. Do not log secrets or retain files longer than needed.
- If a run fails, report its status and avoid silently duplicating or misreporting an upload.

## 12. Constraints and Risks

### Constraints

- Existing hardware is covered. No new subscription or other cost may be incurred without asking the owner first.
- The owner has a day job and wants automation to reduce production effort.
- StoryShorts is the only channel in this phase; streamer and GTA VI content are deferred.
- Original stories should be meaningfully varied; the daily publishing ambition must not force mass-produced or low-quality output.
- Third-party production assets must be licensed or otherwise cleared for the intended use.
- Runs are manually started from a CLI, preferably in Docker.

### Risks and mitigations

| Risk | Likelihood / impact | Mitigation or next step | Owner |
|---|---|---|---|
| Original stories take too long to produce consistently | Medium / High | Pilot a small set, time the workflow, and increase automation for production tasks without removing human story review | Owner |
| A tool or upload workflow incurs a cost | Medium / High | Check pricing and quotas before adoption; require owner approval before any charge | Owner |
| Episodes feel repetitive or mass-produced and are not monetized | Medium / High | Vary premise, character, conflict, and resolution; require human editorial review; review current YouTube policies | Owner |
| A third-party production asset is not licensed for the intended use | Unknown / High | Prefer original assets; record and verify license terms before including anything third-party | Owner |
| Automation uploads the wrong, unapproved, incomplete, or duplicate video | Medium / High | Require per-video approval; confirm channel and schedule before upload; record outcomes and handle retries carefully | Owner |
| A free-tier limit is reached or terms prohibit the intended use | Medium / Medium | Use free services only within their terms; do not rotate accounts to bypass limits; stop and ask before any paid alternative | Owner |
| The production workflow takes too much setup or maintenance to save time | Medium / Medium | Test a small StoryShorts pilot and compare total effort with manual production | Owner |

## 13. Success Measures

| Measure | Current baseline | Target | How / when measured |
|---|---|---|---|
| Original pilot stories completed | No original episodes yet | A small pilot set with at least one story supplied in both `short.md` and `long.md` | Verify each version renders independently; review scripts and finished videos before publication |
| Owner time per completed story | Not measured | Establish a baseline; reduce production effort without losing story quality | Track writing, editing, and production time per episode |
| Publishing cadence | Not established for this concept | Choose a sustainable pilot cadence; work toward daily releases if quality holds | Review workload and release history after the pilot |
| New subscriptions or unapproved spending | No new subscriptions intended | Zero | Review service usage and expenses regularly |
| Audience response | Not measured for original stories | Establish a baseline for retention, comments, and returning viewers | Review YouTube Studio analytics after release |
| Uploads without owner approval or uncleared assets | Not measured | Zero | Review approvals, asset records, and upload history |

- An early positive signal is that viewers respond to the stories and the owner can produce them at a sustainable pace without new subscriptions.
- Audience growth and revenue are uncertain outcomes, not guaranteed results. Use the pilot to validate both the creative premise and production effort before scaling.

## 14. Assumptions and Open Questions

### Assumptions to validate

- The Unsent Archive is a working title for a recurring show/concept; StoryShorts remains the existing channel unless the owner chooses to rebrand it.
- The owner will create or substantially edit original scripts; automation assists production rather than mass-producing story text.
- No LLM is required at runtime; token usage for story generation is zero in the MVP.
- Use existing hardware and avoid new subscriptions or paid services unless approved.
- Audience submissions, if introduced later, will have a clear permission and privacy process.

### Open questions

- [ ] Does "The Unsent Archive" feel like the right premise and working title? Should the stories focus on a particular genre or emotional tone?
- [ ] Should StoryShorts remain the channel name, with The Unsent Archive as a series, or should the channel be rebranded?
- [ ] Should narration use the owner's voice or a free text-to-speech tool whose terms permit monetized YouTube use?
- [ ] What visual style can be produced sustainably: original illustrated artifacts, simple animation, or another approach?
- [ ] Is the proposed Markdown subset (`# Title`, `## Scene heading`, plain-text paragraphs) sufficient for writing stories?
- [ ] What pilot release cadence is realistic before committing to daily uploads?
- [ ] Which operating system and release time/time zone should the CLI and publishing schedule use?

## 15. Decisions

| Date | Decision | Reason | Owner |
|---|---|---|---|
| TBD | Focus this phase on original English-language stories; defer streamer clips and GTA VI | Owner's revised scope | Owner |
| TBD | Use The Unsent Archive as a proposed story concept and working title | Provides a distinctive artifact-led format; owner validation pending | Owner |
| TBD | Require owner approval before every upload or scheduled release | Owner's selected publishing mode | Owner |
| TBD | The owner writes scripts; do not generate story text with an LLM in the MVP | Owner's preference and token-minimization goal | Owner |
| TBD | Store each story in a folder with separate `short.md` and `long.md` versions | Owner's requested input format; each version must be independently supplied | Owner |
| TBD | Avoid new subscriptions or costs without asking the owner | Owner's stated requirement | Owner |
| TBD | Treat daily releases as an ambition; set pilot cadence based on sustainable quality | Original scripts require creative work; validate capacity first | Owner |

## 16. References

- [YouTube channel monetization policies](https://support.google.com/youtube/answer/1311392?hl=en) - reused content and inauthentic/repetitive content; reviewed November 2026.
- [YouTube copyright on YouTube](https://support.google.com/youtube/answer/2797466?hl=en) - general information on permissions and copyright; not a legal determination.
- [YouTube: Schedule video publish time](https://support.google.com/youtube/answer/1270709?hl=en) - supports scheduling a private video to go public at a chosen date/time.
