# AI Package: Pilot (Episode 1)

This AI Package provides prompts and notes for generating the keyframes and video shots described in
the Shot List. For each shot we define a GPT Image prompt (to create a still frame reference), a
negative prompt (to guide the model away from undesired elements), an animation prompt (to animate the
shot from the reference), continuation notes for linking shots, motion instructions, a continuity
checklist and rendering notes. Prompts focus on the DreamWorks-style 3D animated look established in
the character reference sheets (Визуализации/), consistent character appearance and adherence to the
Visual Bible.

**Две модели анимации, в зависимости от того, есть ли в шоте реплика:**

- **Wan 2.7** (`start_image` + опционально `end_image` + `audio_references`) — для всех шотов, где
  персонаж говорит на камеру. Модель синхронизирует движение рта под реальную озвученную реплику
  (TTS локальными голосами — см. Character Bible → «Голос»), а не под текстовое описание «he speaks
  softly», как раньше. Проверено на шоте 3: рот двигается в такт озвучке; звук нужно приложить/свести
  отдельно (см. «Open Issue: Lip Sync» ниже про found-баг с длительностью). Дешевле Seedance 2.0 (9
  кредитов против 27 на тех же параметрах) и не «плывёт» фон между стартовым и финишным кадром.
- **Kling 3.0 Standard** — для шотов без произносимой на камеру реплики (establishing, инсерты,
  безмолвные реакции). Здесь синхронизация рта не нужна вовсе.

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
  прописаны прямо внутри промптов (Wan 2.7 и Kling 3.0 Standard) ниже.

## Модель и режим ввода по шотам

| Шот | Модель | Кадры | Почему |
|---|---|---|---|
| 1 | Kling 3.0 Standard | первый | establishing, без реплик |
| 2 | Kling 3.0 Standard | первый | Ванесса одна, без реплик |
| **3** | **Wan 2.7** | **первый + последний** | Лео говорит на камеру + передаёт кружку — нужны и аудио-синхронизация, и опорный финальный кадр, чтобы передача не «плыла» |
| **4** | **Wan 2.7** | первый | двухкадр, реплики обоих персонажей подряд — см. предупреждение про мультиспикерные шоты ниже |
| **5** | **Wan 2.7** | первый | крупный план Лео, один говорящий в кадре — чистый случай для аудио-липсинка |
| **6** | **Wan 2.7** | первый | крупный план Ванессы; реплика Лео звучит закадрово, пока камера держит её — см. предупреждение ниже |
| 7 | Kling 3.0 Standard | первый + последний | инсерт кружек, смена света ночь→рассвет, без реплик |
| 8 | Kling 3.0 Standard | первый + последний | отъезд камеры к кухне, без реплик в этом шоте |
| **9** | **Wan 2.7** | первый | двухкадр, реплики обоих персонажей подряд — мультиспикерный шот, см. предупреждение ниже |
| **10** | **Wan 2.7** | первый | крупный план Ванессы, один говорящий в кадре |
| **11** | **Wan 2.7** | первый | крупный план Лео, один говорящий в кадре |
| **12** | **Wan 2.7** | первый | крупный план Ванессы, один говорящий в кадре |
| 13 | Kling 3.0 Standard | первый | реакция Лео без реплики |
| **14** | Kling 3.0 Standard | **первый + последний** | реакция Ванессы без реплики, нужен опорный кадр взгляда вниз |
| 15 | Kling 3.0 Standard | первый | финальный инсерт, без реплик |

**Мультиспикерные шоты (4, 9) и закадровая реплика в шоте 6 — открытый риск.** У Wan 2.7 один слот
`audio_references` на весь клип, а в этих шотах в кадре либо говорят оба персонажа по очереди (4, 9),
либо в кадре один человек, а звучит реплика другого (6). Обычная TTS-дорожка со всеми репликами подряд
заставит модель синхронизировать рот того, кто в кадре, под чужие слова тоже. Способ обхода, пока не
протестирован отдельно: в промпте явно прописано, чья реплика звучит в какой момент и что лицо в кадре
должно молчать/слушать во время чужих слов — сама модель должна за это зацепиться по смыслу промпта,
но это не гарантия фонемной точности. Для 5, 10, 11, 12 (и в основном 3) риска нет — один говорящий,
одна аудиодорожка.

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
  stepping out onto a balcony at night. Russet/blond wavy hair, bright blue eyes, dark minimalist
  sweater, matching his character reference sheet. The railing and a small table are visible; the city
  skyline glows behind him. 50 mm virtual lens, warm candlelight, cinematic 3D animated lighting."

- Negative prompt: "No smirking/villain caricature, no exaggerated swagger, no plastic/waxy skin, no
  futuristic clothing, no photoreal rendering."

- **Wan 2.7 input: первый + последний кадр + audio_references.** Последний кадр = стартовый кадр шота 4
  (двухкадр, оба уже держат свою кружку, тёплый свет, город в боке) — так финал шота 3 гарантированно
  совпадает с началом шота 4, без произвольной мизансцены.

- Audio (TTS): реплика Лео — «Замёрзла? Я по тишине понял, что ты здесь. Ты всегда затихаешь, когда
  думаешь.» Сгенерировано через `generate_audio`, model `text2speech_v2`, variant `minimax`, voice_id
  `ef70cc83-3015-4bad-9359-0ea968c43ec0` (пресет «Caspian»). **Важно:** `duration` в `generate_video`
  должен быть ≥ фактической длины TTS-файла, округлённой вверх (в тесте 6.22 с аудио при duration=6
  обрезало конец фразы и дало рассинхрон — используйте 7 с).

- Wan 2.7 prompt: "Leo enters from the apartment doorway onto the balcony at night, DreamWorks-style 3D
  animation. He says: 'Cold? I could tell by the quiet that you were out here. You always go quiet when
  you're thinking.' The camera (virtual steadicam) follows him in a smooth arc towards Vanessa as he
  speaks. As he reaches her, he extends one of the two mugs toward her with his hand and she reaches out
  and takes it into her own hand — a clear, deliberate physical handoff, both hands visible at the moment
  of exchange. Leo keeps the second mug in his other hand. Right after the handoff, his free hand rests
  briefly on the railing beside her or lightly at her shoulder — his familiar, quiet way of controlling
  shared space. The handoff completes near the end of the shot, after his line finishes. His mouth
  movement follows the provided audio track exactly. Use a 50 mm virtual lens with shallow depth of
  field; keep the candle flicker and city backdrop. Duration 7 s."

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
  on a balcony at night, each holding a mug. Leo gazes softly at Vanessa; she looks down shyly. Warm
  candlelight illuminates their faces while the Moscow skyline blurs behind them. 50 mm virtual lens,
  cinematic 3D animated lighting."

- Negative prompt: "No dramatic backlighting, no glamorous fashion beyond reference sheets, no visible
  rig/skeleton artifacts, no lens flares, no photoreal skin."

- **Wan 2.7 input: первый кадр + audio_references.** Мультиспикерный шот — см. предупреждение в разделе
  «Модель и режим ввода по шотам».

- Audio (TTS, две реплики подряд одним файлом или двумя склеенными клипами): Ванесса — «Я не знала, что
  это слышно.» (voice_id `41023a48-71ab-478a-bea7-c7b5a78f6b36`, пресет «Sienna»); Лео — «Мне — слышно.
  Я слышу тебя, даже когда ты молчишь.» (voice_id `ef70cc83-3015-4bad-9359-0ea968c43ec0`, пресет
  «Caspian»). `duration` в `generate_video` ≥ суммарной длины обеих реплик, округлённой вверх.

- Wan 2.7 prompt: "Start from the reference image of both characters on the balcony, DreamWorks-style 3D
  animation. Perform a slow dolly inwards for 4 s while the characters take small sips and exchange
  glances. Vanessa speaks first, quietly: 'I didn't know that was audible.' Her mouth moves only during
  her own line; she stays still and listening the rest of the time. Leo then answers, warmly: 'I hear
  it. I hear you even when you're silent.' His mouth moves only during his own line. Leo stands with
  easy, upright confidence, one hand loosely in his pocket; Vanessa holds her mug with both hands, close
  to her body. Keep a 50 mm virtual lens; handheld breathing motion. Warm tones should dominate the
  foreground with cool bokeh in the background."

- Continuation: Cuts to close-ups (shots 5–6) to emphasise dialogue and emotion.

- Motion notes: Dolly speed slow; maintain equal distance to both characters. Posture contrast is
  deliberate — his open, confident stance versus her more contained, self-holding one (per Character
  Bible body-language notes).

- Continuity checklist: Both mugs remain nearly full; candle stays on table; hair, wardrobe consistent
  with reference sheets; skyline unchanged.

- Rendering notes: Ensure natural skin shading per reference sheets; keep depth of field shallow;
  maintain clean stylized render.

## Shot 5 – Close-up on Leo (Balcony)

- GPT Image prompt: "Close-up of Leo, DreamWorks-style 3D animated character, speaking softly at night.
  Russet/blond wavy hair, bright blue eyes, calm expression matching his reference sheet's 'влюбленный'
  emotion pose. Warm candlelight illuminates his features; the background is a dark bokeh of city
  lights. 85 mm virtual lens, shallow depth of field, cinematic 3D animated lighting."

- Negative prompt: "No harsh shadows, no over-sharpening, no unnatural eye reflections, no
  photorealistic skin pores."

- **Wan 2.7 input: первый кадр + audio_references.** Один говорящий в кадре — чистый случай.

- Audio (TTS): реплика Лео — «Помнишь, как мы только познакомились? Я тогда сразу понял — вот она, моя
  муза.» voice_id `ef70cc83-3015-4bad-9359-0ea968c43ec0` (пресет «Caspian»), model `text2speech_v2`,
  variant `minimax`. `duration` ≥ длины TTS-файла, округлённой вверх.

- Wan 2.7 prompt: "Hold the close-up of Leo delivering his line, DreamWorks-style 3D animation. He says:
  'Do you remember when we first met? I knew right away — there she is, my muse.' His mouth movement
  follows the provided audio track exactly. He blinks slowly and deliberately as he speaks — his
  familiar 'caring listener' mannerism. The camera remains static with micro-jitters to emulate
  handheld. Maintain an 85 mm virtual lens; ensure the light source flickers subtly on his face."

- Continuation: After his line, cut to shot 6 for Vanessa's reaction.

- Motion notes: Micro-jitters only; no rack focus. The slow blink should read as warm, not sleepy or
  theatrical — per Character Bible, it's what makes him seem like a "caring" listener.

- Continuity checklist: Leo's stubble/hair as per Character Bible and reference sheet; consistent
  background bokeh; candle light warm.

- Rendering notes: Maintain clean render with soft subsurface skin shading; maintain warm midtones.

## Shot 6 – Close-up on Vanessa (Balcony)

- GPT Image prompt: "Close-up of Vanessa, DreamWorks-style 3D animated character, listening intently at
  night. Dark wavy hair, emerald-green eyes, expression shifting between hope and doubt (see her
  'задумчивая' reference pose). Warm candlelight highlights her features; cool city lights rim the
  frame. 85 mm virtual lens, cinematic 3D animated lighting."

- Negative prompt: "No tears, no smiling, no cinematic bloom, no lens distortion, no photoreal
  rendering."

- **Wan 2.7 input: первый кадр + audio_references.** Мультиспикерный случай: в кадре Ванесса, но звучит
  и её, и закадровая реплика Лео — см. предупреждение в разделе «Модель и режим ввода по шотам».

- Audio (TTS, три реплики подряд): Ванесса — «Правда?» (voice_id `41023a48-71ab-478a-bea7-c7b5a78f6b36`,
  «Sienna»); Лео (закадрово) — «Правда. Без тебя я просто хорошо одетый человек. С тобой — я чувствую,
  что живу.» (voice_id `ef70cc83-3015-4bad-9359-0ea968c43ec0`, «Caspian»); Ванесса — «...Хорошо.»
  («Sienna»). `duration` ≥ суммарной длины трёх реплик, округлённой вверх.

- Wan 2.7 prompt: "Hold the close-up of Vanessa reacting, DreamWorks-style 3D animation. She asks
  softly: 'Really?' — her mouth moves only during this line. Leo's voice answers off-screen: 'Really.
  Without you I'm just a well-dressed man. With you, I feel alive.' — during his line her face stays
  still and listening, her mouth does not move, only her eyes react. Then she says quietly: '...Okay.' —
  her mouth moves again only for this final line. Her eyes flicker as she processes his words, and her
  fingers may drift toward her ring or a strand of hair — her habitual small gesture when uncertain. The
  camera is static with subtle handheld sway. Maintain 85 mm virtual lens and shallow depth of field."

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
  a modern kitchen in warm morning light — no food, no cooking props in use. Leo speaks calmly, almost
  gently; Vanessa begins to answer, caught mid-word. Both match their character reference sheets
  exactly. 50 mm virtual lens, cinematic 3D animated lighting."

- Negative prompt: "No cooking utensils in use, no plates of food, no exaggerated expressions, no
  visible anger or raised voices in body language, no photoreal rendering."

- **Wan 2.7 input: первый кадр + audio_references.** Мультиспикерный шот — см. предупреждение в разделе
  «Модель и режим ввода по шотам».

- Audio (TTS, три реплики подряд): Лео — «Знаешь, сколько людей были бы счастливы на твоём месте?»
  («Caspian»); Ванесса — «Я счастлива. Просто вчера...» (обрывается, «Sienna»); Лео (перебивает) — «Я же
  не жалуюсь, когда прихожу домой уставшим. Не превращаю это в трагедию.» («Caspian»). `duration` ≥
  суммарной длины трёх реплик, округлённой вверх.

- Wan 2.7 prompt: "Animate the two characters already in conversation, DreamWorks-style 3D animation.
  Leo speaks first, calmly and almost warmly: 'Do you know how many people would be happy to be in your
  place?' — his mouth moves only during his line, hands resting in his pockets or loosely clasped behind
  his back, head tilted slightly toward her — his familiar posture when steering a conversation. Vanessa
  begins to answer, her hand lifting slightly, her mouth moving only for her words: 'I am happy. It's
  just, yesterday...' — she is cut off mid-sentence, her hand stills. Leo interrupts gently, his mouth
  moving again for his line: 'I don't complain when I come home tired. I don't turn it into a tragedy.'
  Camera is static at eye level with a barely perceptible push-in as the exchange lands. Maintain a
  50 mm virtual lens."

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
  soft morning light. Long dark wavy hair, emerald-green eyes, calm but hurt expression — not tearful,
  not defensive. Matches her character reference sheet exactly. 85 mm virtual lens, shallow depth of
  field, cinematic 3D animated lighting."

- Negative prompt: "No tears, no raised eyebrows of anger, no exaggerated hurt expression, no
  photoreal rendering."

- **Wan 2.7 input: первый кадр + audio_references.** Один говорящий в кадре — чистый случай.

- Audio (TTS): реплика Ванессы — «Я не устраивала трагедию. Мне правда было больно.» voice_id
  `41023a48-71ab-478a-bea7-c7b5a78f6b36` (пресет «Sienna»), model `text2speech_v2`, variant `minimax`.
  `duration` ≥ длины TTS-файла, округлённой вверх.

- Wan 2.7 prompt: "Hold the close-up of Vanessa delivering her line, DreamWorks-style 3D animation. She
  says: 'I wasn't making a scene. It really hurt.' Her mouth movement follows the provided audio track
  exactly. Unlike her usual habit, her hands stay still and she doesn't touch her ring or hair here — for
  once she holds herself steady while she speaks. Camera static, shallow depth of field. Her delivery is
  quiet and plain, not a complaint — the first time in the episode she names her feelings directly."

- Continuation: Cut to shot 11 on Leo's response.

- Motion notes: Minimal movement; hold on her eyes. The absence of her usual nervous fidget is
  deliberate — it marks this line as unusually direct for her (per Character Bible).

- Continuity checklist: Hair, pendant and wardrobe match reference sheet; expression reads as quiet
  hurt, not anger or tears.

- Rendering notes: Soft morning light on her face; background softly out of focus.

## Shot 11 – Close-up on Leo, the Caring-Sounding Reframe (Kitchen)

- GPT Image prompt: "Close-up of Leo, DreamWorks-style 3D animated character, speaking gently in warm
  morning light. Russet/blond wavy hair, bright blue eyes, soft almost-tender expression matching his
  reference sheet's warmer emotion poses — not a smirk, not overtly smug. 85 mm virtual lens, shallow
  depth of field, cinematic 3D animated lighting."

- Negative prompt: "No smirking/villain caricature, no visible anger, no exaggerated warmth, no
  photoreal rendering."

- **Wan 2.7 input: первый кадр + audio_references.** Один говорящий в кадре — чистый случай.

- Audio (TTS): реплика Лео — «Может, стоит иначе на это смотреть. (пауза) Я ведь только хочу, чтобы нам
  обоим было легче.» voice_id `ef70cc83-3015-4bad-9359-0ea968c43ec0` (пресет «Caspian»), model
  `text2speech_v2`, variant `minimax`. `duration` ≥ длины TTS-файла (включая паузу), округлённой вверх.

- Wan 2.7 prompt: "Hold the close-up of Leo delivering his reframe, DreamWorks-style 3D animation,
  including a brief pause before his last line. He says: 'Maybe you should look at it differently.'
  (pause) 'I just want things to be easier for both of us.' His mouth movement follows the provided
  audio track exactly, including staying still during the pause. The same slow, deliberate blink from
  shot 5 returns here, with a faint head tilt — his familiar 'caring' mannerism, now doing quieter work.
  Camera static, shallow depth of field. Delivery should read as loving and reasonable, not cruel — the
  manipulation is entirely in the words."

- Continuation: Cut to shot 12 on Vanessa's question.

- Motion notes: Minimal movement; hold through the pause without cutting away. The blink/head-tilt
  callback to shot 5 should be recognisable, not exaggerated.

- Continuity checklist: Leo's hair/stubble as per Character Bible and reference sheet; expression stays
  warm and controlled throughout, never hardens.

- Rendering notes: Warm light on his face; calm, composed rendering — nothing should visually signal
  that this is the manipulative core of the scene.

## Shot 12 – Close-up on Vanessa, the Disarming Question (Kitchen)

- GPT Image prompt: "Close-up of Vanessa, DreamWorks-style 3D animated character, asking a quiet
  question in soft morning light. Calm, genuinely curious expression — not challenging, not ironic.
  Matches her character reference sheet exactly. 85 mm virtual lens, shallow depth of field, cinematic
  3D animated lighting."

- Negative prompt: "No smirk, no confrontational expression, no raised eyebrow of challenge, no
  photoreal rendering."

- **Wan 2.7 input: первый кадр + audio_references.** Один говорящий в кадре — чистый случай.

- Audio (TTS): реплика Ванессы — «А тебе самому — легко?» voice_id `41023a48-71ab-478a-bea7-c7b5a78f6b36`
  (пресет «Sienna»), model `text2speech_v2`, variant `minimax`. `duration` ≥ длины TTS-файла, округлённой
  вверх.

- Wan 2.7 prompt: "Hold the close-up of Vanessa asking her question, DreamWorks-style 3D animation. She
  says: 'Is it easy for you?' Her mouth movement follows the provided audio track exactly. Her hands and
  shoulders stay still and unclenched — no fidgeting, no touching her ring or hair. Camera static with
  slight rack focus to keep her eyes sharp. Delivery is calm and sincere, almost tender — not a
  challenge."

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
  reference for the Wan 2.7 / Kling 3.0 Standard animations, and must match the character reference
  sheets in Визуализации/.

- Negative prompts explicitly exclude photorealism/live-action rendering and comedic/chibi
  proportions to keep the tone consistent with a mature, cinematic animated drama.

- Animation prompts (Wan 2.7 for dialogue shots, Kling 3.0 Standard for the rest) should describe
  movement, virtual lens, duration and mood succinctly. Use "start from the reference image" as a
  baseline. For Wan 2.7 shots, the actual dialogue line is written into the prompt itself (not just
  "he speaks softly") so the described performance matches the words being spoken via `audio_references`.

- Continuity checklists should be consulted by the person responsible for visual consistency before and
  after each generation pass.

- Rendering notes remind the compositing team of the desired DreamWorks-style 3D look (no film grain,
  no photoreal skin) and aspect ratio (9:16 vertical for social media).

## ✅ Липсинк решён через Wan 2.7 (не через dubbing)

Изначальный план («немой Kling-клип → `dubbing` поверх него») не сработал: `dubbing` переводит и
пересинхронизирует уже существующую в видео речь — а у немого Kling-клипа речи нет вообще, инструмент
падает (протестировано на шоте 3, job завершился со статусом `failed`, кредиты вернулись автоматически).

**Рабочий пайплайн для шотов с репликой на камеру:**

1. Сгенерировать TTS-реплику через `generate_audio` (`text2speech_v2` / `minimax`, локальные голоса —
   Лео = «Caspian» `ef70cc83-3015-4bad-9359-0ea968c43ec0`, Ванесса = «Sienna»
   `41023a48-71ab-478a-bea7-c7b5a78f6b36`).
2. Сгенерировать сам видео-шот через `generate_video`, model `wan2_7`, передав стартовый (и, где нужно,
   финишный) кадр как `start_image`/`end_image` и готовый TTS-файл как `audio_references`. Модель
   синхронизирует движение рта под реальную озвучку, а не под текстовое описание.
3. **`duration` обязательно ≥ фактической длины TTS-файла, округлённой вверх до целой секунды.** В
   тесте на шоте 3 TTS занял 6.22 с, а `duration` был выставлен в 6 — конец фразы обрезался видеорядом,
   из-за чего к финалу реплики губы и звук расходились. При duration ≥ длины аудио этой проблемы быть не
   должно (не перепроверено на новом прогоне, но причина установлена однозначно).
4. Готовый клип от Wan 2.7 идёт **без звука в файле** — озвучку нужно свести/наложить отдельно в монтаже
   (TTS-файл уже есть от шага 1, просто не встроен автоматически в видеофайл).

**Почему Wan 2.7, а не Seedance 2.0:** обе модели тестировались на шоте 3 с одинаковыми
стартовым/финишным кадром и озвучкой. Seedance 2.0 (27 кредитов) дал движение рта, но без звука в файле
и с «плывущим» фоном между кадрами. Wan 2.7 (9 кредитов) — звук был встроен, фон стабильный; из минусов
— рассинхрон губ, но он объясняется багом с длительностью (см. пункт 3), а не моделью как таковой.

**Открытый риск:** шоты 4, 6, 9 — мультиспикерные (в кадре либо говорят оба персонажа по очереди, либо
звучит закадровая реплика второго персонажа). У Wan 2.7 один слот `audio_references` на клип; промпты
для этих шотов явно прописывают, чья реплика звучит в какой момент и что лицо в кадре должно
молчать/слушать во время чужих слов, но фонемная точность на нескольких голосах в одной дорожке пока не
протестирована отдельно — стоит проверить на одном из этих трёх шотов перед тем, как гнать всю сцену.
