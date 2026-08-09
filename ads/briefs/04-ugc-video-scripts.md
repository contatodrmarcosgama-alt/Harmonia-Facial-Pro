# UGC video scripts

Seis roteiros, cada um ligado a um ângulo de `01-angles-and-hooks.md` e a um avatar de
`02-avatars.md`. Os payloads prontos da API estão em `05-arcads-prompts.md`.

> **Contrato da API conferido** contra `skills/arcads-external-api/reference.md`. Três achados
> mudam o plano de produção — leia antes de gerar qualquer coisa.

---

## Achado 1 — o `startFrame` do Veo 3.1 está quebrado

`reference.md` (regressão confirmada em 2026-04-09) registra que a entrada de imagem pelo
endpoint v2 retorna **HTTP 500** em quase todos os modelos:

| Modelo | Modo de imagem | Resultado |
|---|---|---|
| `veo31` | `startFrame` | ❌ 500 |
| `sora2` | `referenceImages` | ❌ 500 |
| `grok-video` | `startFrame` | ❌ 500 |
| `kling-3.0` | `startFrame` | ✅ funciona |
| `seedance-2.0` | `referenceImages` | ✅ funciona |

Ou seja: o fluxo "gera o still, aprova, anima no Veo com `startFrame`" **não roda hoje**. Só
existem dois caminhos para travar o rosto do avatar:

- **`seedance-2.0`** com `referenceImages` — fala, áudio, 4–15s. **Único caminho com voz.**
- **`kling-3.0`** com `startFrame` — **mudo**, sem fala nenhuma.

Como todo roteiro aqui tem diálogo, **Seedance 2.0 é o único caminho viável** para os vídeos
com rosto consistente. Rode uma sonda de sanidade por modelo no início da sessão: a regressão
pode ter caído desde a última validação do repo.

## Achado 2 — Seedance 2.0 custa ~48 créditos/segundo

`reference.md` linha 141, revalidado em 2026-05-19 sobre 8 execuções de produção:

| Duração | Créditos estimados |
|---|---|
| 8s | ~384 |
| 10s | ~480 |
| 12s | ~576 |
| 15s | **~720** |

Áudio ligado **não** muda o preço. Compare com os outros:

| Modelo | 15s aprox. | Fala? |
|---|---|---|
| Grok Video | ~0,41 | ❌ |
| Kling 3.0 | ~0,7 | ❌ |
| Veo 3.1 (auto ~8s) | 1,0 fixo | ✅ |
| **Seedance 2.0 i2v** | **~720** | ✅ |

Não é erro de digitação — são três ordens de grandeza. Uma tabela mais antiga no mesmo arquivo
(linha 177) ainda diz "0,06/seg"; a nota de maio corrige explicitamente esse número e diz que
o `MASTER_CONTEXT.md` estava certo o tempo todo. **Use ~48/seg e confirme na plataforma
Arcads antes de disparar** — a skill exige mostrar o custo estimado e esperar confirmação.

Consequência prática: um único UGC de 15s com rosto travado custa mais que centenas de
imagens estáticas (Nano Banana ≈ 0,03). **Valide o ângulo em estático antes de gastar em
vídeo.**

## Achado 3 — Seedance cobra antes do content checker

Créditos são debitados **no create**, antes da checagem de conteúdo. Se o prompt for
sinalizado, o asset vira `failed` e **os créditos não voltam**. Numa oferta de aparência isso
é risco real: nada de linguagem sobre defeito facial, correção, ou comparação antes/depois nos
prompts. Se der `failed` na primeira, **não repita o mesmo payload** — suavize o texto antes.

## Armadilha de polling

Seedance 2.0 é criado em `/v2/videos/generate` mas **vive na família de assets**. Polling em
`GET /v1/videos/{id}` devolve **404**. Use `GET /v1/assets/{id}` e leia `status`. O mp4 final
sai no campo `url` do asset.

## Uploads presignados são de uso único

Um `filePath` funciona **uma vez**. Reusar devolve `400 REFERENCE_FILE_NOT_FOUND`. Para
ancorar o mesmo hero still em vários clipes, **refaça o upload antes de cada chamada**.

---

## Roteamento final

| Necessidade | Modelo | Observação |
|---|---|---|
| Talking head com rosto travado | **`seedance-2.0`** + `referenceImages` + `audioEnabled: true` | Único caminho com voz. ~48 cr/s |
| Voz sem rosto específico (locução, mãos, tela) | **`veo31`** texto puro | 1,0 crédito fixo, ~8s, ~67s de geração |
| Locução mais longa sem rosto | **`sora2`** texto puro | até 20s, ~0,05/s |
| B-roll mudo com still ancorado | **`kling-3.0`** + `startFrame` | 15s = 0,7 crédito, mudo |
| Still de personagem / anúncio estático | `POST /v2/images/generate`, `nano-banana-2` | ~0,03, ~35s |

Seedance **não aceita** `startFrame` — a imagem entra por `referenceImages` (máx. 3). E
`referenceImages` + `referenceVideos` na mesma chamada dá 500: escolha um modo.

**Aspect ratio:** Seedance só aceita `9:16` e `16:9`. Não há `1:1` em vídeo.

---

## Orçamento de fala por clipe

~2,5 palavras/segundo. Seedance vai até 15s, então **o teto é ~35 palavras por clipe**. Os
roteiros abaixo já vêm quebrados em beats que cabem — cada beat é uma chamada de API separada,
depois costurada com `ffmpeg`.

Blocos obrigatórios em todo prompt de vídeo:

```
No subtitles, no captions, no text overlays.
Speaking Brazilian Portuguese, natural São Paulo accent.
Camera imperfections: slight motion blur, mild overexposure near the window,
visible grain, off-center handheld framing, occasional soft focus.
Skin: visible pores, slight unevenness in skin tone, minor undereye shadows,
hint of shine from natural oils.
```

Mais 3–4 marcações de movimento humano por prompt, ou o sujeito vira manequim.

---

## V1 — "A reunião" (Ângulo 1, avatar A1 Rafael)

Dois clipes Seedance de 12s. ~28 palavras cada. Custo estimado: **~1.152 créditos**.

**Beat 1 — [HOOK] (12s, ~27 palavras)**

> Ontem eu falei numa reunião inteira. A conversa continuou como se eu não tivesse falado.
> Não é que me ignoram. É que ninguém repara.

**Beat 2 — [CTA] (12s, ~29 palavras)**

> Achei um app que analisa duas selfies e devolve um relatório com o que dá pra aprimorar e em
> que ordem. Doze minutos. Link aqui embaixo.

Cena: sentado, plano médio, escritório desfocado ao fundo. Movimento: desvia o olhar em
"ninguém repara", pequeno dar de ombros, inclina pra frente no CTA.

---

## V2 — "Cegueira da Harmonia" (Ângulo 2, avatar A3 Marcelo)

Dois clipes de 11s. Custo estimado: **~1.056 créditos**.

**Beat 1 — [HOOK] (11s, ~25 palavras)**

> Existe um nome pro motivo de você não conseguir olhar pro próprio rosto. Chama Cegueira da
> Harmonia. Você convive com esse rosto há trinta anos.

**Beat 2 — [MECANISMO + CTA] (11s, ~26 palavras)**

> Você perdeu a capacidade de ver ele de fora. Por isso o espelho não ajuda. Esse app dá o
> olhar de fora em doze minutos.

Cena: bancada da cozinha, luz da manhã, apoiado. Movimento: gesto único em "de fora",
inclinação de cabeça no nome do mecanismo, quebra de contato visual no meio da frase.

---

## V3 — "Oito meses de mewing" (Ângulo 3, avatar A2 Diego)

O de maior intenção. Dois clipes de 12s. Custo estimado: **~1.152 créditos**.

**Beat 1 — [HOOK] (12s, ~28 palavras)**

> Oito meses fazendo mewing. Sabe o que eu consigo te falar sobre o resultado? Nada. Eu tava
> seguindo vídeo de gringo aleatório, sem saber se servia pro meu rosto.

**Beat 2 — [CTA] (12s, ~27 palavras)**

> Aí eu fiz uma análise de verdade. Mandei duas selfies, respondi umas perguntas, e recebi um
> plano que faz sentido. Com checklist pra medir.

Cena: celular na mão, espelho do banheiro, manhã. **Direção:** ele está irritado com o tempo
perdido, nunca com o rosto. Não deixe o modelo examinar o próprio reflexo criticamente — isso
transforma o anúncio em acusação de defeito e ainda aumenta o risco no content checker.

---

## V4 — "A mentira educada" (Ângulo 4, avatar A1 Rafael)

Dois clipes de 11s. Custo estimado: **~1.056 créditos**.

**Beat 1 — [HOOK] (11s, ~26 palavras)**

> Você já pediu opinião sincera sobre a sua aparência e ouviu "você é bonito do seu jeito"?
> Isso não é resposta. É gentileza.

**Beat 2 — [CTA] (11s, ~27 palavras)**

> Ninguém fala a verdade porque falar tem custo. Um relatório não tem esse problema. Doze
> minutos, sem julgamento e sem nota.

Cena: banco do motorista, carro parado, luz do para-brisa. Movimento: olha o retrovisor,
ajusta a postura, pausa breve antes do CTA.

---

## V5 — "Como funciona" (Ângulo 5, sem rosto)

**Não precisa de avatar** → sai de Seedance e vai para **`sora2` texto puro, 20s**. Custo
estimado: **~1,0 crédito**. É literalmente 1.000× mais barato que os roteiros com rosto.

> Duas selfies. Qualquer luz, nada profissional. Um questionário de cinco minutos sobre como
> você se vê. Doze minutos depois, o relatório: o que ajustar, o que manter, e a ordem exata.
> Não é curso, não é videoaula. É um app. Quarenta e sete reais, com garantia de sete dias.

(~48 palavras → 20s no enum do Sora 2.)

Cena: plano aéreo e por cima do ombro, mãos no celular, mesa, luz do dia. Só locução.

**Comece por aqui.** É o roteiro mais barato, o mais seguro no content checker (não faz
nenhuma afirmação emocional) e o mais provável de durar como evergreen.

---

## V6 — "10 anos de consultório" (Ângulo 6, sem rosto de IA)

`sora2` texto puro, 16s, locução sobre b-roll. Custo estimado: **~0,8 crédito**.

> Dez anos fazendo harmonização facial e análise de simetria. No consultório era sempre o
> mesmo padrão: cara jovem, perdido em informação contraditória, tentando coisa aleatória. Ele
> transformou os critérios da prática clínica num sistema.

(~38 palavras → 16s.)

Cena: b-roll não identificável — caderno, caneta, mãos, luz de janela. Nunca fotografia de
paciente. Se houver imagem liberada do próprio Dr Gama, use ela: vai performar melhor.

---

## Ordem de produção (ajustada ao custo real)

1. **V5 primeiro.** Sem avatar, ~1 crédito, no ar hoje.
2. **Estáticos** (`03-image-ads.md`) para descobrir qual ângulo tem tração — ~0,03 cada.
3. **Só então** monte as character sheets (`02-avatars.md`) do ângulo vencedor.
4. Gere o hero still, **aprove**, e produza **um** clipe Seedance de teste antes de fechar a
   série inteira. ~576 créditos é caro demais para descobrir problema de direção no clipe 6.
5. Costure os beats com `ffmpeg`, queime legendas com a skill `caption-video`.
6. Publique via `meta-ad-builder` — todo anúncio nasce PAUSADO.

## Portões obrigatórios da skill

A skill exige, antes de qualquer geração:

- **Portão de diálogo** — apresentar as falas numeradas por beat e esperar `yes` explícito.
- **Portão de custo** — mostrar o total estimado com a fonte, e esperar confirmação.
- **Pasta da sessão** — criar/reusar `Arcads API - YYYY-MM-DD` e passar `projectId` em tudo.
- **Log** — anexar cada chamada em `logs/arcads-api.jsonl` (sem prompt completo, sem chaves).

## Checagem de conformidade antes de publicar

- [ ] Nenhum antes/depois em nenhum frame
- [ ] Nenhuma nota ou score dito ou mostrado
- [ ] Nenhuma frase que afirme defeito no espectador
- [ ] Nenhuma promessa de resultado físico ou prazo
- [ ] Legendas em pt-BR com acentuação correta
- [ ] Nenhuma foto de paciente ou material clínico real
