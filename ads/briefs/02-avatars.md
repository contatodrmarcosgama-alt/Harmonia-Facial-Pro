# Avatars

The upstream pack ships 11 stock influencer character sheets in `references/influencers/`.
They were not vendored into this repo: they skew North American/European, and they are mostly
women. This offer sells to Brazilian men. Build your own set.

Use the `character-sheet` workflow in
`skills/arcads-external-api/prompting/prompt-library/character-sheet.md` — Nano Banana 2, hero
front portrait first, **user approves the hero before the other 9 angles are generated**.

Folder naming convention (from that skill):
`references/influencers/{name}-{hair}-{style}-{feature}-{eyes}-{skin}/`

---

## Casting rules for this offer

The actor is **not** a model, and is **not** presented as someone with a facial problem. He is
an ordinary, reasonably put-together guy who found something useful. Getting this wrong is the
single most common way creative for this category fails:

- **Age 24–36.** Old enough to be in the meetings the headline references.
- **Ordinary attractiveness.** If the actor is visibly a model, the ad reads as a beauty ad and
  the "invisibility" premise collapses.
- **Never direct the model to look sad about his face.** He can look tired, distracted, or
  mid-thought. Direction like "insecure about his appearance" produces creative that asserts a
  flaw in the viewer — which is both a Meta policy risk and off-brand.
- **Brazilian phenotype range.** Cast across the actual spread: pardo, branco, preto, with
  Brazilian-typical hair textures. Do not generate one look and call it done.
- **Wardrobe:** plain t-shirt, casual button-down, or a polo. Nothing aspirational, no suits.
- **Skin realism block is mandatory** (visible pores, slight unevenness, minor undereye
  shadows, hint of natural oil) — but never acne, redness, or blemishes. "Real person, not
  retouched," never "person with a skin condition."

---

## The four avatars to build

### A1 — Rafael, 29, pardo, escritório

The headline avatar. He is the guy in the meeting.

```
A 29-year-old Brazilian man with dark brown short wavy hair, medium-brown (pardo) skin
with visible pores and slight unevenness in skin tone, dark brown eyes, average build,
light stubble, wearing a plain heather-grey t-shirt. Clean white studio background,
photorealistic, visible skin texture, individual hair strands catching light,
minor undereye shadows, hint of shine from natural oils.
```

Folder: `references/influencers/rafael-dark-brown-short-wavy-stubble-brown-eyes-medium/`

### A2 — Diego, 25, branco, academia/casa

The mewing-and-YouTube-tutorials avatar. Angle 3.

```
A 25-year-old Brazilian man with light brown straight hair in a short crop, fair skin
with visible pores and light freckling across the nose, hazel eyes, lean athletic build,
clean-shaven, wearing a plain navy crew-neck t-shirt. Clean white studio background,
photorealistic, visible skin texture, individual hair strands catching light,
minor undereye shadows.
```

Folder: `references/influencers/diego-light-brown-short-crop-freckles-hazel-eyes-fair/`

### A3 — Marcelo, 34, preto, profissional

The authority-adjacent avatar. Angles 4 and 6, and retargeting.

```
A 34-year-old Brazilian man with black tightly-coiled hair in a low fade, deep brown skin
with visible pores and natural sheen, dark brown eyes, medium build, close-trimmed beard,
wearing a plain white button-down shirt with the collar open. Clean white studio background,
photorealistic, visible skin texture, minor undereye shadows.
```

Folder: `references/influencers/marcelo-black-low-fade-trimmed-beard-brown-eyes-deep/`

### A4 — Thiago, 22, branco, quarto/UGC

The youngest, most native-feeling UGC avatar. Bedroom and bathroom selfie setups.

```
A 22-year-old Brazilian man with dark blond messy medium-length hair, fair skin with
visible pores and slight unevenness in skin tone, blue-grey eyes, slim build,
patchy light stubble, wearing a plain black t-shirt. Clean white studio background,
photorealistic, visible skin texture, individual hair strands catching light,
minor undereye shadows, hint of shine from natural oils.
```

Folder: `references/influencers/thiago-dark-blond-messy-medium-stubble-blue-grey-eyes-fair/`

---

## Dr Marcos Gama in creative

Do not generate an AI likeness of Dr Marcos Gama, and do not use his clinical photography in
ads. For Angle 6, either:

- shoot or supply a real, cleared photo of him and use it as a static with a typography
  treatment (T27 handwritten founder letter, T33 bold typography hero), or
- run the angle as voiceover over b-roll with no face on screen.

The same rule covers patient photography: never in an ad without written release, and never
as a before/after regardless of release.

---

## Scene setups to pair with the avatars

Feed these as the situation half of the prompt once the character sheet exists. Reference
image order is always **character hero first**, then product, then style refs.

| Setup | Avatar | Angle | Note |
|---|---|---|---|
| Meeting room, mid-table, others talking | A1 | 1 | He is present but not the focus — that *is* the ad |
| Bathroom mirror, morning, phone in hand | A4, A2 | 2, 3 | The classic UGC frame; mirror must not read as a "checking my flaws" moment |
| Bedroom desk, laptop closed, phone up | A2 | 3, 5 | Where the questionnaire actually gets filled out |
| Car, parked, seatbelt on, talking to camera | A1, A3 | 4 | Highest-trust UGC frame in this category |
| Kitchen, morning, leaning on counter | A3 | 6 | Calm, authority-adjacent |

Every one of these needs the camera imperfection block (motion blur, slight overexposure,
grain, off-center framing) or it will look like stock footage and lose the UGC read.
