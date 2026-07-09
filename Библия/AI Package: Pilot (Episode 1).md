# AI Package: Pilot (Episode 1)

This AI Package provides prompts and notes for generating the keyframes and video shots described in
the Shot List. For each shot we define a GPT Image prompt (to create a still frame reference), a
negative prompt (to guide the model away from undesired elements), a Kling 3.0 Standard prompt (to animate the shot
from the reference), continuation notes for linking shots, motion instructions, a continuity
checklist and rendering notes. Prompts focus on the DreamWorks-style 3D animated look established in
the character reference sheets (Визуализации/), consistent character appearance and adherence to the
Visual Bible.

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
  of her hair in the night breeze. Maintain 50 mm virtual lens and shallow depth of field; candle and
  city lights should flicker naturally."

- Continuation: Seamlessly cut to shot 3 as Leo enters. Vanessa maintains position and gaze.

- Motion notes: Handheld sway mimics breathing. Ensure push-in speed is constant.

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

- Kling 3.0 Standard prompt: "Animate Leo entering from the apartment doorway into the balcony space, DreamWorks-style
  3D animation. The camera (virtual steadicam) follows him in a smooth arc towards Vanessa. Use a 50 mm
  virtual lens with shallow depth of field; keep the candle flicker and city backdrop. Duration 5 s."

- Continuation: Leads into shot 4 where Leo stands beside Vanessa.

- Motion notes: Smooth steadicam; slight parallax as camera arcs around the balcony table.

- Continuity checklist: Both mugs should be identical; Leo's hair neat; clothing matches Character
  Bible and reference sheet; city view matches previous shots.

- Rendering notes: Balanced exposure; warm tones on faces; cool bokeh in background.

## Shot 4 – Two-Shot (Balcony)

- GPT Image prompt: "Two DreamWorks-style 3D animated characters, Vanessa and Leo, stand side by side
  on a balcony at night, each holding a mug. Leo gazes softly at Vanessa; she looks down shyly. Warm
  candlelight illuminates their faces while the Moscow skyline blurs behind them. 50 mm virtual lens,
  cinematic 3D animated lighting."

- Negative prompt: "No dramatic backlighting, no glamorous fashion beyond reference sheets, no visible
  rig/skeleton artifacts, no lens flares, no photoreal skin."

- Kling 3.0 Standard prompt: "Start from the reference image of both characters on the balcony, DreamWorks-style 3D
  animation. Perform a slow dolly inwards for 4 s while the characters take small sips and exchange
  glances. Keep a 50 mm virtual lens; handheld breathing motion. Warm tones should dominate the
  foreground with cool bokeh in the background."

- Continuation: Cuts to close-ups (shots 5–6) to emphasise dialogue and emotion.

- Motion notes: Dolly speed slow; maintain equal distance to both characters.

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

- Kling 3.0 Standard prompt: "Hold the close-up of Leo delivering his heartfelt speech for 5 s, DreamWorks-style 3D
  animation. The camera remains static with micro-jitters to emulate handheld. Maintain an 85 mm
  virtual lens; ensure the light source flickers subtly on his face."

- Continuation: After his line, cut to shot 6 for Vanessa's reaction.

- Motion notes: Micro-jitters only; no rack focus.

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

- Kling 3.0 Standard prompt: "Hold the close-up of Vanessa reacting for 5 s, DreamWorks-style 3D animation. The camera
  is static with subtle handheld sway. Maintain 85 mm virtual lens and shallow depth of field. Her eyes
  flicker as she processes Leo's words."

- Continuation: Crossfade to shot 7 (insert of cups) as conversation ends.

- Motion notes: Slight breathing movement; ensure eyes stay in focus.

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

- Kling 3.0 Standard prompt: "Animate the two characters already in conversation, DreamWorks-style 3D animation. Leo
  delivers his line calmly, almost warmly; Vanessa opens her mouth to respond and is gently cut off.
  Camera is static at eye level with a barely perceptible push-in as the exchange lands. Maintain a
  50 mm virtual lens. Duration 6 s."

- Continuation: Cut to shot 10 on Vanessa as she answers.

- Motion notes: Push-in must stay almost invisible — the visual tone should not telegraph conflict; the
  words should carry all of the tension.

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

- Kling 3.0 Standard prompt: "Hold the close-up of Vanessa delivering her line for 4 s, DreamWorks-style 3D animation.
  Camera static, shallow depth of field. Her delivery is quiet and plain, not a complaint — the first
  time in the episode she names her feelings directly."

- Continuation: Cut to shot 11 on Leo's response.

- Motion notes: Minimal movement; hold on her eyes.

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

- Kling 3.0 Standard prompt: "Hold the close-up of Leo delivering his reframe for 5–6 s, DreamWorks-style 3D
  animation, including a brief pause before his last line. Camera static, shallow depth of field.
  Delivery should read as loving and reasonable, not cruel — the manipulation is entirely in the words."

- Continuation: Cut to shot 12 on Vanessa's question.

- Motion notes: Minimal movement; hold through the pause without cutting away.

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

- Kling 3.0 Standard prompt: "Hold the close-up of Vanessa asking her question for 3–4 s, DreamWorks-style 3D
  animation. Camera static with slight rack focus to keep her eyes sharp. Delivery is calm and sincere,
  almost tender — not a challenge."

- Continuation: Cut to shot 13 on Leo's reaction.

- Motion notes: Slight rack focus only; no other movement.

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
  micro-expression: a barely perceptible widening of the eyes or falter in his usual calm, held for a
  beat, then smoothed back over as he regains his composure. Camera static, held slightly longer than a
  normal reaction shot."

- Continuation: Cut to shot 14 on Vanessa looking away.

- Motion notes: The entire shot is the micro-expression; no camera movement.

- Continuity checklist: This is the first shot in the whole episode where Leo's face shows something he
  didn't choose to show — keep it subtle enough that it rewards a close rewatch rather than announcing
  itself.

- Rendering notes: Same warm light as shot 11, but read slightly harder/flatter to mark the shift.

## Shot 14 – Close-up on Vanessa, Looking Away (Kitchen, no dialogue)

- GPT Image prompt: "Close-up of Vanessa, DreamWorks-style 3D animated character, holding a steady gaze
  for a beat before looking down and away. Calm, unresolved expression — neither defiant nor defeated.
  Matches her character reference sheet exactly. 85 mm virtual lens, shallow depth of field, cinematic
  3D animated lighting."

- Negative prompt: "No tears, no smiling, no triumphant expression, no photoreal rendering."

- Kling 3.0 Standard prompt: "Hold on Vanessa for 3 s, DreamWorks-style 3D animation, no dialogue. She holds his gaze,
  then slightly tilts her head down and looks away. Camera static with a slight tilt down following her
  gaze."

- Continuation: Cut to shot 15, the closing cups insert.

- Motion notes: Slight tilt down only, timed to her gaze shift.

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
  reference for the Kling 3.0 Standard animations, and must match the character reference sheets in Визуализации/.

- Negative prompts explicitly exclude photorealism/live-action rendering and comedic/chibi
  proportions to keep the tone consistent with a mature, cinematic animated drama.

- Kling 3.0 Standard prompts should describe movement, virtual lens, duration and mood succinctly. Use "start from the
  reference image" as a baseline.

- Continuity checklists should be consulted by the person responsible for visual consistency before and
  after each generation pass.

- Rendering notes remind the compositing team of the desired DreamWorks-style 3D look (no film grain,
  no photoreal skin) and aspect ratio (9:16 vertical for social media).

## Open Issue: Lip Sync

Kling 3.0 Standard does not lip-sync mouth movement to the actual dialogue text — a shot generated from
a prompt like "he speaks softly" produces generic talking motion, not phoneme-accurate lip movement for
the Russian line in Dialogue: Pilot (Episode 1).md. This still needs a resolved pipeline before final
production. Working plan (not yet finalized):

1. Generate the silent/generic-talking Kling clip per shot as described above.
2. Generate the Russian voice line via TTS in a consistent voice per character (voice choice — preset
   vs. cloned — still TBD; whichever is picked should be documented in Character Bible alongside each
   character's other consistency markers, e.g. colour palette).
3. Run a dubbing/lip-sync pass (e.g. the `dubbing` tool, target_language=rus) over the silent clip with
   the real line to re-sync the mouth. Unverified whether this works on a clip with no original audio
   track — test on a single shot before committing to the full episode.
