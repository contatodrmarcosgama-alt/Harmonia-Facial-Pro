# Master context — Harmonia Facial Pro

**Purpose:** One place for humans and AI agents to capture **decisions**, **brand voice**,
**API quirks**, and **what we learned** while producing creative for this offer.

Populated from the live landing page (`index.html`) on 2026-08-09. If the page changes,
update this file in the same commit.

## How agents should use this file

- **At the start of substantive work:** Read this file for project-specific context that is
  not in the skill.
- **After meaningful changes:** Append a dated entry under [Changelog](#changelog)
  (Decision / What changed / Why).
- **If fields are empty:** Offer to populate them — ask the user once and write the values back.

---

## The offer

| | |
|---|---|
| **Product** | Harmonia Facial Pro — a mobile web app that produces a personalized facial analysis report |
| **Creator** | Dr Marcos Gama — 10 years of clinical practice in facial harmonization and symmetry analysis |
| **Price** | R$47 (anchored from R$197), or 12× R$3,70 |
| **Stated stack value** | R$308 |
| **Delivery** | Immediate access by email after payment confirmation; report in 12 minutes |
| **Guarantee** | Unconditional 7-day refund |
| **Language / market** | Brazilian Portuguese, Brazil |
| **Platform** | 100% mobile |

**Mechanism — "o Revelador de Potencial":** user uploads two ordinary selfies, answers a
5-minute questionnaire about how they see themselves, and receives a descriptive report with
strengths, improvement opportunities, and a sequenced action plan. Criteria are drawn from
10 years of clinical practice. **No scores. No comparison to unattainable standards.**

**Bonuses (all free with purchase):**

1. Guia de Técnicas Básicas (R$37) — the 3 facial exercises that actually work: mewing
   fundamentals, jaw posture, facial massage. PDF.
2. Rotina Express de 5 Minutos (R$27) — a 5-minute daily sequence that accelerates the plan.
   Doable in the shower, in traffic, before bed.
3. Checklist de Progresso (R$47) — objective weekly indicators, so progress does not depend
   on the mirror.

## Audience

**Primary avatar:** young Brazilian men who feel unseen in professional and social rooms.
They already work on themselves — YouTube facial exercises, mewing attempts, posture fixes —
but have no way to tell whether any of it applies to *their* face.

**The named problem: "Cegueira da Harmonia"** (harmony blindness). You are too close to your
own face to see what needs adjusting. The internet offers generic solutions that work for
some people, and you cannot tell whether they work for you.

**Qualifying signals from the page:**

- Looks in the mirror and cannot identify what they would change.
- Tried mewing and random facial exercises without knowing if they were doing it right.
- Wants clear direction, not generic opinion from people who do not understand the subject.
- Tired of researching looksmaxxing and finding empty talk.

**Emotional core:** they have asked for opinions and received vague answers or polite lies.
Nobody gives them the clear truth they need in order to change. The pain is *invisibility*,
not ugliness — never invert this.

## Brand voice

- **Tone:** direct, calm, clinical-but-warm. An expert who respects you enough to be honest.
  Never hype, never mocking, never "alpha/sigma" looksmaxxing bro-speak.
- **Person:** second person singular ("você"), present tense, short sentences.
- **Words to use:** potencial, revelar, direcionamento, plano de ação, personalizado,
  proporção, estrutura única, clareza, sem julgamentos, prática clínica.
- **Words to avoid:** feio, defeito, nota, score, ranking, chad, glow-up, "vire outra pessoa",
  any before/after framing, any promise of a guaranteed physical result.
- **Register check:** if a line would embarrass the reader if a coworker read it over their
  shoulder, rewrite it.

## Advertising compliance (hard constraints)

Health/appearance offer, young male audience, Meta traffic. These are not stylistic
preferences — violating them risks ad account restriction and contradicts the product:

- **No before/after face comparisons.** Prohibited by Meta for this category, and the product
  makes no promise of physical change.
- **No implied personal attributes.** Never assert something about the viewer's face or body.
  Speak to the situation and the desire.
- **No medical claims, no guaranteed outcomes.** The app produces a descriptive report and a
  plan; it does not diagnose or treat.
- **No scores or ratings in creative.** "Sem scores, sem julgamentos" is a core promise.
- **Faces must be AI-generated or licensed.** Never a real patient photo without written
  release; never Dr Marcos Gama's clinical photography.
- **Testimonials** on the page (Jackson S., Alex M., Felipe B.) refer to clinical experience
  at Instituto Marcos Gama, not to app results. Do not reframe them as app outcomes in ads.

## Landing page facts creative must stay consistent with

- Headline: *"Pare de ser invisível nas reuniões"*
- Promise: analysis in **12 minutes**, from **two selfies** + a **5-minute questionnaire**
- Price framing used on page: *"Menos que uma pizza"*
- Scarcity: a 20-minute countdown on the offer
- It is **not** a video course — it is an interactive app producing a personalized report
- Positioning for unusual faces: the system is designed to value your unique structure, not
  to fit you into a standard. The more unique your face, the more useful the report.

## Reference images

Drop reference images into `references/` at the repo root:

- `references/influencers/` — face/body photos to recreate as AI people
- `references/products/` — product/app screenshots for showcase workflows
- `references/aesthetics/` — mood boards, lighting references, style inspiration

Contents are gitignored (local-only); the folder structure is tracked. For this offer, the
useful refs are **Brazilian male avatars, 22–38, varied phenotypes** — the stock avatars
shipped with the upstream pack skew North American/European and should be replaced.

## Universal prompting principles

These apply across all generative-image and generative-video APIs.

### UGC realism

- **Imperfection block (camera):** Every UGC image/video prompt must include camera
  imperfections: motion blur, overexposure, grain, lens distortion, off-center framing,
  soft focus. Without this, output looks too polished.
- **Skin realism block (mandatory):** Include 3–4 subtle skin cues inline with character
  description: "visible pores, slight unevenness in skin tone, minor undereye shadows, hint
  of shine from natural oils." Do NOT use: acne, pimples, breakouts, blemishes, redness.
  Goal is "real person, not retouched" — not "person with skin problems." **For this offer
  this rule is doubly important:** the creative must never imply the actor has a facial
  problem.
- **Reference image order:** character hero first (strongest identity signal), then product,
  then style refs.

### Influencer / character recreation

- Two-step flow: (1) generate a still image with the reference image as input, (2) show user
  for approval, (3) only then generate video using the approved still as the start frame.
- Never skip the approval step — video is expensive, stills are cheap to iterate.

### Image QA

- Visually review still images after generation (hands, fingers, limbs, face, merged objects,
  artifacts).
- If defective, regenerate with refined prompt — up to **2 retries** (3 attempts total).
- QA retries skip a second credit confirmation but still bill credits.

### Video prompting

- **No subtitles, no captions, no text overlays** — append this clause to every prompt; many
  video models burn captions in by default.
- **Human motion cues are mandatory** for person-on-screen videos: 3–4 cues per prompt
  (breaking eye contact, head tilts, weight shifts, grip adjustments). Without these,
  subjects look like frozen mannequins.
- **Portuguese dialogue:** state the language explicitly in the prompt
  ("speaking Brazilian Portuguese, natural São Paulo accent") — models default to English.

## Meta ad deployment

Used by the **`meta-ad-builder`** shared skill (`shared/skills/meta-ad-builder/`). Fill in
your account IDs once; the skill reads them so you don't paste them every run.

- **Default ad account** (`META_AD_ACCOUNT_ID`): _(fill in)_
- **Facebook Page ID** (`META_PAGE_ID`): _(fill in)_
- **Instagram user ID** (`META_IG_USER_ID`): _(fill in)_
- **Meta Pixel ID** (`META_PIXEL_ID`): _(fill in)_
- **Default destination URL / offer link:** _(fill in — the hosted `index.html`)_
- **Default ad set(s) to deploy into** (name → ID): _(fill in)_
- **Default CTA type:** `LEARN_MORE` (avoid `SIGN_UP` — the offer is a paid purchase)

The access token (`META_ACCESS_TOKEN`) lives in `.env`, never here. Every ad the skill creates
is **PAUSED** — review and un-pause in Meta Ads Manager.

> Note: upstream gitignores `MASTER_CONTEXT.md`. This repo tracks it so the offer context is
> shared, which means **account IDs above are committed**. They are identifiers, not secrets,
> but if you would rather not publish them, move them to `.env` and blank these lines.

## Project snapshot — Arcads

- **API base:** `https://external-api.arcads.ai` (see `.env.example`).
- **Auth:** HTTP Basic via `ARCADS_BASIC_AUTH` (pre-encoded `Basic ...` header) or
  `ARCADS_API_KEY` as Basic password. Values in `.env` must be **single-quoted**
  (special chars: `{`, `[`, `*`).
- **Skill:** `.claude/skills/arcads-external-api/` and `.cursor/skills/arcads-external-api/`
  (synced from `skills/arcads-external-api/` via `scripts/sync-skill.sh`).

## My workspace

- **Default product ID:** _(auto-populated after first `GET /v1/products` call)_
- **Default product name:** _(auto-populated)_

Suggested Arcads product record for this offer:

- `name`: Harmonia Facial Pro
- `description`: App de análise facial personalizada. Duas selfies + questionário de 5 minutos
  geram um relatório descritivo com plano de ação, em 12 minutos. Sem scores, sem julgamentos.
- `targetAudience`: Homens brasileiros de 22 a 38 anos que sentem que passam despercebidos em
  reuniões e ambientes sociais, já tentaram mewing e exercícios faciais por conta própria e
  querem direcionamento claro e personalizado.
- `painPoint`: Cegueira da Harmonia — estar perto demais do próprio rosto para enxergar o que
  ajustar, e receber só respostas vagas de quem poderia opinar.
- `perceived`: Clareza e direcionamento clínico, sem julgamento.

## Credit costs

_Rates from `skills/arcads-external-api/reference.md`. **Confirm in the Arcads platform** —
there is no billing endpoint. Once you have real runs, `logs/arcads-api.jsonl` becomes the
authoritative source and outranks this table._

| Model | Rate | 8s | 15s | Speech | Notes |
|-------|------|----|----|:------:|-------|
| Grok Video | 0.027/s | ~0.22 | ~0.41 | ❌ | Cheapest and fastest (~5s to generate) |
| Sora 2 | 0.05/s | ~0.4 | — | ✅ | Duration enum 4/8/12/16/20; 20s ≈ 1.0 |
| Kling 3.0 | 0.073/s at 3s | — | **0.7** | ❌ | Non-linear — ~35% cheaper per second at 15s |
| Veo 3.1 | — | **1.0 flat** | — | ✅ | No duration field, auto ~8s |
| **Seedance 2.0 i2v** | **~48/s** | **~384** | **~720** | ✅ | Re-validated 2026-05-19 over 8 production runs |
| Nano Banana 2 (image) | — | — | — | ❌ | ~0.03 per image, ~35s |

**⚠️ Seedance 2.0 is three orders of magnitude more expensive than every other model.** A
single 15s talking-head clip ≈ 720 credits, versus ~1.0 for a 20s Sora 2 voiceover and ~0.03
for a still. An older table in `reference.md` still shows "0.06/s" — the 2026-05-19 note
explicitly corrects that figure. Validate creative angles on stills and text-only video
**before** spending on face-locked Seedance clips.

**⚠️ Seedance charges at create time, before the content checker runs.** A flagged prompt
lands as `failed` and the credits are **not** refunded. On an appearance-category offer that
is a live risk — never retry a failed payload unchanged; soften the language first.

## API learnings — Arcads

Confirmed behaviors of the Arcads external API (carried over from upstream).

### Auth

- HTTP Basic with `ARCADS_BASIC_AUTH` (pre-encoded header from dashboard) or `ARCADS_API_KEY`
  as Basic username.
- Values in `.env` must be **single-quoted** due to special characters (`{`, `[`, `*`).

### Unified video endpoint (primary route)

- **`POST /v2/videos/generate`** handles every video model via the `model` field:
  `sora2`, `sora2-pro`, `veo31`, `kling-2.6`, `kling-3.0`, `grok-video`, `seedance-2.0`.
- The legacy `POST /v1/veo31/generate/video` and `POST /v1/sora2/generate/video` routes still
  work but should not be used for new work.
- B-roll (`POST /v1/b-roll`) and scene (`POST /v1/scene`) have no v2 equivalent.

### ⚠️ Image-to-video is broken on most models (confirmed 2026-04-09)

Sending an image input through the v2 endpoint returns **HTTP 500** on nearly every model:

| Model | Image mode | Result |
|---|---|---|
| `veo31` | `startFrame` | ❌ 500 |
| `sora2` | `referenceImages` | ❌ 500 |
| `grok-video` | `startFrame` | ❌ 500 |
| `kling-3.0` | `startFrame` | ✅ works |
| `seedance-2.0` | `referenceImages` | ✅ works |

**Consequence for this offer:** the standard "approve a still, then animate it with Veo 3.1
`startFrame`" workflow does not run today. Face-locked video has exactly two routes —
`seedance-2.0` (has speech, ~48 credits/s) or `kling-3.0` (silent). Probe per model at session
start; the regression may have lifted.

### Seedance 2.0

- Created on `/v2/videos/generate`, but **polled at `GET /v1/assets/{id}`** — it returns
  `type: "seedance_20"` and lives in the assets family. Polling `/v1/videos/{id}` gives **404**.
- Duration 4–15s continuous. Aspect ratio **`9:16` or `16:9` only — no `1:1`**.
- Resolution `480p` or `720p`. Speech comes from the prompt text; `audioEnabled` toggles audio.
- Image input is `referenceImages` (max 3) — **it does not accept `startFrame`**.
- `referenceImages` and `referenceVideos` **cannot be combined** — returns 500. Pick one mode.
  `referenceAudios` may be combined with either.
- `referenceVideos` with more than 1 entry returns 500 despite the schema saying max 3.
- Final mp4 is in the top-level `url` field on the asset response.

### Veo 3.1

- No `duration` field — auto-determines length (~8s typical). 1.0 credit flat.
- **Default resolution: `720p`** — 4K and 1080p show no visible quality difference for UGC but
  produce 3–8x larger files.
- `startFrame` currently 500s (see regression above), so treat Veo as **text-only** for now.

### Sora 2

- Duration enum: 4, 8, 12, 16, 20. Text-only prompting works fine.
- `referenceImages` currently 500s, and `refImageAsBase64` on the legacy route was never
  identity-preserving anyway. Do not use Sora 2 to animate a specific face.
- Polls at `GET /v1/videos/{id}` (field `videoStatus`), unlike Seedance.

### Kling 3.0

- `startFrame` works and does not add cost — the only functioning image-to-video route.
- **Silent** — no speech output. `audioEnabled` is Seedance-only.
- **Never use `endFrame`.** Alone it fails after create and **still charges credits**; combined
  with `startFrame` it returns 500. Use Veo 3.1 for frame-to-frame morphing instead.

### Nano Banana image endpoint

- `POST /v2/images/generate` — lowercase `/v2/` per the OpenAPI spec (uppercase `/V2/` also
  works, but prefer lowercase). `model` and `aspectRatio` are both **required**.
- Valid models: `nano-banana`, `nano-banana-2`, `gpt-image`, `gpt-image-2`, `soul`,
  `grok_image`, `seedream`, `seedream_5_lite`.
- Default to `nano-banana-2`. `nano-banana` = Nano Banana Pro (no `nano-banana-pro` in the enum).
- `aspectRatio` enum: `1:1`, `16:9`, `9:16`. **No `4:5`** — generate `1:1` and post-crop for
  Meta feed-portrait.
- `referenceImages` caps: `nano-banana`/`nano-banana-2` max 14; `gpt-image-2` **max 5**.
- Output: `.png` at the `url` field on the asset response (no `thumbnailUrl`). ~35s.

### Scene and b-roll

- `POST /v1/scene` — `productId`, `prompt`, `aspectRatio`; no `duration`. Use the dedicated
  `script` field for dialogue, `prompt` for visuals.
- `POST /v1/b-roll` — requires `duration` (5 or 10). Silent by nature. ~5 min.

### File upload

- `POST /v1/file-upload/get-presigned-url` — field is `fileType`, **not** `contentType`.
- Response: `presignedUrl` (for `PUT` upload) + `filePath` (pass into `startFrame` /
  `referenceImages` / `referenceVideos` / `referenceAudios`).
- **⚠️ A `filePath` is one-time-use.** Reusing it returns `400 REFERENCE_FILE_NOT_FOUND`. To
  anchor the same hero still across several calls, **re-upload before every call**.
- If the image's longest side is under 1024px, upscale to 1080px (Lanczos) and convert to RGB
  JPEG first, or endpoints return `422 The provided image is too small`.

### Polling

| Create response `type` | Poll endpoint | Status field |
|---|---|---|
| `sora2`, `sora2-pro`, `veo31`, `kling-*`, `grok-video` | `GET /v1/videos/{id}` | `videoStatus` |
| **`seedance_20`**, image models, b-roll, scene | `GET /v1/assets/{id}` | `status` |

- Status enum: `created` | `pending` | `generated` | `failed` | `uploaded`.
- Typical times: Grok ~5s, Veo 3.1 ~67s, scene ~75s, Sora 2 ~98s, Kling 15s ≈ 250s,
  Nano Banana ~35s, Seedance 2–6 min.

### Product API

- `ProductCreationDto` has text-only fields (`name`, `description`, `targetAudience`,
  `mainFeatures`, `painPoint`, `perceived`) — no image upload.
- Product images are dashboard-only (`pictureId` field).

### Folder / project organization

- Every agent session that generates assets should create (or reuse) a folder named
  **"Arcads API - YYYY-MM-DD"** with a matching project inside it, then assign all generated
  assets to that project.
- API calls: `POST /v1/folders`, `POST /v1/projects`, `POST /v1/assets/add-to-project`.
  Check `GET /v1/products/{productId}/folders` first to avoid duplicates.

## Changelog

### 2026-08-09 — Pack installed, offer context captured

- **Decision:** Vendor the Arcads skill pack into this repo rather than keeping it separate,
  so ad creative and the landing page it points at stay in sync.
- **What changed:** Added `skills/`, `shared/`, `scripts/`, `.claude/settings.json`,
  `.cursor/rules/`, `.env.example`, agent configs, and `ads/briefs/`. Upstream's 119MB of
  stock reference media was not vendored (upstream gitignores it; the avatars also skew away
  from this offer's Brazilian male audience).
- **Why:** The offer, voice, and compliance constraints were only encoded in the landing page
  copy. Capturing them here means every creative run starts from the same brief instead of
  re-deriving the offer from HTML.
