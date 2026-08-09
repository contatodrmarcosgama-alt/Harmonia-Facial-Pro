# Image ads

Template picks from `shared/skills/image-ad-prompting/prompting/prompt-library.md`, with
variables filled for this offer. Read
`shared/skills/image-ad-prompting/OVERVIEW.md` first.

## Two constraints before you generate anything

**1. There is no product photo.** Every template that asks for a "product hero" was written for
physical goods. This offer is an app. Substitute one of:

- a phone held in hand showing the report screen (generate once, save to
  `references/products/`, reuse as the product reference everywhere), or
- the report itself as a clean UI card, no device frame, or
- nothing — the typography-only templates (T33, T27, T25) need no product at all and are the
  safest starting point.

Build the phone-in-hand asset first. It unlocks most of the library.

**2. Aspect ratio.** On the Arcads backend only `1:1`, `16:9`, and `9:16` render. Meta's
preferred feed-portrait `4:5` is **not** available on Arcads — generate `1:1` and post-crop, or
route that template through KIE Nano Banana. Several strong templates (T1 Apple Notes, T21
napkin testimonial) are specced at `2:3`, which Arcads cannot render at all — use `1:1` there.

**Banned on this offer:** T13, T19, and T17-as-facial-change. See `README.md`.

---

## Tier 1 — start here

### T32 — Pain-point checklist (Angle 3)

`1:1`, both backends clean. The single best fit: this audience is problem-aware and the page's
own qualifier list converts almost verbatim into the checklist.

Filled variables:

- `{headline}` = `VOCÊ JÁ TENTOU DE TUDO. / FUNCIONOU?`
- `{checklist_items}`:
  - `☐ Mewing há meses sem saber se está certo`
  - `☐ Exercício facial que você achou no YouTube`
  - `☐ Pediu opinião e recebeu resposta vaga`
  - `☐ Pesquisou looksmaxxing e achou só papo vazio`
  - `☐ Olha no espelho e não sabe o que mudaria`
- `{tagline}` = `DUAS FOTOS. DOZE MINUTOS. UM PLANO.`
- `{footer_url_line}` = `Harmonia Facial Pro — análise facial personalizada, sem scores e sem julgamentos. R$47.`
- Product section: the phone-in-hand report asset.

Note the headline is a question about *the methods*, not about the reader's face. Keep it that
way — "VOCÊ JÁ TENTOU DE TUDO" is about effort, which is flattering; a headline about results
would assert a flaw.

### T33 — Bold typography hero quote (Angles 1, 4)

`1:1`, no product asset needed, cheapest thing in the library to test. Run the strongest hooks
from `01-angles-and-hooks.md` as pure typography:

- `Ninguém vai te falar a verdade sobre o seu rosto.`
- `Existe um nome pra isso: Cegueira da Harmonia.`
- `Você olha no espelho todo dia. É por isso que você não vê.`

Attribution line: `Harmonia Facial Pro · análise em 12 minutos · R$47`

Three variants at ~0.03 credits each is the cheapest possible read on which angle has legs.
Do this before committing to any video.

### T12 — Fake ChatGPT conversation (Angle 3)

`1:1`, **gpt-image-2 strongly preferred** (nano-banana garbles the logo and body text). Keep the
response to 3 short numbered lines — the template's own warning, and it is real.

- `{user_question}` = `Como sei se o mewing está funcionando no meu rosto?`
- `{chatgpt_response_short}`:

  > Não dá pra saber sozinho — você está perto demais do próprio rosto. O que funciona:
  >
  > 1. Análise dos seus traços específicos
  > 2. Um plano na ordem certa
  > 3. Indicadores objetivos de progresso
  >
  > O Harmonia Facial Pro faz os três.

- `{cta_text}` = `Análise em 12 minutos — R$47`
- `{cta_color}` = pull from the landing page's primary button color

Caveat from the template's own notes: "AI agrees" social proof works best for category leaders.
This is an unknown brand, so treat T12 as a test, not a core creative.

---

## Tier 2 — after Tier 1 gives you a winning angle

### T18 — Flowchart "old way" vs "new way" (Angle 3)

`1:1`. The compliant way to do a comparison on this offer: it compares *processes*, not faces.

- Old way: `Vídeo aleatório no YouTube → tenta por 3 meses → não sabe se mudou → desiste → outro vídeo`
- New way: `Duas selfies → questionário de 5 min → relatório em 12 min → plano na ordem certa → checklist semanal`

### T6 — Comparison table, dark (Angle 3)

`1:1`. Rows compare the approach, never the reader:

| | Conteúdo genérico | Harmonia Facial Pro |
|---|---|---|
| Feito pro seu rosto | ✗ | ✓ |
| Ordem das mudanças | ✗ | ✓ |
| Como medir progresso | ✗ | ✓ |
| Critério clínico | ✗ | 10 anos |
| Tempo até ter um plano | — | 12 minutos |

### T23 — POV calendar timeline of pain points (Angle 1)

`1:1`. Months of effort with no way to tell if it worked — lands the Angle 3 frustration in a
format that feels observational rather than accusatory.

### T27 — Handwritten founder letter (Angle 6)

`1:1`, no AI face needed, which is exactly what you want for the Dr Marcos Gama angle. Source
the letter text from the page's creator section: he built the method because young men were
getting lost in contradictory information online.

### T11 — Fake comment thread (Angle 4)

`1:1`. A comment asking the question everyone asks, and a brand reply. Do **not** fabricate a
customer result in the thread — keep the reply about what the report contains.

---

## Prompt hygiene for this offer

Append to every image prompt, on top of the library's always-on glyph-safety suffix:

```
All text in Brazilian Portuguese with correct accents (ã, ç, é, ê, í, ó, õ, ú).
No before/after comparison. No numeric score, rating, or grade anywhere in the image.
No text asserting a flaw in the viewer's appearance.
```

Portuguese diacritics are the most common rendering failure on these models — check every
generated image for dropped tildes and cedillas during QA, not just hands and faces. `Você`
rendering as `Voce` is an instant credibility kill on Brazilian traffic.

## QA checklist

Per the skill's standard QA (max 2 retries, 3 attempts total), plus for this offer:

- [ ] Accents intact on every word
- [ ] No score, number-out-of-ten, or rating visible
- [ ] No before/after implication
- [ ] Price renders as `R$47` (not `R47`, `$47`, or `R$ 47,00`)
- [ ] Any face in frame reads as an ordinary person, not a model, and is not looking distressed
      at his own reflection
- [ ] Text inside the central 84% safe zone
