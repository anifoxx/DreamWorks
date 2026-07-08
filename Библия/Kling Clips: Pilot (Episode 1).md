# Kling Clips: Pilot (Episode 1)

Пилот разбит на 4 видеоролика по ≈15 секунд (итого ≈60 с — весь эпизод). Модель генерации: **Kling 3.0
Standard**, image-to-video (стартовый кадр + текстовый промпт), формат 9:16.

Важно: Kling генерирует один непрерывный кадр за проход, без внутренних монтажных склеек. Поэтому
каждый ролик спроектирован как **одно непрерывное движение камеры**, которое проходит через все нужные
драматические точки шот-листа (вместо жёсткой нарезки на отдельные шоты). Соответствие шотам из Shot
List указано в скобках — это для монтажёра/референса, а не для склейки внутри генерации.

Раскадровка на каждый ролик — один составной сториборд-кадр (вертикальная полоса панелей сверху вниз) —
служит **только** референсом для арт-дирекшена и питчинга. **В Kling эту составную картинку подавать
нельзя** — модель анимирует ровно то изображение, которое получает, включая рамки панелей, номера и
пунктирные направляющие (именно так и получилась «дичь» в первой версии). Для реальной генерации в Kling
у каждого ролика есть отдельный **«Стартовый кадр»** — одно чистое изображение без панелей, разметки и
номеров, соответствующее самой первой точке ролика. Именно его нужно сгенерировать отдельно и подать в
Kling как image-to-video референс.

## Ролик 1 (0:00–0:15) — «Балкон: она одна → входит Лео» (шоты 1–4)

**Раскадровка (промпт для генерации составного сториборда, GPT Image):**

> «Vertical 4-panel storyboard strip, single image, panels stacked top to bottom with thin white gutters
> and small numbered labels (1–4), DreamWorks-style 3D animated render, cinematic 3D lighting, consistent
> character design matching reference sheets. Panel 1: wide establishing shot of a modern Moscow
> high-rise balcony at night, city lights glittering in the distance, balcony silhouetted, warm candle
> glow. Panel 2: medium shot of Vanessa (long dark wavy hair, emerald-green eyes, elegant old-money coat)
> standing alone at the balcony railing wrapped in a blanket, looking out at the city. Panel 3: medium
> shot of Leo (russet/blond wavy hair, bright blue eyes, dark minimalist sweater) stepping onto the
> balcony carrying two mugs, approaching Vanessa. Panel 4: two-shot of Leo and Vanessa standing together
> at the railing, both holding mugs, warm candlelight on their faces, city skyline blurred behind them.
> 9:16 vertical crop guides within each panel.»

**⚠️ Не подавать в Kling.** Используется только для планирования; иначе Kling заанимирует лист с
рамками и цифрами (как в первой неудачной версии).

**Стартовый кадр для Kling (GPT Image, ОДНО чистое изображение, без панелей):**

> «Wide establishing shot of a modern Moscow high-rise balcony at night, DreamWorks-style 3D animated
> render. City lights glittering in the distance, balcony railing and a small table with a candle
> silhouetted in the foreground. No characters in frame. 35 mm virtual lens, cinematic 3D animated
> lighting, deep blue night sky, warm candle glow, clean stylized render. Single full-frame image, no
> panels, no borders, no text, no numbers.»

**Негативный промпт (для стартового кадра и для видео):** «No photorealism, no live-action, no
chibi/comedic proportions, no text, numbers, panel borders or watermarks, no extra characters, no
distorted hands or faces, no split-screen or grid composition.»

**Промпт для Kling 3.0 Standard (видео, 15 с, от этого стартового кадра):**

> «Cinematic 3D animated short, DreamWorks-style, vertical 9:16. A modern Moscow balcony at night, warm
> candlelight, city skyline glittering in the distance. Camera holds on the wide static shot of the
> empty balcony for a beat, then slowly pushes in toward a woman standing alone at the railing, wrapped
> in a blanket, gazing at the city. A man steps out from the apartment doorway carrying exactly two
> mugs; camera follows him in a smooth arcing move as he crosses to stand beside her. They settle into a
> warm two-shot, each now holding one of the same two mugs, exchanging a tender glance — no additional
> mugs appear anywhere in the shot. Slow, steady continuous camera movement throughout — no cuts, no
> shake, single unbroken take, no split-screen. Soft naturalistic warm-and-cool lighting, shallow depth
> of field, gentle handheld breathing motion. Duration 15 seconds.»

**Что происходит по хронометражу:** 0–4с статичный общий план → 4–9с наезд на Ванессу → 9–15с приход
Лео и переход в двухкадр (реплики «Замёрзла?» / «Спасибо…» / «Мне — слышно…» ложатся на последние
секунды ролика).

## Ролик 2 (0:15–0:30) — «Признание Лео → реакция Ванессы → рассвет» (шоты 5–7)

**Раскадровка:**

> «Vertical 3-panel storyboard strip, single image, panels stacked top to bottom with thin white gutters
> and numbered labels (1–3), DreamWorks-style 3D animated render, cinematic 3D lighting. Panel 1:
> close-up of Leo speaking softly at night, warm candlelight on his face, dark bokeh city lights behind
> him, tender expression. Panel 2: close-up of Vanessa listening, warm candlelight on her cheeks, cool
> city-light rim, expression shifting between tenderness and a flicker of worry. Panel 3: close overhead
> view of two white ceramic mugs on the balcony table, nearly full, small candle beside them, city
> skyline blurred — lighting subtly shifting from night-blue toward dawn amber. 9:16 vertical crop guides
> within each panel.»

**⚠️ Не подавать в Kling.** Только для планирования.

**Стартовый кадр для Kling (GPT Image, ОДНО чистое изображение, без панелей):**

> «Close-up of Leo, DreamWorks-style 3D animated character, speaking softly at night. Russet/blond wavy
> hair, bright blue eyes, calm tender expression, matching his character reference sheet. Warm
> candlelight illuminates his features; the background is a dark bokeh of city lights. 85 mm virtual
> lens, shallow depth of field, cinematic 3D animated lighting. Single full-frame image, no panels, no
> borders, no text, no numbers.»

**Негативный промпт:** «No photorealism, no live-action, no tears, no smiling/smirking, no text, numbers,
panel borders or watermarks, no distorted hands or faces, no split-screen or grid composition.»

**Промпт для Kling 3.0 Standard (видео, 15 с, от этого стартового кадра):**

> «Cinematic 3D animated short, DreamWorks-style, vertical 9:16. Intimate night scene on a Moscow
> balcony. Camera holds close on a man's face as he speaks tenderly, warm candlelight flickering across
> his features. Camera slowly arcs around the table to reframe on a woman's face as she listens, her
> expression drifting between warmth and a brief flicker of worry before softening again. Camera then
> tilts down and pushes into a close overhead view of two mugs sitting on the table between them; over
> the final seconds the surrounding light gradually shifts from cool night-blue to warm dawn amber,
> as if time is quietly passing. Slow, continuous camera movement throughout — no hard cuts, no shake,
> single unbroken take, no split-screen. Shallow depth of field, soft candlelight, natural micro-movement.
> Duration 15 seconds.»

**Что происходит по хронометражу:** 0–5с крупный план Лео (реплики про знакомство/музу) → 5–10с разворот
камеры на Ванессу (её «Правда?», его ответ, её «…Хорошо») → 10–15с спуск к кружкам и переход света в
рассвет.

## Ролик 3 (0:30–0:45) — «Кухня: раскрытие → начало конфликта» (шоты 8–10)

**Раскадровка:**

> «Vertical 3-panel storyboard strip, single image, panels stacked top to bottom with thin white gutters
> and numbered labels (1–3), DreamWorks-style 3D animated render, cinematic 3D lighting. Panel 1:
> extreme close-up of two white ceramic mugs on a kitchen table in soft morning light, no characters
> visible. Panel 2: wide-to-medium view of a modern open-plan kitchen with Leo and Vanessa already
> standing together mid-conversation, warm morning light, no cooking props in use. Panel 3: close-up of
> Vanessa speaking quietly, calm but hurt expression, soft morning light on her face. 9:16 vertical crop
> guides within each panel.»

**⚠️ Не подавать в Kling.** Только для планирования.

**Стартовый кадр для Kling (GPT Image, ОДНО чистое изображение, без панелей):**

> «Extreme close-up of two white ceramic mugs on a kitchen table in soft morning light, DreamWorks-style
> 3D animated render. No characters visible. Exactly two mugs, both nearly full. 35 mm virtual lens,
> cinematic 3D animated lighting. Single full-frame image, no panels, no borders, no text, no numbers.»

**Негативный промпт:** «No photorealism, no live-action, no cooking utensils or food, no exaggerated
expressions, no text, numbers, panel borders or watermarks, no distorted hands or faces, no split-screen
or grid composition, no extra mugs.»

**Промпт для Kling 3.0 Standard (видео, 15 с, от этого стартового кадра):**

> «Cinematic 3D animated short, DreamWorks-style, vertical 9:16. A modern open-plan kitchen in soft
> morning light. Camera starts on an extreme close-up of exactly two mugs on the table, then slowly pulls
> back and cranes upward to reveal the kitchen around them — floor-to-ceiling windows, sleek cabinets, a
> marble island — where a man and a woman are already standing together, mid-conversation. Camera settles
> into a calm two-shot as he speaks gently; she begins to answer and is softly cut off. Camera then
> pushes in slowly to a close-up of her face as she quietly states how she feels, calm but hurt, not
> raising her voice. Slow, continuous camera movement throughout — no hard cuts, single unbroken take, no
> split-screen. Warm morning light, soft shadows, shallow depth of field on the final close-up. Duration
> 15 seconds.»

**Что происходит по хронометражу:** 0–5с крупный план кружек с отъездом → 5–9с раскрытая кухня,
двухкадр и первые реплики Лео → 9–15с наезд на Ванессу («Я не устраивала трагедию. Мне правда было
больно»).

## Ролик 4 (0:45–1:00) — «Манипуляция → обезоруживающий вопрос → финал» (шоты 11–15)

**Раскадровка:**

> «Vertical 4-panel storyboard strip, single image, panels stacked top to bottom with thin white gutters
> and numbered labels (1–4), DreamWorks-style 3D animated render, cinematic 3D lighting. Panel 1:
> close-up of Leo speaking gently, soft almost-tender expression, warm morning light. Panel 2: close-up
> of Vanessa asking a quiet question, calm and genuinely curious expression, soft morning light. Panel 3:
> extreme close-up of Leo with a fraction-of-a-second flicker of genuine surprise crossing his face
> before he catches himself. Panel 4: close overhead view of two mugs on the kitchen table, one still
> full, one already empty, neutral morning light, no characters. 9:16 vertical crop guides within each
> panel.»

**⚠️ Не подавать в Kling.** Только для планирования.

**Стартовый кадр для Kling (GPT Image, ОДНО чистое изображение, без панелей):**

> «Close-up of Leo, DreamWorks-style 3D animated character, speaking gently in warm morning light.
> Russet/blond wavy hair, bright blue eyes, soft almost-tender expression, matching his character
> reference sheet. 85 mm virtual lens, shallow depth of field, cinematic 3D animated lighting. Single
> full-frame image, no panels, no borders, no text, no numbers.»

**Негативный промпт:** «No photorealism, no live-action, no overt shock/wide eyes, no smirking, no
triumphant or tearful expressions, no text, numbers, panel borders or watermarks, no distorted hands or
faces, no split-screen or grid composition, no extra mugs.»

**Промпт для Kling 3.0 Standard (видео, 15 с, от этого стартового кадра):**

> «Cinematic 3D animated short, DreamWorks-style, vertical 9:16. Intimate kitchen scene in soft morning
> light. Camera holds a close two-shot framing on a man and a woman facing each other; focus rests on
> him as he speaks gently, warmly, almost tenderly. Camera subtly reframes/racks focus to her as she asks
> a quiet, sincere question, not challenging. Camera then holds on his face a beat longer than expected —
> a barely perceptible flicker of surprise crosses it before he smooths his composure back over, saying
> nothing. Camera slowly tilts down and pushes into a close overhead view of exactly two mugs on the
> table — one still full, one already empty — holding for the final moment before a slow fade to black.
> Slow, continuous camera movement throughout — no hard cuts, single unbroken take, no split-screen. Soft
> morning light, shallow depth of field. Duration 15 seconds, ending on a fade.»

**Что происходит по хронометражу:** 0–4с Лео («Может, стоит иначе… чтобы нам обоим было легче») → 4–7с
Ванесса («А тебе самому — легко?») → 7–11с реакция Лео (без слов) → 11–15с спуск к кружкам и фейд.

## Сводка

| Ролик | Тайминг | Шоты | Локация |
|---|---|---|---|
| 1 | 0:00–0:15 | 1–4 | Балкон |
| 2 | 0:15–0:30 | 5–7 | Балкон → переход |
| 3 | 0:30–0:45 | 8–10 | Кухня |
| 4 | 0:45–1:00 | 11–15 | Кухня |

Каждый ролик — отдельная генерация в Kling. Пайплайн такой:

1. Сгенерировать **«Стартовый кадр»** (одно чистое изображение, без панелей/номеров/рамок) по
   соответствующему промпту.
2. Подать этот кадр в Kling 3.0 Standard как image-to-video референс вместе с текстовым Kling-промптом
   ролика.
3. Составной сториборд (4-панельная полоса) используется **только** для внутреннего согласования
   раскадровки — в модель он никогда не подаётся.

Реплики внутри роликов не произносятся вслух моделью — Kling не генерирует синхронизированную речь;
текст реплик используется только как тайминг-ориентир для монтажа и последующей озвучки/липсинка
отдельным инструментом.
