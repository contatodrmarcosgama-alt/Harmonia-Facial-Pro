# UGC video scripts

Six scripts, each mapped to an angle from `01-angles-and-hooks.md` and an avatar from
`02-avatars.md`.

## Model routing

| Need | Model | Why |
|---|---|---|
| Animate an approved avatar still | **Veo 3.1** with `startFrame` | Only route that preserves the face. ~8s, auto-length, 720p default |
| Talking-head longer than ~8s | **Veo 3.1** ×2 stitched, or **Seedance 2** | Sora 2's `refImageAsBase64` is style-only and will not hold the face |
| No specific face needed (b-roll, hands, phone) | **Sora 2** | Up to 20s, text-only prompting is fine here |
| Scene/product beats | `POST /v1/scene` | ~75s turnaround, returns a `.jpg` thumbnail too |

**Never** use Sora 2 to animate a specific avatar. It does not preserve identity — the ad will
come back with a different person than your approved still.

## Mandatory prompt blocks

Every video prompt below assumes these are appended:

```
No subtitles, no captions, no text overlays.
Speaking Brazilian Portuguese, natural São Paulo accent.
Camera imperfections: slight motion blur, mild overexposure near the window,
visible grain, off-center handheld framing, occasional soft focus.
Skin: visible pores, slight unevenness in skin tone, minor undereye shadows,
hint of shine from natural oils.
```

Plus 3–4 human motion cues per prompt, or the subject reads as a mannequin. Examples that suit
this category: breaking eye contact to look down at the phone, tilting the head while thinking,
shifting weight against the counter, adjusting grip on the phone, brief half-smile before
continuing.

Captions get burned in afterward via the `caption-video` skill — not by the model.

---

## V1 — "A reunião" (Angle 1, avatar A1 Rafael)

Format: talking head, ~15s, two Veo clips stitched. Meeting-room b-roll optional.

> **[0–3s, hook]** Ontem eu falei numa reunião e a conversa continuou como se eu não tivesse
> falado. Já aconteceu com você?
>
> **[3–9s]** Não é que eu seja ignorado. É que ninguém repara. E eu não sabia nem o que fazer
> com isso, porque quando eu pergunto pros outros, ninguém responde de verdade.
>
> **[9–15s, CTA]** Achei um app que analisa duas selfies suas e te devolve um relatório com o
> que dá pra aprimorar e em que ordem. Doze minutos. Link aqui embaixo.

Shot: seated, medium close, office or home in soft background blur. Motion cues: glances off
camera on "ninguém repara", small shrug, leans in on the CTA.

---

## V2 — "Cegueira da Harmonia" (Angle 2, avatar A3 Marcelo)

Format: talking head, ~12s. The highest-credibility read of the mechanism.

> **[0–3s, hook]** Existe um nome pro motivo de você não conseguir olhar pro próprio rosto:
> Cegueira da Harmonia.
>
> **[3–8s]** Você convive com esse rosto há 30 anos. Perdeu completamente a capacidade de ver
> ele de fora. Por isso o espelho não ajuda e a opinião dos outros também não.
>
> **[8–12s, CTA]** Esse app te dá o olhar de fora. Duas fotos, doze minutos, plano de ação.

Shot: kitchen counter, morning light, leaning. Motion cues: gestures once on "de fora", head
tilt on the mechanism name, breaks eye contact mid-sentence.

---

## V3 — "Oito meses de mewing" (Angle 3, avatar A2 Diego)

Format: bathroom-mirror selfie UGC, ~15s. Highest-intent script in the set.

> **[0–3s, hook]** Oito meses fazendo mewing. Quer saber o que eu consigo te falar sobre o
> resultado? Nada.
>
> **[3–10s]** Sério. Eu não tenho como saber se funcionou, se eu tava fazendo certo, nem se
> era pro meu tipo de rosto. Eu tava seguindo vídeo de gringo aleatório.
>
> **[10–15s, CTA]** Aí eu fiz uma análise de verdade. Mandei duas selfies, respondi umas
> perguntas, e recebi um plano que faz sentido pro meu rosto. Com um checklist pra eu medir.

Shot: phone held in hand, bathroom mirror, morning. **Direction note:** he is annoyed at the
wasted time, never at his face. Do not let the model examine his reflection critically — that
frames the ad as a defect callout. Motion cues: phone hand shifts, looks away on "nada", small
laugh on "vídeo de gringo aleatório".

---

## V4 — "A mentira educada" (Angle 4, avatar A1 Rafael)

Format: car, parked, seatbelt on, ~12s. The most native UGC frame in this category.

> **[0–4s, hook]** Você já pediu opinião sincera sobre a sua aparência e recebeu "você é bonito
> do seu jeito"? Isso não é resposta.
>
> **[4–9s]** Ninguém fala a verdade porque falar a verdade sobre a cara de alguém tem custo.
> Então todo mundo se protege com resposta vaga.
>
> **[9–12s, CTA]** Um relatório não tem esse problema. Doze minutos, sem julgamento e sem nota.

Shot: driver's seat, parked, daylight through windshield. Motion cues: glances at rearview,
adjusts posture, brief pause before the CTA line.

---

## V5 — "Como funciona" (Angle 5, no face required)

Format: screen-and-hands walkthrough, ~20s. **Sora 2** is fine here — no identity to preserve.

> **[0–4s]** Duas selfies. Qualquer luz, nada profissional.
>
> **[4–10s]** Um questionário de cinco minutos sobre como você se vê. É aí que o sistema
> entende o seu caso.
>
> **[10–16s]** Doze minutos depois, o relatório: o que ajustar, o que manter, e a ordem exata.
>
> **[16–20s]** Não é curso, não é videoaula. É um app. R$47, com garantia de sete dias.

Shot: overhead and over-shoulder of hands on a phone, desk, daylight. Voiceover only, no face.
This is the script most likely to survive as an evergreen — it makes no emotional claim, so it
carries less policy risk and less creative fatigue.

---

## V6 — "10 anos de consultório" (Angle 6, no AI face)

Format: voiceover over b-roll, ~15s. No face on screen — see the Dr Marcos Gama rule in
`02-avatars.md`.

> **[0–4s]** Dez anos fazendo harmonização facial e análise de simetria.
>
> **[4–10s]** No consultório era sempre o mesmo padrão: cara jovem, perdido em informação
> contraditória da internet, tentando coisa aleatória sem saber se servia pra ele.
>
> **[10–15s]** Então ele pegou os critérios da prática clínica e transformou num sistema que
> funciona sem agendar consulta.

Shot: b-roll — clinic-adjacent but non-identifying (notebook, pen, hands, window light). Never
patient photography. If you have cleared footage of Dr Gama himself, use that instead of
generated b-roll; it will outperform.

---

## Production order

1. Build the four character sheets (`02-avatars.md`). Approve each hero before the 9 angles.
2. Generate one still per script from the approved character sheet. **Approve the still.**
3. Only then animate with Veo 3.1 using that still as `startFrame`.
4. QA, then burn captions with the `caption-video` skill (needs `ffmpeg`, `whisper`, and
   `npx hyperframes`).
5. Publish via `meta-ad-builder`. Every ad it creates lands PAUSED — un-pause in Ads Manager.

V5 needs no avatar at all, so it is the fastest script to get into the account. Start there if
you want a video live before the character sheets are built.

## Compliance re-check before publishing

- [ ] No before/after in any frame
- [ ] No score or rating shown or spoken
- [ ] No line asserting a flaw in the viewer
- [ ] No guaranteed outcome or timeline for physical change
- [ ] Burned-in captions match the spoken pt-BR, accents intact
- [ ] No real patient or clinical photography
