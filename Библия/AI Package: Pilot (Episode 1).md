# AI Package: Pilot (Episode 1)

This AI Package provides prompts and notes for generating the keyframes and video shots described in
the Shot List. For each shot we define a GPT Image prompt (to create a still frame reference), a
negative prompt (to guide the model away from undesired elements), an animation prompt (to animate the
shot from the reference), continuation notes for linking shots, motion instructions, a continuity
checklist and rendering notes. Prompts focus on the DreamWorks-style 3D animated look established in
the character reference sheets (Визуализации/), consistent character appearance and adherence to the
Visual Bible.

**Одна модель для видео (Kling 3.0 Standard) + локальная постпродакшн-озвучка для шотов с репликой:**

- **Все шоты генерируются в Kling 3.0 Standard**, `sound: on`. Для шотов, где персонаж говорит на
  камеру, реплика вписывается в промпт **прямо на русском, в кавычках** (не «he speaks softly», а
  буквальная цитата) — это заставляет Kling анимировать настоящее открытие рта в такт речи. Озвучка,
  которую Kling сочиняет сама под эту цитату, звучит как тарабарщина (не настоящий язык) — это ожидаемо
  и не страшно, потому что её всё равно заменяют в посте.
- **Постпродакшн (локально, ffmpeg, без AI):** генерируем реальную реплику через `generate_audio`
  зафиксированным голосом (Caspian/Sienna — см. Character Bible → «Голос»), затем накладываем её на
  видео вместо тарабарской дорожки Kling. Полный рецепт — в разделе «✅ Липсинк решён» в конце документа.
  Проверено и подтверждено на шоте 3.

## Conventions

- Characters: Vanessa has long dark wavy hair, emerald-green eyes, an "old money" wardrobe over a
  DreamWorks-style 3D animated design (see her reference sheet — signature gold pendant with a green
  stone); Leo has russet/blond wavy hair, bright blue eyes and a calm, confident demeanour (see his
  reference sheet — dark minimalist wardrobe, leather watch strap). Their appearances must match the
  character reference sheets exactly.

- Environment: The balcony scene is set at night with a view of Moscow's lights; the kitchen scene is
  modern and bright.

- Style: DreamWorks-style 3D animated feature look — expressive but semi-realistic character
  proportions, soft skin subsurface-scattering shading, detailed hair grooming, physically based
  materials (fabric, leather, glass, brass), cinematic 3D lighting, shallow depth of field for
  close-ups, virtual handheld camera feel.

- Negative prompt keywords: avoid photorealistic/live-action rendering, avoid flat toon-shading or
  chibi/comedic proportions, avoid exaggerated slapstick expressions, avoid plastic/waxy skin, avoid
  unrealistic lighting.

- Жесты и язык тела: во все промпты с персонажами вплетены фирменные жесты из Character Bible (у Лео —
  медленное моргание как «забота», контроль пространства лёгкими касаниями, руки в карманах/за спиной,
  наклон головы при доминировании; у Ванессы — касание кольца/волос при тревоге, руки близко к телу,
  отсутствие этих жестов как сознательный акцент в переломные моменты). Это не отдельный слой — жесты
  прописаны прямо внутри Kling-промптов ниже.

## Модель и режим ввода по шотам

Все шоты — **Kling 3.0 Standard**, `sound: on`. Различается только кадры (первый / первый+последний) и
нужен ли постпродакшн-этап замены звука.

| Шот | Кадры | Постпродакшн-озвучка нужна? | Почему |
|---|---|---|---|
| 1 | первый | нет | establishing, без реплик |
| 2 | первый | нет | Ванесса одна, без реплик |
| **3** | **первый + последний** | **да** | Лео говорит + передаёт кружку — проверено и подтверждено (см. «✅ Липсинк решён») |
| **4** | первый | **да** | двухкадр, реплики обоих персонажей подряд — мультиспикерный, см. примечание ниже |
| **5** | первый | **да** | крупный план Лео, один говорящий |
| **6a** | первый | **да** | крупный план Ванессы, один говорящий («Правда?») |
| **6b** | первый | **да** | крупный план Лео, один говорящий — реплика теперь физически в кадре, не закадрово |
| **6c** | первый | **да** | крупный план Ванессы, один говорящий («...Хорошо.») |
| 7 | первый + последний | нет | инсерт кружек, смена света ночь→рассвет, без реплик |
| 8 | первый + последний | нет | отъезд камеры к кухне, без реплик в этом шоте |
| **9** | первый | **да** | двухкадр, реплики обоих персонажей подряд — мультиспикерный |
| **10** | первый | **да** | крупный план Ванессы, один говорящий |
| **11** | первый | **да** | крупный план Лео, один говорящий |
| **12** | первый | **да** | крупный план Ванессы, один говорящий |
| 13 | первый | нет | реакция Лео без реплики |
| **14** | **первый + последний** | нет | реакция Ванессы без реплики, нужен опорный кадр взгляда вниз |
| 15 | первый | нет | финальный инсерт, без реплик |

**Шот 6 разбит на три под-шота (6a/6b/6c)** — раньше это был один мультиспикерный кадр на Ванессе с
закадровой репликой Лео; теперь Лео физически в кадре для своей реплики, и каждый под-шот — чистый
одноголосый случай, как 5/10/11/12.

**Мультиспикерные шоты (4, 9).** С новым пайплайном это менее рискованно, чем казалось с Wan 2.7:
раз замена звука идёт в посте по обнаруженным сегментам речи (см. «✅ Липсинк решён»), для шотов с
несколькими репликами подряд нужно просто найти в тарабарской дорожке Kling **несколько** отрезков
речи (а не один) и наложить на каждый свою реплику нужным голосом — тот же `silencedetect`, применённый
к каждому сегменту отдельно. Не протестировано на реальном многоречевом шоте, но принцип тот же, что
уже подтверждён на шоте 3.

## Shot-by-Shot Prompts

## Shot 1 – Establishing Shot (Balcony)

- GPT Image prompt: "Wide establishing shot of a modern Moscow high-rise balcony at night, rendered in
  DreamWorks-style 3D animation. City lights shimmer in the distance. The balcony railing and table
  with a candle are silhouetted. 35 mm virtual lens, cinematic 3D animated lighting, deep blue night
  sky, warm candle glow, clean stylized render with soft global illumination."

- Negative prompt: "No photorealism, no live-action look, no cartoonish/chibi proportions, no HDR
  over-glow, no futuristic skyscrapers, no people in frame, no flat toon shading."

- Kling 3.0 Standard prompt: "Start with the still frame of the wide balcony at night, DreamWorks-style 3D animation.
  Hold for a moment, then slowly pan right to reveal more of the skyline. Maintain a 35 mm virtual lens
  perspective and keep the candle flicker and city lights. Duration 4 s."

- Continuation: This shot fades into the medium shot of Vanessa (Shot 2) with a simple cut.

- Motion notes: Pan is smooth and slow; no zooming. Camera is on a virtual tripod.

- Continuity checklist: Verify night sky tone; candle present; no characters; matching skyline with
  World Bible; render style matches Visual Bible (no film grain, no photoreal skin).

- Rendering notes: Clean 3D animated render, no film grain or LUT emulation. Resolution 1920×1080
  (vertical crop in post). Keep shadows soft and colour temperature cool.

## Shot 2 – Vanessa Medium (Balcony)

- GPT Image prompt: "Medium shot of Vanessa, DreamWorks-style 3D animated character, standing at a
  balcony railing at night. Long dark wavy hair, emerald-green eyes, elegant old-money coat draped
  around her shoulders, matching her character reference sheet. Warm candlelight illuminates her
  profile while cool blue city lights rim her hair. 50 mm virtual lens, cinematic 3D animated
  lighting."

- Negative prompt: "No photorealistic skin, no exaggerated comedic poses, no heavy stylised makeup
  beyond her reference sheet, no futuristic outfits, no flat studio lighting."

- Kling 3.0 Standard prompt: "Begin with the reference image of Vanessa gazing at the city, DreamWorks-style 3D
  animation. Use a virtual handheld push-in towards her over 4 seconds, capturing the subtle movement
  of her hair in the night breeze. Her hands hold the blanket close around her shoulders; her fingers
  occasionally touch the ring on her hand — a small, unconscious nervous habit. Maintain 50 mm virtual
  lens and shallow depth of field; candle and city lights should flicker naturally."

- Continuation: Seamlessly cut to shot 3 as Leo enters. Vanessa maintains position and gaze.

- Motion notes: Handheld sway mimics breathing. Ensure push-in speed is constant. Ring-touch gesture is
  small and unhurried — a habit, not a performed action (per Character Bible).

- Continuity checklist: Vanessa's hair down and coat draped correctly; candle remains lit; city lights
  consistent with Shot 1; design matches her reference sheet (pendant, hair, eye colour).

- Rendering notes: Maintain clean stylized render; preserve highlight roll-off; no sudden brightness
  shifts.

## Shot 3 – Leo Entrance (Balcony)

- GPT Image prompt: "Medium shot of Leo, DreamWorks-style 3D animated character, carrying two mugs
  stepping out onto a balcony at night, his face openly warm — a genuine, unguarded smile as he looks
  toward Vanessa, eyes soft with real affection. Russet/blond wavy hair, bright blue eyes, dark
  minimalist sweater, matching his character reference sheet. The railing and a small table are visible;
  the city skyline glows behind him. 50 mm virtual lens, warm candlelight, cinematic 3D animated
  lighting."

- Negative prompt: "No smirking/villain caricature, no exaggerated swagger, no plastic/waxy skin, no
  futuristic clothing, no photoreal rendering."

- **Kling input: первый + последний кадр, `sound: on`.** Последний кадр = стартовый кадр шота 4
  (двухкадр, оба уже держат свою кружку, тёплый свет, город в боке) — так финал шота 3 гарантированно
  совпадает с началом шота 4, без произвольной мизансцены. Реплика Лео вписана в промпт напрямую в
  кавычках — Kling 3.0 сама генерирует голос под неё и синхронизирует рот (родной `sound: on`).
  Сгенерированная Kling озвучка звучит как тарабарщина (ожидаемо) — её заменяют на реальный TTS голосом
  «Caspian» в постпродакшне. **✅ Протестировано и подтверждено:** речь в тарабарской дорожке Kling
  началась на 4.3 с (не с начала клипа — до этого Лео молча идёт от двери); реальная TTS-реплика длиннее
  оставшегося до конца клипа времени, поэтому её ускорили на ~9% (`atempo`), а не растянули видео
  замороженным кадром — заморозка кадра в анимации выглядит как баг. Полный рецепт со значениями — в
  разделе «✅ Липсинк решён» в конце документа.

- Kling 3.0 Standard prompt: "Leo enters from the apartment doorway onto the balcony at night,
  DreamWorks-style 3D animation. He says: 'Замёрзла? Я по тишине понял, что ты здесь. Ты всегда
  затихаешь, когда думаешь.' The camera (virtual steadicam) follows him in a smooth arc towards Vanessa
  as he speaks, his face visibly warm and affectionate, eyes crinkled with genuine tenderness as he
  looks at her. As he reaches her, he extends one of the two mugs toward her with his hand and she
  reaches out and takes it into her own hand — a clear, deliberate physical handoff, both hands visible
  at the moment of exchange. Leo keeps the second mug in his other hand. Right after the handoff, his
  free hand rests briefly on the railing beside her or lightly at her shoulder — his familiar, quiet way
  of controlling shared space. The handoff completes near the end of the shot, after his line finishes.
  Use a 50 mm virtual lens with shallow depth of field; keep the candle flicker and city backdrop.
  Duration 7 s."

- Continuation: Leads into shot 4 where Leo stands beside Vanessa, each already holding their own mug
  following the handoff completed in this shot.

- Motion notes: Smooth steadicam; slight parallax as camera arcs around the balcony table. The mug
  handoff should read as an unhurried, natural gesture, not a quick or fumbled motion. His touch after
  the handoff is light and brief, not proprietary or heavy (per Character Bible: controls space through
  small touches, not obvious gestures).

- Continuity checklist: Both mugs should be identical; the handoff must be visibly completed by the end
  of the shot (mug physically passes from Leo's hand to Vanessa's, not swapped between frames); Leo's
  hair neat; clothing matches Character Bible and reference sheet; city view matches previous shots.

- Rendering notes: Balanced exposure; warm tones on faces; cool bokeh in background.

## Shot 4 – Two-Shot (Balcony)

- GPT Image prompt: "Two DreamWorks-style 3D animated characters, Vanessa and Leo, stand side by side
  on a balcony at night, each holding a mug. Leo gazes at Vanessa with unmistakable warmth and
  adoration, his eyes soft and fully focused on her; she looks down with a shy smile that visibly
  reaches her eyes, clearly pleased. Warm candlelight illuminates their faces while the Moscow skyline
  blurs behind them. 50 mm virtual lens, cinematic 3D animated lighting."

- Negative prompt: "No dramatic backlighting, no glamorous fashion beyond reference sheets, no visible
  rig/skeleton artifacts, no lens flares, no photoreal skin."

- **Kling input: первый кадр, `sound: on`.** Мультиспикерный шот — постпродакшн заменяет звук по двум
  найденным сегментам речи (см. «Мультиспикерные шоты» выше и «✅ Липсинк решён»). Реальные реплики:
  Ванесса — «Я не знала, что это слышно.» (голос «Sienna»); Лео — «Мне — слышно. Я слышу тебя, даже
  когда ты молчишь.» (голос «Caspian»).

- Kling 3.0 Standard prompt: "Start from the reference image of both characters on the balcony,
  DreamWorks-style 3D animation. Perform a slow dolly inwards for 4 s while the characters take small
  sips and exchange glances. Vanessa speaks first, quietly: 'Я не знала, что это слышно.' She stays
  still and listening the rest of the time. Leo then answers, warmly: 'Мне — слышно. Я слышу тебя, даже
  когда ты молчишь.' — his face open and visibly warm as he says it, eyes soft on her. Leo stands with
  easy, upright confidence, one hand loosely in his pocket; Vanessa holds her mug with both hands, close
  to her body, her own smile clearly readable, pleased and a little shy. Keep a 50 mm virtual lens;
  handheld breathing motion. Warm tones should dominate the foreground with cool bokeh in the
  background."

- Continuation: Cuts to close-ups (shots 5–6) to emphasise dialogue and emotion.

- Motion notes: Dolly speed slow; maintain equal distance to both characters. Posture contrast is
  deliberate — his open, confident stance versus her more contained, self-holding one (per Character
  Bible body-language notes).

- Continuity checklist: Both mugs remain nearly full; candle stays on table; hair, wardrobe consistent
  with reference sheets; skyline unchanged.

- Rendering notes: Ensure natural skin shading per reference sheets; keep depth of field shallow;
  maintain clean stylized render.

## Shot 5 – Close-up on Leo (Balcony)

- GPT Image prompt: "Close-up of Leo, DreamWorks-style 3D animated character, speaking softly at night,
  openly and visibly besotted — eyes shining with real tenderness, a soft unguarded smile, matching and
  pushing further into his reference sheet's 'влюбленный' emotion pose. Russet/blond wavy hair, bright
  blue eyes. Warm candlelight illuminates his features; the background is a dark bokeh of city lights.
  85 mm virtual lens, shallow depth of field, cinematic 3D animated lighting."

- Negative prompt: "No harsh shadows, no over-sharpening, no unnatural eye reflections, no
  photorealistic skin pores."

- **Kling input: первый кадр, `sound: on`.** Один говорящий в кадре — чистый случай для постпродакшн-
  озвучки. Реальная реплика: Лео — «Помнишь, как мы только познакомились? Я тогда сразу понял — вот она,
  моя муза.» (голос «Caspian»).

- Kling 3.0 Standard prompt: "Hold the close-up of Leo delivering his line, DreamWorks-style 3D
  animation. He says: 'Помнишь, как мы только познакомились? Я тогда сразу понял — вот она, моя муза.' —
  his eyes visibly shining with warmth as he speaks, the tenderness openly readable on his whole face,
  not just implied. He blinks slowly and deliberately as he speaks — his familiar 'caring listener'
  mannerism. The camera remains static with micro-jitters to emulate handheld. Maintain an 85 mm virtual
  lens; ensure the light source flickers subtly on his face."

- Continuation: After his line, cut to shot 6a for Vanessa's reaction.

- Motion notes: Micro-jitters only; no rack focus. The slow blink should read as warm, not sleepy or
  theatrical — per Character Bible, it's what makes him seem like a "caring" listener.

- Continuity checklist: Leo's stubble/hair as per Character Bible and reference sheet; consistent
  background bokeh; candle light warm.

- Rendering notes: Maintain clean render with soft subsurface skin shading; maintain warm midtones.

## Shot 6a – Close-up on Vanessa, the Question (Balcony)

Раньше шот 6 был одним мультиспикерным кадром на Ванессе, а реплика Лео звучала закадрово — физически
неправдоподобно и требовало разделять два голоса на одной аудиодорожке в посте. Разбит на три чистых
одноголосых под-шота (6a/6b/6c): Лео теперь физически в кадре для своей реплики.

- GPT Image prompt: "Close-up of Vanessa, DreamWorks-style 3D animated character, listening intently at
  night, her face visibly lighting up with hope, eyes bright and open as she asks a question. Dark wavy
  hair, emerald-green eyes. Warm candlelight highlights her features; cool city lights rim the frame.
  85 mm virtual lens, cinematic 3D animated lighting."

- Negative prompt: "No tears, no cinematic bloom, no lens distortion, no photoreal rendering."

- **Kling input: первый кадр, `sound: on`.** Один говорящий в кадре — чистый случай. Реальная реплика:
  Ванесса — «Правда?» (голос «Sienna»).

- Kling 3.0 Standard prompt: "Hold the close-up of Vanessa, DreamWorks-style 3D animation. She asks
  softly, hope visibly lighting up her face: 'Правда?' Her eyes stay bright and open, genuinely hopeful.
  Camera static with subtle handheld sway. Maintain 85 mm virtual lens and shallow depth of field."

- Continuation: Cut to shot 6b as Leo answers, now in frame.

- Motion notes: Slight breathing movement; ensure eyes stay in focus.

- Continuity checklist: Hair parting consistent with reference sheet; jewellery (pendant) visible;
  candlelight flicker.

- Rendering notes: Balanced highlights; maintain warm key light and cool rim.

## Shot 6b – Close-up on Leo, the Answer (Balcony)

- GPT Image prompt: "Close-up of Leo, DreamWorks-style 3D animated character, speaking warmly at night,
  his face openly tender as he answers her — eyes soft, a genuine unguarded warmth. Russet/blond wavy
  hair, bright blue eyes. Warm candlelight illuminates his features; the background is a dark bokeh of
  city lights. 85 mm virtual lens, shallow depth of field, cinematic 3D animated lighting."

- Negative prompt: "No smirking/villain caricature, no harsh shadows, no photorealistic skin pores, no
  photoreal rendering."

- **Kling input: первый кадр, `sound: on`.** Один говорящий в кадре — чистый случай. Реальная реплика:
  Лео — «Правда. Без тебя всё это — просто красивые декорации.» (голос
  «Caspian»).

- Kling 3.0 Standard prompt: "Hold the close-up of Leo, DreamWorks-style 3D animation. He answers her,
  his face visibly warm and tender: 'Правда. Без тебя всё это — просто красивые декорации.' The same open warmth as shot 5 — this line should read as completely genuine.
  Camera static, shallow depth of field. Maintain 85 mm virtual lens."

- Continuation: Cut back to shot 6c on Vanessa's reaction.

- Motion notes: Minimal movement; hold on his eyes.

- Continuity checklist: Leo's hair/stubble as per Character Bible and reference sheet; consistent
  background bokeh; candle light warm.

- Rendering notes: Maintain clean render with soft subsurface skin shading; maintain warm midtones.

## Shot 6c – Close-up on Vanessa, Thrown Off Balance (Balcony)

**⚠️ Пересмотрено после теста.** Первая версия этого промпта описывала «явную, читаемую вспышку
растерянности» прямо в GPT Image кадре — а это статичный референс, который становится стартовым (и по
факту единственным) состоянием лица на весь клип. В результате на реальной генерации Ванесса весь шот
просидела с тревожным, широко раскрытыми глазами выражением — не вспышка, а устойчивая тревога на
несколько секунд, из-за чего весь балкон стал читаться так, будто она уже обижена ещё до кухни. Это
ломает всю задуманную структуру контраста (балкон = чистая романтика, ничего кроме тепла). Ниже —
исправленная версия: стартовый кадр снова тёплый/нежный, а лёгкая заминка прописана только в
Kling-промпте как быстрое, мимолётное движение внутри клипа, а не как поза.

- GPT Image prompt: "Close-up of Vanessa, DreamWorks-style 3D animated character, looking at him
  tenderly and warmly — soft, open, affectionate expression, continuing the warmth from the previous
  shot. Dark wavy hair, emerald-green eyes. Warm candlelight highlights her features; cool city lights
  rim the frame. 85 mm virtual lens, cinematic 3D animated lighting."

- Negative prompt: "No tears, no wide/startled eyes, no anxious expression, no cinematic bloom, no lens
  distortion, no photoreal rendering."

- **Kling input: первый кадр, `sound: on`.** Один говорящий в кадре — чистый случай. Реальная реплика:
  Ванесса — «...Хорошо.» (голос «Sienna»).

- Kling 3.0 Standard prompt: "Hold the close-up of Vanessa, DreamWorks-style 3D animation. She looks at
  him tenderly and warmly for the first second or two — this is the dominant expression of the shot. Only
  briefly, for less than a second, the faintest flicker of uncertainty crosses her face — barely visible,
  gone almost as soon as it registers, not a held or lingering expression. Her warmth returns immediately
  as she says quietly: '...Хорошо.' Her fingers may drift toward her ring or a strand of
  hair — her habitual small gesture when uncertain. Camera static with subtle handheld sway. Maintain
  85 mm virtual lens and shallow depth of field."

- Continuation: Crossfade to shot 7 (insert of cups) as conversation ends.

- Motion notes: Slight breathing movement; ensure eyes stay in focus. Hand-to-ring/hair gesture is
  brief and unconscious, not a lingering fidget.

- Continuity checklist: Hair parting consistent with reference sheet; jewellery (pendant) visible;
  candlelight flicker.

- Rendering notes: Balanced highlights; maintain warm key light and cool rim.

## Shot 7 – Insert of Cups (Night–Dawn Transition, close-up only)

- GPT Image prompt: "Close overhead view of two white ceramic mugs on a balcony table at night,
  DreamWorks-style 3D animated render. A small candle burns beside them. The mugs are nearly full. The
  city skyline is blurred in the background. No characters in frame. 35 mm virtual lens, cinematic 3D
  animated lighting."

- Negative prompt: "No human figures, no messy table, no neon colours, no photoreal rendering, no wide
  establishing framing — stay tight on the cups."

- **Kling input: первый + последний кадр.** Смена света ночь→рассвет — процесс, у которого обязательно
  должна быть конкретная целевая точка, а не открытый «раствор в никуда».

- GPT Image prompt (последний кадр): "Close overhead view of the same two white ceramic mugs on the same
  balcony table, DreamWorks-style 3D animated render, identical composition and cup positions to the
  first frame. Soft dawn light now replaces the night lighting — cool blue shadows give way to warm
  amber morning light. The candle has burned down slightly. No characters in frame. 35 mm virtual lens."

- Kling 3.0 Standard prompt: "Begin with the reference image of the cups at night, DreamWorks-style 3D animation. Hold
  for 2 s, then slowly dissolve as the surrounding light shifts from night-blue through dawn amber to
  soft cool morning daylight — the camera never leaves this close framing on the cups. The liquid in
  the cups is unchanged. Maintain 35 mm virtual lens and static camera throughout. Duration 5 s."

- Continuation: Match-dissolve, still close on the cups, directly into shot 8 — no dialogue plays over
  this shot; the cups carry the passage of time purely visually.

- Motion notes: Dissolve conveys passage of time; camera does not cut wide at any point in this shot.

- Continuity checklist: Cup positions unchanged; candle may have burned down slightly; mugs match props
  list; no characters or dialogue in this shot.

- Rendering notes: Ensure seamless blend between night and morning colour temperatures within the same
  close framing. Night image uses cool blue shadows; morning uses soft warm daylight.

## Shot 8 – Cups at Morning, Pull-Back to Establish Kitchen

- GPT Image prompt: "Extreme close-up of the same two white ceramic mugs, now on a kitchen table in
  soft morning light, DreamWorks-style 3D animated render, matching shot 7's framing exactly. No
  characters visible yet. 35 mm virtual lens, cinematic 3D animated lighting."

- Negative prompt: "No people, no clutter, no harsh shadows, no trendy neon, no photoreal rendering, no
  dialogue/caption text."

- **Kling input: первый + последний кадр.** Отъезд от кружек до раскрытой кухни — крупная смена
  композиции; без опорного финального кадра камера может «доехать» не туда и Лео с Ванессой окажутся в
  случайных позах. Последний кадр = стартовый кадр шота 9 (двухкадр, они уже стоят и разговаривают).

- Kling 3.0 Standard prompt: "Start on the same close-up of the cups where shot 7 left off, now in full morning light,
  DreamWorks-style 3D animation. Over 4–5 s, slowly pull back / crane out to reveal the modern open-plan
  kitchen around them — floor-to-ceiling windows, sleek cabinets, marble island. Maintain a 35 mm
  virtual lens throughout the pull-back; no hard cut to a wide shot."

- Continuation: Once the pull-back completes and the kitchen is fully revealed, cut to shot 9 — Leo
  and Vanessa are already standing in the kitchen, already mid-conversation. No cooking, no greeting.

- Motion notes: Single continuous pull-back/crane-out move; no separate wide static insert.

- Continuity checklist: Cups unchanged from shot 7 (same position, same near-full liquid level);
  window view matches World Bible; lighting consistent with time of day; the cups are never referenced
  in dialogue — they read as a purely visual motif.

- Rendering notes: Colour temperature cool but softened; clean stylized render; highlights not blown;
  keep the cups sharp through the pull-back before the kitchen resolves into focus.

## Shot 9 – Two-Shot, Already Mid-Conversation (Kitchen)

- GPT Image prompt: "Two-shot of Vanessa and Leo, DreamWorks-style 3D animated characters, standing in
  a modern kitchen in warm morning light — no food, no cooking props in use. Leo speaks calmly, his warm
  expression completely genuine and unguarded on his face; Vanessa begins to answer, caught mid-word,
  a clear flicker of surprise and hurt crossing her eyes before she composes herself. Both match their
  character reference sheets exactly. 50 mm virtual lens, cinematic 3D animated lighting."

- Negative prompt: "No cooking utensils in use, no plates of food, no exaggerated expressions, no
  visible anger or raised voices in body language, no photoreal rendering."

- **Kling input: первый кадр, `sound: on`.** Мультиспикерный шот — постпродакшн находит три сегмента
  речи. Реальные реплики: Лео — «Знаешь, сколько людей были бы счастливы на твоём месте?» («Caspian»);
  Ванесса — «Я счастлива. Просто вчера...» (обрывается, «Sienna»); Лео перебивает — «Я же не жалуюсь,
  когда прихожу домой уставшим. Не превращаю это в трагедию.» («Caspian»).

- Kling 3.0 Standard prompt: "Animate the two characters already in conversation, DreamWorks-style 3D
  animation. Leo speaks first, calmly and almost warmly: 'Знаешь, сколько людей были бы счастливы на
  твоём месте?' — his warmth completely genuine and visible on his face, hands resting in his pockets or
  loosely clasped behind his back, head tilted slightly toward her — his familiar posture when steering
  a conversation. Vanessa begins to answer, her hand lifting slightly: 'Я счастлива. Просто вчера...' —
  she is cut off mid-sentence, a clear flicker of surprise and hurt visible in her eyes for a moment
  before she composes herself, her hand stills. Leo interrupts gently: 'Я же не жалуюсь, когда прихожу
  домой уставшим. Не превращаю это в трагедию.' Camera is static at eye level with a barely perceptible
  push-in as the exchange lands. Maintain a 50 mm virtual lens."

- Continuation: Cut to shot 10 on Vanessa as she answers.

- Motion notes: Push-in must stay almost invisible — the visual tone should not telegraph conflict; the
  words should carry all of the tension. Leo's posture reads as relaxed control, not aggression (per
  Character Bible); Vanessa's stalled hand gesture is small, not a visible protest.

- Continuity checklist: No cooking/food props in frame; wardrobe and hair match reference sheets; the
  two cups from shots 7–8 are visible somewhere in the kitchen background, untouched.

- Rendering notes: Warm, soft morning light with no dramatic shadows; nothing in the lighting should
  hint at the conflict yet.

## Shot 10 – Close-up on Vanessa, First Named Hurt (Kitchen)

- GPT Image prompt: "Close-up of Vanessa, DreamWorks-style 3D animated character, speaking quietly in
  soft morning light, her eyes visibly glistening with real hurt, brows subtly drawn with pain that
  reads clearly on her face even as she holds herself together — calm but unmistakably hurting, not
  tearful, not defensive. Long dark wavy hair, emerald-green eyes. Matches her character reference sheet
  exactly. 85 mm virtual lens, shallow depth of field, cinematic 3D animated lighting."

- Negative prompt: "No tears, no raised eyebrows of anger, no exaggerated hurt expression, no
  photoreal rendering."

- **Kling input: первый кадр, `sound: on`.** Один говорящий в кадре — чистый случай. Реальная реплика:
  Ванесса — «Я не устраивала трагедию. Мне правда было больно.» (голос «Sienna»).

- Kling 3.0 Standard prompt: "Hold the close-up of Vanessa delivering her line, DreamWorks-style 3D
  animation. She says: 'Я не устраивала трагедию. Мне правда было больно.' — her eyes visibly glistening
  with real hurt as she says it, the pain clearly readable on her face even though her voice stays quiet
  and plain. Unlike her usual habit, her hands stay still and she doesn't touch her ring or hair here —
  for once she holds herself steady while she speaks. Camera static, shallow depth of field. Her
  delivery is quiet, not a complaint — the first time in the episode she names her feelings directly, and
  her face should make that cost visible."

- Continuation: Cut to shot 11 on Leo's response.

- Motion notes: Minimal movement; hold on her eyes. The absence of her usual nervous fidget is
  deliberate — it marks this line as unusually direct for her (per Character Bible).

- Continuity checklist: Hair, pendant and wardrobe match reference sheet; expression reads as quiet
  hurt, not anger or tears.

- Rendering notes: Soft morning light on her face; background softly out of focus.

## Shot 11 – Close-up on Leo, the Caring-Sounding Reframe (Kitchen)

- GPT Image prompt: "Close-up of Leo, DreamWorks-style 3D animated character, speaking gently in warm
  morning light, his warmth completely convincing and visibly genuine — eyes soft, a caring half-smile
  that reads as entirely sincere, matching and pushing further into his reference sheet's warmer emotion
  poses. Not a smirk, not overtly smug — this has to look like real love for the manipulation underneath
  it to work. Russet/blond wavy hair, bright blue eyes. 85 mm virtual lens, shallow depth of field,
  cinematic 3D animated lighting."

- Negative prompt: "No smirking/villain caricature, no visible anger, no exaggerated warmth, no
  photoreal rendering."

- **Kling input: первый кадр, `sound: on`.** Один говорящий в кадре — чистый случай. Реальная реплика:
  Лео — «Может, стоит иначе на это смотреть. (пауза) Я ведь только хочу, чтобы нам обоим было легче.»
  (голос «Caspian»).

- Kling 3.0 Standard prompt: "Hold the close-up of Leo delivering his reframe, DreamWorks-style 3D
  animation, including a brief pause before his last line. He says: 'Может, стоит иначе на это
  смотреть.' (pause) 'Я ведь только хочу, чтобы нам обоим было легче.' — his face visibly warm and
  soft throughout, eyes tender, the caring completely convincing to look at. The same slow, deliberate
  blink from shot 5 returns here, with a faint head tilt — his familiar 'caring' mannerism, now doing
  quieter work. Camera static, shallow depth of field. Delivery should read as loving and reasonable,
  not cruel — the manipulation is entirely in the words, so his face must be unmistakably warm."

- Continuation: Cut to shot 12 on Vanessa's question.

- Motion notes: Minimal movement; hold through the pause without cutting away. The blink/head-tilt
  callback to shot 5 should be recognisable, not exaggerated.

- Continuity checklist: Leo's hair/stubble as per Character Bible and reference sheet; expression stays
  warm and controlled throughout, never hardens.

- Rendering notes: Warm light on his face; calm, composed rendering — nothing should visually signal
  that this is the manipulative core of the scene.

## Shot 12 – Close-up on Vanessa, the Disarming Question (Kitchen)

- GPT Image prompt: "Close-up of Vanessa, DreamWorks-style 3D animated character, asking a quiet
  question in soft morning light, her curiosity completely open and visible on her face, eyes wide and
  genuinely present, not guarded at all — not challenging, not ironic, unmistakably sincere. Matches her
  character reference sheet exactly. 85 mm virtual lens, shallow depth of field, cinematic 3D animated
  lighting."

- Negative prompt: "No smirk, no confrontational expression, no raised eyebrow of challenge, no
  photoreal rendering."

- **Kling input: первый кадр, `sound: on`.** Один говорящий в кадре — чистый случай. Реальная реплика:
  Ванесса — «А тебе самому — легко?» (голос «Sienna»).

- Kling 3.0 Standard prompt: "Hold the close-up of Vanessa asking her question, DreamWorks-style 3D
  animation. She says: 'А тебе самому — легко?' — her eyes wide, open and genuinely present, the
  sincerity completely visible on her face, not guarded. Her hands and shoulders stay still and
  unclenched — no fidgeting, no touching her ring or hair. Camera static with slight rack focus to keep
  her eyes sharp. Delivery is calm and sincere, almost tender — not a challenge."

- Continuation: Cut to shot 13 on Leo's reaction.

- Motion notes: Slight rack focus only; no other movement. The stillness is the point — this is the
  one moment she isn't managing her own anxiety while she speaks.

- Continuity checklist: Hair, pendant, wardrobe consistent with reference sheet; expression reads as
  sincere, not smug or triumphant.

- Rendering notes: Same soft morning light as shot 10, for visual continuity between her two close-ups.

## Shot 13 – Close-up on Leo, Composure Flickers (Kitchen, no dialogue)

- GPT Image prompt: "Extreme close-up of Leo, DreamWorks-style 3D animated character, a fraction-of-a-
  second flicker of genuine surprise crossing his face before he catches himself — matching his
  reference sheet's features exactly, but with a rare, almost-invisible crack in his usual composed
  expression. 85 mm virtual lens, shallow depth of field, cinematic 3D animated lighting."

- Negative prompt: "No overt shock, no wide eyes, no mouth agape — the reaction must be subtle, almost
  missable, no photoreal rendering."

- Kling 3.0 Standard prompt: "Hold on Leo's face for 3 s, DreamWorks-style 3D animation, no dialogue. Animate a
  micro-expression: a barely perceptible widening of the eyes or falter in his usual calm, his jaw
  tightening almost imperceptibly and the corners of his mouth flattening for an instant, held for a
  beat, then he consciously smooths his face back into composure. Camera static, held slightly longer
  than a normal reaction shot."

- Continuation: Cut to shot 14 on Vanessa looking away.

- Motion notes: The entire shot is the micro-expression; no camera movement. Jaw/mouth tightening is
  the same tell described in Character Bible for when his composure is threatened — here it must stay
  barely visible, not read as open anger.

- Continuity checklist: This is the first shot in the whole episode where Leo's face shows something he
  didn't choose to show — keep it subtle enough that it rewards a close rewatch rather than announcing
  itself.

- Rendering notes: Same warm light as shot 11, but read slightly harder/flatter to mark the shift.

## Shot 14 – Close-up on Vanessa, Looking Away (Kitchen, no dialogue)

- GPT Image prompt: "Close-up of Vanessa, DreamWorks-style 3D animated character, holding a steady,
  level gaze straight ahead. Calm, unresolved expression — neither defiant nor defeated. Matches her
  character reference sheet exactly. 85 mm virtual lens, shallow depth of field, cinematic 3D animated
  lighting."

- Negative prompt: "No tears, no smiling, no triumphant expression, no photoreal rendering."

- **Kling input: первый + последний кадр.** Уход взгляда вниз — конкретное направленное движение головы;
  без опорного финального кадра наклон может не случиться или уйти не в ту сторону.

- GPT Image prompt (последний кадр): "Same close-up of Vanessa, identical framing and lighting, but her
  head is now tilted down and her gaze has dropped away from camera — calm, unresolved expression,
  neither defiant nor defeated. Matches her character reference sheet exactly. 85 mm virtual lens,
  shallow depth of field, cinematic 3D animated lighting."

- Kling 3.0 Standard prompt: "Hold on Vanessa for 3 s, DreamWorks-style 3D animation, no dialogue. She holds his gaze,
  then slightly tilts her head down and looks away. Her shoulders don't straighten the way they do when
  she's happy — they stay slightly low as she looks away, a quiet, deflated stillness rather than a
  dramatic gesture. Camera static with a slight tilt down following her gaze."

- Continuation: Cut to shot 15, the closing cups insert.

- Motion notes: Slight tilt down only, timed to her gaze shift. Shoulder posture is the quiet tell here
  — per Character Bible, straightened shoulders read as happy for her, so keeping them low signals the
  opposite without any theatrical gesture.

- Continuity checklist: Hair, pendant, wardrobe consistent with reference sheet; expression reads as
  quietly unresolved, not as a clear win or loss for either character.

- Rendering notes: Cool daylight very slightly dims the palette compared to shot 12, echoing her
  withdrawal.

## Shot 15 – Insert of Cups, Episode Closer (Kitchen)

- GPT Image prompt: "Close overhead view of the same two white ceramic mugs from shots 7–8, on the
  kitchen table in neutral morning light, DreamWorks-style 3D animated render. One mug still full, the
  other empty. No characters in frame. 35 mm virtual lens, cinematic 3D animated lighting."

- Negative prompt: "No human figures, no messy table, no dramatic lighting, no photoreal rendering."

- Kling 3.0 Standard prompt: "Static overhead shot of the two cups, DreamWorks-style 3D animation, held for 3–4 s, then
  a slow fade to black to end the episode. Maintain 35 mm virtual lens throughout."

- Continuation: End of episode — fade out.

- Motion notes: Static hold, then fade; no camera movement.

- Continuity checklist: Cup design matches shots 7–8 exactly; which cup is empty is left deliberately
  unassigned/ambiguous — the imbalance should read as belonging to the relationship, not to one person.

- Rendering notes: Neutral, slightly cool morning light; no warm/cool bias that would editorialise the
  symbol — let the imbalance speak for itself.

## General Notes

- All GPT Image prompts should be used to generate high-resolution keyframes that capture the
  composition, lighting, mood and DreamWorks-style 3D render of each shot. These images become the
  reference for the Kling 3.0 Standard animations, and must match the character reference sheets in
  Визуализации/.

- Negative prompts explicitly exclude photorealism/live-action rendering and comedic/chibi
  proportions to keep the tone consistent with a mature, cinematic animated drama.

- Animation prompts should describe movement, virtual lens, duration and mood succinctly. Use "start
  from the reference image" as a baseline. For shots with dialogue, the actual Russian line is written
  into the prompt itself in quotes (not just "he speaks softly") with `sound: on` — this is what makes
  Kling animate real mouth movement, even though the voice Kling generates for it is not usable and gets
  replaced in postproduction (see "✅ Липсинк решён").

- Continuity checklists should be consulted by the person responsible for visual consistency before and
  after each generation pass.

- Rendering notes remind the compositing team of the desired DreamWorks-style 3D look (no film grain,
  no photoreal skin) and aspect ratio (9:16 vertical for social media).

## ✅ Липсинк решён: нативный Kling `sound: on` + локальная замена звука (ffmpeg)

Перебрали четыре подхода, прежде чем зафиксировать финальный:

1. **`dubbing` поверх немого Kling-клипа** — не сработал. `dubbing` переводит и пересинхронизирует уже
   существующую в видео речь, а у немого клипа речи нет вообще — job падает со статусом `failed`
   (протестировано на шоте 3, кредиты вернулись автоматически).
2. **Wan 2.7 / Seedance 2.0 с `audio_references`** (генерация видео, ведомая готовым TTS-файлом) —
   рабочий, но лишний платный шаг генерации (9–27 кредитов за шот) поверх уже готового Kling-клипа.
3. **Kling Lip Sync (раздел AI Human на kling.ai, липсинк по загруженному аудио)** — протестирован и
   отвергнут: на стилизованном DreamWorks-персонаже перерисовка области рта дала уродливые артефакты
   (кривые фотореалистичные зубы поверх мультяшного лица). Причина системная: пост-липсинк-инструменты
   обучены на реальных лицах и «чинят» рот в сторону фотореализма — на анимационном стиле это ломает
   лицо. По той же причине не стоит ждать лучшего от `dubbing` и аналогов на этом материале.
4. **Финальный вариант (ниже)** — единственный без перерисовки лица: рот анимирует сама Kling при
   генерации, звук заменяется локально. Фонемная точность неидеальна (см. «Известное ограничение»
   ниже), зато ноль визуальных артефактов.

**Почему у Kling вообще не открывался рот (изначальный баг).** Промпты описывали реплику текстом
(«he speaks softly»), а не цитировали её — Kling нечего было озвучивать, значит и рот двигать было
незачем.

**Известное ограничение: русский язык.** Kling 3.0 официально поддерживает речь только на пяти языках
(китайский, английский, японский, корейский, испанский). Реплику на любом другом языке — включая
русский — модель **переводит на английский** или озвучивает тарабарщиной; добавка вроде «RUSSIAN
speech» в промпт не помогает (проверено). Следствие: движение рта тяготеет к английским фонемам, и
наложенная в посте русская озвучка совпадает с губами лишь приблизительно. Это принятая цена пайплайна
— альтернативы (пост-липсинк) ломают стилизованное лицо, см. пункт 3 выше.

**Финальный пайплайн (проверено и подтверждено на шоте 3):**

1. В промпт Kling 3.0 Standard реплика вписывается **на русском, в кавычках**, `sound: on`. Kling
   анимирует настоящее открытие рта под эту цитату — но озвучка, которую она сама сочиняет, звучит как
   тарабарщина (не настоящий язык). Это ожидаемо и не мешает следующему шагу.
2. Сгенерировать реальную реплику через `generate_audio` (`text2speech_v2` / `minimax`, зафиксированные
   голоса — Лео = «Caspian» `ef70cc83-3015-4bad-9359-0ea968c43ec0`, Ванесса = «Sienna»
   `41023a48-71ab-478a-bea7-c7b5a78f6b36`).
3. Найти реальный момент начала речи в тарабарской дорожке Kling через `ffmpeg -af
   silencedetect=noise=-30dB:d=0.3` — персонаж может несколько секунд молча входить в кадр/подходить, и
   накладывать TTS с нулевой секунды неверно (так и было в первой попытке — звук пришёл до открытия
   рта). На шоте 3 речь в тарабарской дорожке началась на **4.3 с**.
4. Наложить TTS-файл на видео через `ffmpeg` (`adelay` на найденную задержку), заменив тарабарскую
   дорожку полностью:
   `ffmpeg -i видео.mp4 -i реплика.mp3 -filter_complex "[1:a]atempo=X,adelay=D|D,apad=whole_dur=T[a]" -map 0:v -map "[a]" -c:v copy -c:a aac -shortest итог.mp4`
   где `D` — найденная задержка в мс, `T` — длительность видео в секундах.
5. **Если TTS-реплика не помещается до конца клипа** (частый случай — TTS без пауз на вход/выход длиннее
   отснятого окна) — **ускорить аудио через `atempo`** (в тесте — `atempo=1.09`, ~9%, звучит естественно
   для голоса «Caspian»), а не растягивать видео замороженным кадром. Заморозка кадра в 3D-анимации
   читается как явный баг рендера, а не художественный приём — визуально недопустима.

**Мультиспикерные шоты (4, 9).** В кадре говорят оба персонажа по очереди. Промпт по-прежнему цитирует
все реплики по очереди на русском; в посте `silencedetect` должен найти **несколько** сегментов
тарабарской речи вместо одного, и на каждый сегмент накладывается своя реплика нужным голосом (тот же
рецепт, шаги 3–5, применённый по сегментам). Принцип идентичен уже подтверждённому на шоте 3, но на
реальном многоречевом шоте пока не протестирован — сделать это перед тем, как гнать всю сцену целиком.
(Шот 6 раньше был таким же случаем с закадровой репликой Лео — решён по-другому: разбит на три
одноголосых под-шота 6a/6b/6c, см. «Модель и режим ввода по шотам».)
