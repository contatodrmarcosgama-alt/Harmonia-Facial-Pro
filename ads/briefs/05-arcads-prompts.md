# Prompts prontos para a API Arcads

Payloads conferidos contra `skills/arcads-external-api/reference.md`. **Nada aqui foi
disparado** — são os corpos de requisição prontos para quando você tiver a chave no `.env`.

Substitua `PRODUCT_ID` e `PROJECT_ID` pelos valores da sua conta. Auth em todos os exemplos:
`-H "Authorization: $ARCADS_BASIC_AUTH"` (a referência recomenda o header em vez de `-u` para
evitar 403 no polling posterior).

---

## 0. Setup da sessão (a skill exige antes de gerar)

```bash
source .env
BASE="https://external-api.arcads.ai"
TODAY=$(date +%F)

# 1. achar o produto
curl -sS -H "Authorization: $ARCADS_BASIC_AUTH" "$BASE/v1/products"

# 2. reusar a pasta do dia se já existir
curl -sS -H "Authorization: $ARCADS_BASIC_AUTH" "$BASE/v1/products/PRODUCT_ID/folders"

# 3. senão, criar pasta + projeto
curl -sS -X POST -H "Authorization: $ARCADS_BASIC_AUTH" -H "Content-Type: application/json" \
  -d "{\"productId\":\"PRODUCT_ID\",\"name\":\"Arcads API - $TODAY\"}" "$BASE/v1/folders"

curl -sS -X POST -H "Authorization: $ARCADS_BASIC_AUTH" -H "Content-Type: application/json" \
  -d "{\"productId\":\"PRODUCT_ID\",\"folderId\":\"FOLDER_ID\",\"name\":\"Arcads API - $TODAY\"}" \
  "$BASE/v1/projects"
```

## 1. Criar o produto no Arcads

`POST /v1/products` — só texto, sem imagem (imagem é pelo dashboard).

```json
{
  "name": "Harmonia Facial Pro",
  "description": "App de análise facial personalizada. Duas selfies e um questionário de 5 minutos geram um relatório descritivo com plano de ação, em 12 minutos. Sem scores, sem julgamentos.",
  "targetAudience": "Homens brasileiros de 22 a 38 anos que sentem que passam despercebidos em reuniões e ambientes sociais, já tentaram mewing e exercícios faciais por conta própria e querem direcionamento claro e personalizado.",
  "mainFeatures": [
    "Relatório personalizado em 12 minutos a partir de duas selfies",
    "Plano de ação com a ordem exata das mudanças",
    "Critérios de 10 anos de prática clínica em harmonização facial",
    "Checklist de progresso semanal, sem depender do espelho",
    "100% mobile, sem consulta e sem videoaula"
  ],
  "painPoint": "Cegueira da Harmonia: estar perto demais do próprio rosto para enxergar o que ajustar, e só receber respostas vagas de quem poderia opinar.",
  "perceived": "Clareza e direcionamento clínico, sem julgamento e sem nota."
}
```

---

## 2. Character sheet — hero still (Nano Banana 2)

`POST /v2/images/generate`. `aspectRatio` é **obrigatório** (`1:1`, `16:9` ou `9:16`).
Custo ≈ 0,03. Geração ≈ 35s. Poll em `GET /v1/assets/{id}`.

Passe 1 — hero frontal do avatar A1 (Rafael). **Aprove antes de gerar os 9 ângulos.**

```json
{
  "productId": "PRODUCT_ID",
  "projectId": "PROJECT_ID",
  "model": "nano-banana-2",
  "aspectRatio": "1:1",
  "prompt": "A 29-year-old Brazilian man with dark brown short wavy hair, medium-brown (pardo) skin, dark brown eyes, average build, light stubble, wearing a plain heather-grey t-shirt, relaxed neutral expression looking directly at camera. Clean white studio background, photorealistic, visible skin texture with visible pores and slight unevenness in skin tone, minor undereye shadows, hint of shine from natural oils, individual hair strands catching light. Ordinary approachable person, not a fashion model, not retouched. Exactly one face, two hands, anatomically correct."
}
```

Passe 2 — os 9 ângulos, com o hero aprovado em `referenceImages` (Nano Banana aceita até 14).
**Refaça o upload presignado antes de cada chamada** — o `filePath` é de uso único.

Ângulos: `02-3q-left`, `03-3q-right`, `04-profile-left`, `05-profile-right`, `06-face-closeup`,
`07-back-shoulder`, `08-medium-portrait`, `09-full-body-3q`, `10-above-angle`.

```json
{
  "productId": "PRODUCT_ID",
  "projectId": "PROJECT_ID",
  "model": "nano-banana-2",
  "aspectRatio": "1:1",
  "referenceImages": ["FILEPATH_DO_UPLOAD_FRESCO"],
  "prompt": "The same man from the reference image, three-quarter view turned 45 degrees to his left, same face, same hair, same heather-grey t-shirt, same lighting. Clean white studio background, photorealistic, visible skin texture, minor undereye shadows. Identity must match the reference exactly."
}
```

Salve em `references/influencers/rafael-dark-brown-short-wavy-stubble-brown-eyes-medium/`.

Repita para A2 Diego, A3 Marcelo e A4 Thiago com os descritores de `02-avatars.md`.

---

## 3. Anúncios estáticos

`POST /v2/images/generate`. Comece por estes — ~0,03 cada, é onde você compra sinal barato.

### T33 — tipografia pura (Ângulo 4), sem produto e sem rosto

```json
{
  "productId": "PRODUCT_ID",
  "projectId": "PROJECT_ID",
  "model": "gpt-image-2",
  "aspectRatio": "1:1",
  "prompt": "1:1 static ad creative, 1080x1080, edge-to-edge. Pure off-white #FAFAF8 background. Centered bold black sans-serif typography, tight tracking, filling the central 84% safe zone, in four stacked lines at large size: \"NINGUÉM VAI TE\" / \"FALAR A VERDADE\" / \"SOBRE O SEU\" / \"ROSTO.\" Below, separated by generous white space, a thin horizontal rule, then one small line of regular-weight grey text: \"Harmonia Facial Pro · análise em 12 minutos · R$47\". Calm, editorial, premium. Standalone ad creative, no device frame, no browser chrome. All text in Brazilian Portuguese with correct accents. No before/after comparison. No numeric score, rating or grade anywhere. No human face in the image."
}
```

Variantes: troque o texto pelos outros hooks de `01-angles-and-hooks.md` —
`EXISTE UM NOME PRA ISSO: CEGUEIRA DA HARMONIA.` e
`VOCÊ OLHA NO ESPELHO TODO DIA. É POR ISSO QUE VOCÊ NÃO VÊ.`

### T32 — checklist de dores (Ângulo 3)

```json
{
  "productId": "PRODUCT_ID",
  "projectId": "PROJECT_ID",
  "model": "gpt-image-2",
  "aspectRatio": "1:1",
  "prompt": "1:1 static ad creative, 1080x1080, edge-to-edge, pure white background. Top section (~22% height): centered bold black sans-serif headline, two stacked lines, large, tight tracking: \"VOCÊ JÁ TENTOU DE TUDO.\" / \"FUNCIONOU?\" Middle section (~40% height, generous vertical spacing): a vertical list of exactly five checklist rows, each a hollow grey square checkbox on the left plus regular black sans-serif text. Items verbatim: \"Mewing há meses sem saber se está certo\", \"Exercício facial que você achou no YouTube\", \"Pediu opinião e recebeu resposta vaga\", \"Pesquisou looksmaxxing e achou só papo vazio\", \"Olha no espelho e não sabe o que mudaria\". Bottom section (~20% height): centered, bold serif line \"DUAS FOTOS. DOZE MINUTOS. UM PLANO.\", then smaller regular grey line \"Harmonia Facial Pro — análise facial personalizada, sem scores e sem julgamentos. R$47\". All text within the central 84% safe zone. All text in Brazilian Portuguese with correct accents (ã, ç, é, ê, í, ó, õ, ú). No before/after comparison. No numeric score, rating or grade. No text asserting a flaw in the viewer's appearance. No human face."
}
```

### T12 — conversa ChatGPT (Ângulo 3)

`gpt-image-2` fortemente preferido — a referência avisa que o `nano-banana` embaralha o logo e
o corpo do texto. Mantenha a resposta curta: 3 linhas numeradas + 1 fecho.

```json
{
  "productId": "PRODUCT_ID",
  "projectId": "PROJECT_ID",
  "model": "gpt-image-2",
  "aspectRatio": "1:1",
  "prompt": "1:1 static ad creative, 1080x1080, edge-to-edge — a fake ChatGPT-style conversation screenshot as a standalone ad creative. Dark grey background #343541. Render text density LOW, body text LARGE and fully legible. Top (~22%): user message row — small rounded-square avatar on the left, then white sans-serif text at large size: \"Como sei se o mewing está funcionando no meu rosto?\" Faint grey divider. Middle (~58%): ChatGPT response row — small green rounded-square tile with a white spiral glyph on the left, then white sans-serif text at large size with generous line spacing, reading exactly: \"Não dá pra saber sozinho — você está perto demais do próprio rosto. O que funciona:\" then three numbered lines \"1. Análise dos seus traços específicos\" \"2. Um plano na ordem certa\" \"3. Indicadores objetivos de progresso\" then a closing line \"O Harmonia Facial Pro faz os três.\" Bottom (~12%): a full-width horizontal CTA bar in deep teal, white sans-serif text left-aligned \"Análise em 12 minutos — R$47\" with a small white right-arrow on the right edge. No browser chrome, no sidebar, no input box. All text in Brazilian Portuguese with correct accents. No before/after. No numeric score or rating."
}
```

---

## 4. Vídeo com rosto travado — Seedance 2.0

`POST /v2/videos/generate`. Só `9:16` ou `16:9`. Sem `startFrame` — a imagem entra em
`referenceImages`. **Nunca** combine `referenceImages` com `referenceVideos` (500).

**Custo: ~48 créditos/segundo.** 12s ≈ 576 créditos. Mostre a estimativa e espere confirmação.

V3 beat 1 ("Oito meses de mewing", avatar A2 Diego):

```json
{
  "model": "seedance-2.0",
  "productId": "PRODUCT_ID",
  "projectId": "PROJECT_ID",
  "aspectRatio": "9:16",
  "duration": 12,
  "resolution": "720p",
  "audioEnabled": true,
  "referenceImages": ["FILEPATH_DO_UPLOAD_FRESCO"],
  "prompt": "Vertical selfie-style UGC video. A 25-year-old Brazilian man matching the reference image holds his phone at arm's length in a bathroom, morning daylight from a window to his left, plain tiled wall behind him. He talks straight to camera, casual and a little exasperated about wasted time, upbeat not sad. Dialogue, spoken in Brazilian Portuguese with a natural São Paulo accent: \"Oito meses fazendo mewing. Sabe o que eu consigo te falar sobre o resultado? Nada. Eu tava seguindo vídeo de gringo aleatório, sem saber se servia pro meu rosto.\" Human motion cues: he shifts his grip on the phone mid-sentence, glances away briefly on the word Nada, gives a short amused half-laugh, tilts his head slightly. Camera imperfections: slight handheld motion blur, mild overexposure near the window, visible grain, off-center framing, occasional soft focus. Skin: visible pores, slight unevenness in skin tone, minor undereye shadows, hint of shine from natural oils. He never examines or critiques his own reflection. No subtitles, no captions, no text overlays."
}
```

Beat 2 — mesmo payload, trocando só o diálogo:

> "Aí eu fiz uma análise de verdade. Mandei duas selfies, respondi umas perguntas, e recebi um
> plano que faz sentido. Com checklist pra medir."

**Polling (a armadilha):**

```bash
# Seedance vive em ASSETS, não em videos. /v1/videos/{id} devolve 404.
curl -sS -H "Authorization: $ARCADS_BASIC_AUTH" "$BASE/v1/assets/ASSET_ID"
# status: pending -> generated | failed ; mp4 final no campo url
```

---

## 5. Vídeo sem rosto — Sora 2 (o caminho barato)

`sora2` texto puro funciona normalmente — a regressão só atinge entrada de imagem. ~0,05/s.

V5 "Como funciona", 20s ≈ **1,0 crédito**:

```json
{
  "model": "sora2",
  "productId": "PRODUCT_ID",
  "projectId": "PROJECT_ID",
  "aspectRatio": "9:16",
  "duration": 20,
  "resolution": "720p",
  "prompt": "Vertical video, no person's face on screen. Overhead and over-the-shoulder shots of a pair of hands using a smartphone at a wooden desk in daytime window light: taking two quick selfies, tapping through a short questionnaire, then scrolling a clean report screen. Calm, unhurried pacing, three simple shots. A male voiceover speaks in Brazilian Portuguese with a natural São Paulo accent: \"Duas selfies. Qualquer luz, nada profissional. Um questionário de cinco minutos sobre como você se vê. Doze minutos depois, o relatório: o que ajustar, o que manter, e a ordem exata. Não é curso, não é videoaula. É um app. Quarenta e sete reais, com garantia de sete dias.\" Camera imperfections: slight handheld motion, visible grain, shallow depth of field. No subtitles, no captions, no text overlays. No before/after comparison. No numeric score or rating on any screen."
}
```

V6 "10 anos de consultório", 16s ≈ 0,8 crédito — mesmo formato, b-roll de caderno/caneta/mãos
com luz de janela, sem rosto e sem nada identificável de paciente.

**Polling:** Sora 2 fica na família de vídeos → `GET /v1/videos/{id}`, campo `videoStatus`.

---

## 6. B-roll mudo ancorado — Kling 3.0

Único modelo com `startFrame` funcionando. **Mudo.** 15s = 0,7 crédito, mas leva ~250s.
Bom para cortes de apoio entre os beats falados.

```json
{
  "model": "kling-3.0",
  "productId": "PRODUCT_ID",
  "projectId": "PROJECT_ID",
  "duration": 10,
  "startFrame": "FILEPATH_DO_UPLOAD_FRESCO",
  "prompt": "Subtle natural motion from the still: the man shifts his weight slightly, blinks, light from the window flickers gently across his face. Handheld camera micro-movement. Photorealistic, no scene change, no cuts. No subtitles, no captions, no text overlays."
}
```

**Não use `endFrame` no Kling 3.0.** Sozinho, falha depois do create e **cobra créditos**;
junto com `startFrame`, dá 500.

---

## 7. Upload presignado (obrigatório antes de cada referência)

```bash
PRESIGN=$(curl -sS -X POST -H "Authorization: $ARCADS_BASIC_AUTH" \
  -H "Content-Type: application/json" -d '{"fileType":"image/jpeg"}' \
  "$BASE/v1/file-upload/get-presigned-url")

PRESIGN_URL=$(echo "$PRESIGN" | jq -r .presignedUrl)
FILEPATH=$(echo "$PRESIGN" | jq -r .filePath)

curl -sS -o /dev/null -X PUT -H "Content-Type: image/jpeg" \
  --data-binary @hero.jpg "$PRESIGN_URL"
# $FILEPATH serve para UMA chamada só. Refaça o upload para a próxima.
```

Se o lado maior da imagem tiver menos de 1024px, reamostre para 1080px (Lanczos) e converta
para JPEG RGB antes — vários endpoints devolvem `422 The provided image is too small`.

---

## 8. Ordem de gasto recomendada

| Etapa | Modelo | Custo estimado |
|---|---|---|
| 1. V5 "Como funciona" | `sora2` 20s | ~1,0 |
| 2. Seis estáticos de teste | `gpt-image-2` | ~0,2 |
| 3. Character sheet do vencedor | `nano-banana-2` ×10 | ~0,3 |
| 4. **Um** clipe Seedance de teste | `seedance-2.0` 12s | **~576** |
| 5. Série completa (se o teste passar) | `seedance-2.0` ×7 | **~4.000** |

As etapas 1 a 3 custam junto menos de 2 créditos e respondem quase toda a pergunta criativa.
A etapa 4 é onde o dinheiro começa. **Não pule direto para o vídeo com rosto.**

> Estimativas. A Arcads não expõe endpoint de billing — confirme o preço na plataforma antes
> de disparar, e registre o `creditsCharged` real em `logs/arcads-api.jsonl` para as próximas
> estimativas saírem dos seus dados e não desta tabela.
