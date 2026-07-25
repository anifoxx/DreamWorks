# AI Package: Episode 2 — «Подарок» (Love Bombing)

GPT Image (стили-кадры) + Kling 3.0 Standard (видео), вертикаль 9:16, DreamWorks-style 3D
animation — тот же пайплайн, что и в пилоте. Полный процесс липсинка и постпродакшна
описан в «AI Package: Pilot (Episode 1).md» («✅ Липсинк решён»); здесь применяем его
выводы сразу, без повторного нащупывания:

- Реплики цитируются в Kling-промпте в **испанской орфографической транслитерации**
  (вариант 2 из пилота) сразу, а не после того как Kling выдаст английский перевод —
  это сэкономит цикл проб и ошибок.
- Реальная озвучка генерируется отдельно (`generate_audio`, `text2speech_v2`/`minimax`,
  голоса Sienna/Caspian — или Arty Grumson для Лео, если решим перенести голос из
  пилота) и накладывается локально через ffmpeg по той же схеме (silencedetect → adelay
  → atempo при необходимости).
- **Шот 8 — исключение.** Реплик там нет вообще (немой шот под музыку), поэтому Kling-
  промпт не содержит цитаты и `sound: on` не требуется; TTS/дубляж этому шоту не нужны.

## Shot 1 — Insert/Establishing (Table Set)

- GPT Image prompt: "Insert shot of a dining table set unusually for the evening in a
  modern apartment, DreamWorks-style 3D animation. Two lit candles, a small box wrapped
  with ribbon on the table. Warm candlelight dominates, soft evening dusk light through a
  window behind. Cinematic 3D animated lighting, shallow depth of field on the box."

- Negative prompt: "No characters visible, no photoreal rendering, no clutter."

- Kling input: первый кадр, без реплик, `sound: off` (окружающий шум по желанию).

- Kling 3.0 Standard prompt: "Static insert shot holding on the wrapped box and candles,
  DreamWorks-style 3D animation. Slow, subtle push-in toward the box. Warm candlelight
  flickers. Near the end of the shot, Vanessa appears in the doorway in soft focus behind,
  noticing the table — her reaction stays soft focus, this shot belongs to the table."

- Continuation: Cut to shot 2.

- Motion notes: Minimal movement; push-in should feel unhurried, establishing anticipation
  rather than urgency.

- Continuity checklist: Same apartment interior as established; candle style consistent
  with Vanessa's evening ritual (see Character Bible: "часто зажигает свечу вечером").

- Rendering notes: Warm/cool contrast identical to Visual Bible's intimacy palette.

## Shot 2 — Two-Shot (The Box)

- GPT Image prompt: "Two-shot of Leo and Vanessa in their apartment, DreamWorks-style 3D
  animated characters, evening candlelight. Leo (tall, light brown wavy hair neatly
  styled, blue eyes with a warm-but-hollow quality, square jaw, light stubble, small scar
  above right eyebrow, in a dark navy smart-casual shirt) holds out a ribboned box toward
  Vanessa (dark chestnut wavy hair in a loose low ponytail, big green eyes, soft features,
  small mole on left cheek, wearing a rich emerald or ink-blue top). Her expression is
  surprised, curious. 50 mm virtual lens, cinematic 3D animated lighting."

- Negative prompt: "No smirk on Leo, no forced/exaggerated surprise on Vanessa, no
  photoreal rendering."

- **Kling input: первый кадр, `sound: on`.** Оба в кадре, реплики короткие и раздельные —
  чистый случай. Реальная реплика: Лео — «Вот. Ничего особенного.» (голос «Caspian»/Arty
  Grumson — уточнить), Ванесса — «С чего вдруг?» (голос «Sienna»).

- Kling 3.0 Standard prompt: "Static two-shot, DreamWorks-style 3D animation, slight
  handheld breathing. Leo holds out the box and says (in Spanish): 'Vot. Nichevó
  asóbennovo.' — his tone light, warm, deliberately casual. Vanessa looks at the box, then
  at him, and says (in Spanish): '¿S chevó vdruk?' — genuinely surprised, not suspicious.
  Camera static, warm candlelight on both faces."

- Continuation: Cut to shot 3.

- Motion notes: Slight handheld sway only; no push-in yet, saving that for shot 8.

- Continuity checklist: Leo's stubble/hair per reference sheet; Vanessa's mole and hair
  part consistent.

- Rendering notes: Warm light dominant, matching Visual Bible's intimacy cues.

## Shot 3 — Close-up on Vanessa (Unwrapping)

- GPT Image prompt: "Close-up of Vanessa, DreamWorks-style 3D animated character,
  unwrapping a small box and recognising a vintage vinyl record inside, her face lighting
  up with surprised recognition, not generic excitement — this specific gift means
  something. Big green eyes, soft features, small mole on left cheek, dark chestnut wavy
  hair. Warm candlelight, 85 mm virtual lens, shallow depth of field, cinematic 3D
  animated lighting."

- Negative prompt: "No exaggerated gasp, no photoreal rendering."

- **Kling input: первый кадр, `sound: on`.** Один говорящий в кадре. Реальная реплика:
  Ванесса — «Ты... я же сказала это один раз, мельком.» (голос «Sienna»).

- Kling 3.0 Standard prompt: "Hold the close-up of Vanessa looking at the record in her
  hands, DreamWorks-style 3D animation. She says (in Spanish): 'Ti... Ya zhe skazála éto
  odín raz, myél'kam.' — her face reads quiet disbelief that he remembered something this
  small. Camera static, shallow depth of field."

- Continuation: Cut to shot 4.

- Motion notes: No camera movement; the record itself can be visible in frame (vintage
  sleeve, Chopin nocturnes).

- Continuity checklist: Same mole/hair as reference sheet; record art should read as
  vintage/worn, not new.

- Rendering notes: Warm candlelight on her face, background softly blown out.

## Shot 4 — Close-up on Leo (The Line)

- GPT Image prompt: "Close-up of Leo, DreamWorks-style 3D animated character, delivering a
  warm, disarming line with a light smile — charming, not smug. Matches reference sheet:
  light brown wavy hair, blue eyes, square jaw, small scar above right eyebrow, light
  stubble. Warm candlelight, 85 mm virtual lens, shallow depth of field, cinematic 3D
  animated lighting."

- Negative prompt: "No smirk, no villain caricature, no photoreal rendering."

- **Kling input: первый кадр, `sound: on`.** Реальная реплика: Лео — «Я запоминаю то, что
  важно для тебя.» (голос «Caspian»/Arty Grumson).

- Kling 3.0 Standard prompt: "Hold the close-up of Leo, DreamWorks-style 3D animation. He
  says (in Spanish): 'Ya zapaminayú to, shto vázhna dlya tebyá.' — light, easy smile,
  completely convincing warmth, no calculation visible on the surface. Camera static,
  shallow depth of field."

- Continuation: Cut to shot 5.

- Motion notes: Minimal movement; the same 'caring' half-smile established in the pilot's
  reference poses should read here.

- Continuity checklist: Hair/stubble/scar per reference sheet.

- Rendering notes: Warm light on his face, background softly blown out.

## Shot 5 — Close-up on Vanessa (Touched)

- GPT Image prompt: "Close-up of Vanessa, DreamWorks-style 3D animated character, visibly
  touched and slightly overwhelmed by the gesture, soft vulnerable warmth in her eyes.
  Matches reference sheet. Warm candlelight, 85 mm virtual lens, shallow depth of field,
  cinematic 3D animated lighting."

- Negative prompt: "No crying, no exaggerated emotion, no photoreal rendering."

- **Kling input: первый кадр, `sound: on`.** Реальная реплика: Ванесса — «Не нужно было...»
  (голос «Sienna»).

- Kling 3.0 Standard prompt: "Hold the close-up of Vanessa, DreamWorks-style 3D animation.
  She says (in Spanish), trailing off: 'Ne núzhna bíla...' — soft, moved, voice trailing
  into the pause. Camera static, shallow depth of field."

- Continuation: Cut to shot 6.

- Motion notes: No movement; let the trailing line breathe before the cut.

- Continuity checklist: Mole, hair, expression consistent with reference sheet.

- Rendering notes: Warm light, same palette as shot 3/5 for continuity.

## Shot 6 — Close-up on Leo (The Hook)

- GPT Image prompt: "Close-up of Leo, DreamWorks-style 3D animated character, looking away
  slightly, voice dropping — a flicker of rehearsed vulnerability crossing his face, not
  full sadness, something more controlled and performed. Matches reference sheet. Light
  dims very slightly compared to earlier shots. 85 mm virtual lens, shallow depth of
  field, cinematic 3D animated lighting."

- Negative prompt: "No overt tears, no melodrama, no photoreal rendering — this must read
  as controlled, not raw."

- **Kling input: первый кадр, `sound: on`.** Реальная реплика: Лео — «Мне не сложно. У меня
  никогда не было того, кому можно дарить просто так. В детстве... неважно.» (голос
  «Caspian»/Arty Grumson).

- Kling 3.0 Standard prompt: "Hold the close-up of Leo, DreamWorks-style 3D animation. He
  looks slightly away, voice quieter, and says (in Spanish): 'Mnye ne slózhna. U menyá
  nikagdá ne bíla tavó, kamú mózhna darít' prósta tak. V détstve... nevázhna.' — he cuts
  himself off on the last words, as if deciding not to go further, but the delivery is
  just a touch too composed for genuine raw pain — controlled vulnerability, not
  breakdown. Camera static, shallow depth of field."

- Continuation: Cut to shot 7.

- Motion notes: The look-away should be small, deliberate, not a full head turn.

- Continuity checklist: Hair/stubble/scar per reference sheet.

- Rendering notes: Light dims marginally from prior shots — first subtle shift toward the
  emotional pivot of the episode.

## Shot 7 — Close-up on Vanessa (Opening the Door)

- GPT Image prompt: "Close-up of Vanessa, DreamWorks-style 3D animated character, gently
  inviting him to continue — soft, open, no hesitation, she wants to know. Matches
  reference sheet. Warm candlelight, 85 mm virtual lens, shallow depth of field, cinematic
  3D animated lighting."

- Negative prompt: "No forced concern, no photoreal rendering."

- **Kling input: первый кадр, `sound: on`.** Реальная реплика: Ванесса — «Расскажи.»
  (голос «Sienna»).

- Kling 3.0 Standard prompt: "Hold the close-up of Vanessa, DreamWorks-style 3D animation.
  She says softly (in Spanish): 'Rasskazhí.' — gentle invitation, not prying. Camera
  static, shallow depth of field."

- Continuation: Cut to shot 8.

- Motion notes: None; this is the pivot line into the silent sequence.

- Continuity checklist: Consistent with reference sheet.

- Rendering notes: Same warm palette as preceding close-ups.

## Shot 8 — Two-Shot / Alternating Close-ups, SILENT (No Dialogue, No TTS)

- GPT Image prompt (reference frame, two-shot): "Two-shot of Leo and Vanessa already
  seated close together on a couch, knee to knee, shoulders touching, warm candlelight,
  DreamWorks-style 3D animation — mid ordinary, easy conversation, both animated and
  relaxed, not posed. Leo holds an old, worn photograph, his expression caught mid-
  sentence with a flicker of genuine-looking vulnerability. Vanessa leans in, one hand
  resting over his. Matches both reference sheets exactly (Leo: light brown/dirty-blonde
  wavy hair — not dark brown). Cinematic 3D animated lighting, intimate framing."

- GPT Image prompt (insert, the photograph itself — needs to exist as a distinct
  reference asset): "A small, worn photograph, DreamWorks-style 3D animated illustration
  style: a boy of about eight stands alone at a school recital holding a certificate or
  award, looking toward camera; in the background, slightly out of focus, his mother is
  turned away, mid-conversation with someone else, not looking at him. On the reverse
  side of the photo (separate framing/insert), handwritten in warm ink: 'Лёвушка, я так
  тобой горжусь' — the Cyrillic text must render clearly and legibly. Same date visible
  near the inscription."

- Negative prompt: "No spoken dialogue, no lip-sync to any line, no legible mismatch in
  the handwriting style, no photoreal rendering, no melodrama in expressions."

- **Kling input: первый или первый+последний кадр, `sound: off` (без реплик). Никакой
  реальной реплики нет — шот полностью немой, музыка накладывается отдельно в монтаже.
  Мимика и жесты играют реплику визуально; TTS/дубляж не требуются.**

- Kling 3.0 Standard prompt: "Silent sequence, DreamWorks-style 3D animation, no audible
  dialogue at all — performance is entirely visual. Open on Leo and Vanessa already
  seated close together on a couch, knee to knee, mid ordinary conversation — both
  animated, gesturing, silently laughing, natural back-and-forth energy, completely at
  ease. A beat in, Leo takes an old photograph from his pocket; the mood shifts, he speaks
  quieter, lips still moving with no words meant to be heard, and for a moment his usual
  composure drops, something more genuine-looking flickers across his face. Vanessa leans
  in closer, takes his hand. She turns the photograph over mid-gesture — the handwritten
  inscription is visible for a beat. A barely perceptible flicker crosses her face, gone
  almost as soon as it appears. Leo takes the photograph back, a fraction too quickly to
  be entirely casual; she doesn't react to that either. The easy, warm conversation
  resumes as she rests her head on his shoulder. Camera holds a slow, gentle drift/push-in
  throughout, alternating with a brief insert of the photograph close enough to read the
  inscription. No sound cues, no dialogue. Leo: light brown/dirty-blonde wavy hair per
  reference sheet, not dark brown."

- Continuation: Cut to shot 9.

- Motion notes: Slow push-in throughout; the photograph insert should be held just long
  enough for the inscription to register, without lingering suspiciously. Vanessa's
  flicker must stay subtle — same discipline as the pilot's shot 6c fix (dominant emotion
  stays warm, the doubt is a flicker, not a held expression).

- Continuity checklist: Both characters per reference sheets; photograph must look
  genuinely aged/worn (not a clean modern print) to sell the "old photo" premise.

- Rendering notes: Warmest lighting in the episode — this is the emotional peak. No music
  or SFX baked into the render; left clean for the producer's own music layer.

## Shot 9 — Insert, Episode Closer (The Photo on the Shelf)

- GPT Image prompt: "Insert shot, DreamWorks-style 3D animation: the same worn photograph,
  now in a small frame, standing on a shelf next to a framed photo of Leo and Vanessa
  together as a couple. Warm evening light, cinematic 3D animated lighting, shallow depth
  of field."

- Negative prompt: "No characters visible, no photoreal rendering."

- Kling input: первый кадр, без реплик, `sound: off`.

- Kling 3.0 Standard prompt: "Static insert shot holding on the two framed photographs
  side by side on the shelf, DreamWorks-style 3D animation. Very slow, almost
  imperceptible push-in. Warm light holds steady. No characters, no dialogue."

- Continuation: Fade out / cut to Episode 3.

- Motion notes: Minimal; this insert should feel like a quiet exhale, mirroring the
  pilot's cups-insert technique.

- Continuity checklist: The couple photo should look consistent with an established shared
  life (same apartment visible in background if relevant).

- Rendering notes: Same warm palette as shot 1, bookending the episode visually.

## Model & Input Summary

| Shot | Реплика | Голос | Kling input | TTS/дубляж нужен |
|------|---------|-------|-------------|-------------------|
| 1 | — | — | первый кадр, sound off | Нет |
| 2 | Лео + Ванесса | Caspian/Arty Grumson + Sienna | первый кадр, sound on | Да |
| 3 | Ванесса | Sienna | первый кадр, sound on | Да |
| 4 | Лео | Caspian/Arty Grumson | первый кадр, sound on | Да |
| 5 | Ванесса | Sienna | первый кадр, sound on | Да |
| 6 | Лео | Caspian/Arty Grumson | первый кадр, sound on | Да |
| 7 | Ванесса | Sienna | первый кадр, sound on | Да |
| 8 | — (немой) | — | первый/+последний, sound off | **Нет** |
| 9 | — | — | первый кадр, sound off | Нет |

7 из 9 шотов требуют дубляжа (меньше, чем в пилоте, за счёт немого шота 8 и двух чистых
инсертов).
