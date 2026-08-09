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

_Fill in your plan's credit costs. The agent references this table before every generation.
Values below are upstream defaults — **confirm in the Arcads platform**, there is no billing
endpoint._

| Model | Credits per generation | Notes |
|-------|----------------------|-------|
| Veo 3.1 | 1 | Same cost at 720p, 1080p, and 4K |
| Sora 2 | _(fill in)_ | |
| Sora 2 Pro | _(fill in)_ | Auto-selected when using `refImageAsBase64` |
| Kling 3.0 (scene) | _(fill in)_ | |
| Kling 3.0 (b-roll) | _(fill in)_ | |
| Nano Banana 2 (image, `nano-banana-2`) | 0.03 | ~35s generation time |
| Nano Banana Pro (image, `nano-banana`) | _(fill in)_ | |
| Nano Banana (scene) | _(fill in)_ | |

## API learnings — Arcads

Confirmed behaviors of the Arcads external API (carried over from upstream).

### Auth

- HTTP Basic with `ARCADS_BASIC_AUTH` (pre-encoded header from dashboard) or `ARCADS_API_KEY`
  as Basic username.
- Values in `.env` must be **single-quoted** due to special characters (`{`, `[`, `*`).

### Nano Banana image endpoint

- `POST /V2/images/generate` (note **uppercase V2**). `model` is **required**.
- Valid models: `nano-banana`, `nano-banana-2`, `gpt-image`, `soul`, `grok_image`, `seedream`,
  `seedream_5_lite`.
- Default to `nano-banana-2`. `nano-banana` = Nano Banana Pro (no `nano-banana-pro` in the enum).
- Output: `.png` at the `url` field on the asset response (no `thumbnailUrl`).
- Generation time: ~35 seconds typical.

### Scene for image-like output

- `POST /v1/scene` with only `productId`, `prompt`, `aspectRatio` produces a short video +
  `.jpg` thumbnail.
- Best path when you need a still frame to feed into another model.
- No `duration` required (unlike b-roll, which needs 5 or 10).

### B-roll

- Requires `duration` (5 or 10 seconds). Slower than scene (~5 min vs ~75s).

### Veo 3.1

- `startFrame` vs `referenceImages` are **mutually exclusive**. `startFrame` = video animates
  from this exact image. `referenceImages` = style/mood inspiration only.
- Default: always use `startFrame` when the user provides a single person photo.
- No `duration` field — auto-determines length (~8s typical).
- **Default resolution: `720p`** — 4K and 1080p show no visible quality difference for UGC but
  produce 3–8x larger files.

### Sora 2

- `refImageAsBase64` is a **style/mood reference only** — it does NOT preserve face, pose, or
  scene. Do NOT use Sora 2 to animate a specific starting frame.
- Best for text-only video generation, or a product photo → UGC video directly.
- Duration enum: 4, 8, 12, 16, 20.

### File upload (for Veo start frames / reference images)

- `POST /v1/file-upload/get-presigned-url` — field is `fileType`, **not** `contentType`.
- Response: `presignedUrl` (for `PUT` upload) + `filePath` (pass into `startFrame` /
  `referenceImages`).

### Kling / Nano Banana video routing

- No dedicated POST endpoints for Kling. Asset type enums (`kling_30`, `nano-banana`) exist on
  responses. Model selection may be server-side for b-roll/scene.

### Polling

- `GET /v1/assets/{id}` — status goes `pending` → `generated` | `failed`.
- Typical times: scene ~75s, b-roll ~5 min, Veo 3.1 ~4 min, Nano Banana image ~35s.

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
