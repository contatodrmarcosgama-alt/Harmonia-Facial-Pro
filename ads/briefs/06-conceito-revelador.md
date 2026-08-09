# Conceito "Cegueira → Revelação"

O vídeo traduz o mecanismo da própria copy. Escuridão total = a **Cegueira da Harmonia**.
Linhas douradas que se desenham sozinhas e travam em simetria = o **Revelador de Potencial**.
Fecha em espaço negativo no terço inferior — exatamente onde entra o texto na pós.

**Sem rosto humano, sem antes/depois, sem nota.** É o conceito mais seguro de todo o pacote em
compliance: não há espectador a quem atribuir defeito, não há comparação, não há score. As três
restrições que mais derrubam conta nessa categoria simplesmente não têm onde encostar aqui.

---

## Por que "no text" na geração

Modelo de vídeo erra tipografia. Você perde o 4K num letreiro torto, e em pt-BR o erro é pior
— acento comido (`Voce`, `R47`) mata a credibilidade na hora. Todos os prompts abaixo carregam
uma cláusula de negação de texto explícita e redundante.

O terço inferior sai limpo de propósito. O texto entra na pós:

```
HARMONIA FACIAL PRO
Desvende o potencial único do seu rosto.
R$47
```

**Spec do terço inferior:** área livre garantida dos 66% aos 100% da altura. Em 9:16 a 1080×1920
isso é a faixa de y=1267 até y=1920. Deixe 120px de margem inferior para a UI do Reels/Stories
e mais 80px laterais. Área útil real: 920×533px.

---

## Arco em 4 beats

| Beat | Tempo (15s) | O que acontece |
|---|---|---|
| 1 — Cegueira | 0–3s | Preto absoluto. Só poeira suspensa captando um resto de luz. Quase nada. |
| 2 — O traço começa | 3–8s | Primeiras linhas douradas se desenham sozinhas, hesitantes, incompletas. |
| 3 — Trava | 8–12s | As linhas encontram os eixos, se completam e **travam** em simetria. Pulso de brilho. |
| 4 — Respiro | 12–15s | Assenta. Câmera para. Terço inferior limpo, esperando o texto. |

Em 12s, corte o beat 4 para 2s. Abaixo de 10s o conceito não respira — não vale.

---

## Prompt de vídeo (mestre)

Serve para Seedance 2.0, Veo 3.1, Sora 2 e Kling. Texto único, um parágrafo, sem sopa de
palavras-chave — como a skill exige.

```
Absolute darkness fills the frame, a deep near-black void with only faint suspended dust
catching a trace of warm light. Slowly, delicate luminous golden lines begin to draw
themselves out of the blackness, stroke by stroke, as if an unseen hand were tracing the
proportional axes and contours of a face — a thin architectural wireframe, like a
constellation or an architect's drafting overlay, never a photograph and never a real face.
The strokes are hesitant and incomplete at first, some dissolving back into the dark. Then
they find their axes, complete themselves, and lock into perfect bilateral symmetry with a
soft pulse of light. Warm gold tones, deep amber into pale champagne, subtle bloom, gentle
lens glow, fine particulate haze drifting through the beam. The geometry occupies the upper
two thirds of the frame and settles there, calm and balanced. The entire lower third of the
frame remains pure empty black negative space, completely clean and unobstructed for the
whole shot. Camera is nearly static with a slow, almost imperceptible push in, coming to
rest. Cinematic, premium, minimal, extremely high contrast. No text, no letters, no numbers,
no digits, no typography, no captions, no subtitles, no watermark, no logo, no user
interface, no measurement labels, no readouts, no scores or ratings of any kind, no human
skin, no photographic face.
```

**Cláusula de compliance embutida:** `no scores or ratings of any kind` e `no photographic
face` não são decoração. Uma malha dourada sobre rosto fotográfico lê como scan de avaliação
facial — contradiz "sem scores, sem julgamentos" e é exatamente o tipo de visual que o Meta
restringe nessa categoria. Mantenha abstrato.

---

## Payloads — Arcads

Precisa de `.env` com `ARCADS_API_KEY`. Rode `./scripts/setup.sh` primeiro.

### Opção A — Sora 2, 16s (recomendada para começar: ~0,8 crédito)

Sem rosto para travar, então **não precisa de Seedance**. Texto puro funciona e custa ~1/900
do Seedance.

```json
{
  "model": "sora2",
  "productId": "PRODUCT_ID",
  "projectId": "PROJECT_ID",
  "aspectRatio": "9:16",
  "duration": 16,
  "resolution": "1080p",
  "prompt": "<PROMPT MESTRE ACIMA>"
}
```

Poll: `GET /v1/videos/{id}`, campo `videoStatus`.

### Opção B — Veo 3.1, ~8s (1,0 crédito fixo, melhor qualidade de luz)

Sem campo `duration` — ele decide (~8s). Bom se você quiser o beat 2+3 apenas e cortar o resto
na pós. Resolução até `4K`.

```json
{
  "model": "veo31",
  "productId": "PRODUCT_ID",
  "projectId": "PROJECT_ID",
  "aspectRatio": "9:16",
  "resolution": "4K",
  "prompt": "<PROMPT MESTRE ACIMA>"
}
```

### Opção C — Kling 3.0, 15s (0,7 crédito, o mais barato longo)

Mudo, mas este conceito **não tem fala** — a trilha entra na pós. Kling é a melhor relação
custo/duração aqui.

```json
{
  "model": "kling-3.0",
  "productId": "PRODUCT_ID",
  "projectId": "PROJECT_ID",
  "duration": 15,
  "prompt": "<PROMPT MESTRE ACIMA>"
}
```

> **Não use Seedance 2.0 neste conceito.** ~48 créditos/s = ~720 num clipe de 15s, e a única
> vantagem dele (fala + rosto travado) não é usada aqui. Seria pagar 900× a mais por nada.

---

## Payloads — Morphix (se o Arcads não estiver configurado)

Mesmo prompt mestre. Modelos disponíveis no servidor conectado:

| Objetivo | Modelo | Parâmetros |
|---|---|---|
| Melhor luz / volumetria | `google/veo-3.1` | `duration: 15`, `aspectRatio: "9:16"`, `resolution: "4k"`, `audio: "off"` |
| Barato e rápido | `google/veo-3-fast` | `duration: 10`, `9:16`, `1080p` |
| Alternativa de textura | `kwaivgi/kling-v2.5-turbo-pro` | `duration: 10`, `9:16`, `1080p` |
| Movimento suave de linhas | `wan-video/wan-2.6-t2v` | `duration: 15`, `9:16`, `1080p` |

`audio: "off"` em todos — a trilha entra na pós junto com o texto.

---

## Key visual estático (mesmo conceito, para os estáticos)

`POST /v2/images/generate` no Arcads (`gpt-image-2` ou `nano-banana-2`), ou `generate_image`
no Morphix (`black-forest-labs/flux-2-max`, `google/nano-banana-pro`).

Formatos: `9:16` (Stories/Reels), `1:1` (feed), `4:5` só via Morphix — o Arcads não tem 4:5,
gere `1:1` e recorte.

```
Extreme darkness, a near-black void filling the frame. Emerging from that darkness, delicate
luminous golden lines trace the abstract proportional axes and contours of a face — a thin
architectural wireframe, like a constellation or an architect's drafting overlay, elegant and
precise, never a photograph. The line work is caught mid-draw, some strokes still incomplete
and dissolving into the black. Warm gold light, deep amber into pale champagne, with subtle
bloom, soft lens glow and fine particulate haze catching the light. The geometry sits in the
upper two thirds of the frame, calm and perfectly symmetrical, locked and balanced. The entire
lower third is pure empty black negative space, completely clean and unobstructed. Cinematic,
premium, minimal, extremely high contrast, shallow depth of field. Absolutely no text, no
letters, no numbers, no digits, no typography, no watermark, no logo, no user interface, no
measurement labels, no scores or ratings of any kind.
```

**Variações que valem testar** (troque só a frase do meio):

1. **Constelação** — `the golden lines connect through small bright nodes, like a star chart`
2. **Blueprint** — `the lines read as a precise technical blueprint in gold on black`
3. **Único traço** — `a single continuous unbroken golden line describes the whole structure`

A 3 costuma ser a mais elegante e a que menos sofre com artefato de linha quebrada.

---

## QA antes de aprovar qualquer render

- [ ] **Terço inferior 100% limpo** — nenhuma linha, brilho ou partícula invadindo
- [ ] **Zero texto** em qualquer canto do frame (é a falha mais comum)
- [ ] Nenhum dígito ou marca de medição que possa ler como nota
- [ ] Nenhuma pele ou rosto fotográfico — só geometria
- [ ] Simetria realmente trava no fim; se as linhas continuam tremendo, regenere
- [ ] Preto real (não cinza lavado) — o conceito depende do contraste

Cap de 2 regenerações por render, conforme a skill. Se passar disso, o prompt é que está
errado — não o modelo.

---

## Pós-produção

1. Importe o render. Corte no ponto em que a simetria trava + ~2s de respiro.
2. Texto no terço inferior, dentro da área útil (920×533 em 9:16 a 1080p):
   - `HARMONIA FACIAL PRO` — sans-serif, peso 800, tracking largo, branco puro
   - `Desvende o potencial único do seu rosto.` — peso 400, cinza claro, corpo menor
   - `R$47` — peso 700, dourado puxado do próprio render
3. Fade-in do texto **depois** do lock da simetria, nunca antes — o texto é a resposta que o
   visual acabou de fazer a pergunta.
4. Trilha: drone grave subindo, com um único acento no lock. Sem locução.
5. Exporte 1080×1920 H.264, e uma versão 1:1 recortada do centro para o feed.

---

## Status

Nada deste conceito foi gerado ainda. Os dois caminhos estavam bloqueados no momento em que
este arquivo foi escrito:

- **Arcads** — sem `.env`, rode `./scripts/setup.sh` com sua chave.
- **Morphix** — as chamadas MCP voltaram `requires approval`; é preciso autorizar o servidor.

Assim que um dos dois abrir, os payloads acima estão prontos para disparar sem edição.
