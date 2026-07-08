# AI Package: Pilot (Episode 1)

This AI Package provides prompts and notes for generating the keyframes and video shots described in
the Shot List. For each shot we define a GPT Image prompt (to create a still frame reference), a
negative prompt (to guide the model away from undesired elements), a Veo prompt (to animate the shot
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

- Veo prompt: "Start with the still frame of the wide balcony at night, DreamWorks-style 3D animation.
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

- Veo prompt: "Begin with the reference image of Vanessa gazing at the city, DreamWorks-style 3D
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

- Veo prompt: "Animate Leo entering from the apartment doorway into the balcony space, DreamWorks-style
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

- Veo prompt: "Start from the reference image of both characters on the balcony, DreamWorks-style 3D
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

- Veo prompt: "Hold the close-up of Leo delivering his heartfelt speech for 5 s, DreamWorks-style 3D
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

- Veo prompt: "Hold the close-up of Vanessa reacting for 5 s, DreamWorks-style 3D animation. The camera
  is static with subtle handheld sway. Maintain 85 mm virtual lens and shallow depth of field. Her eyes
  flicker as she processes Leo's words."

- Continuation: Crossfade to shot 7 (insert of cups) as conversation ends.

- Motion notes: Slight breathing movement; ensure eyes stay in focus.

- Continuity checklist: Hair parting consistent with reference sheet; jewellery (pendant) visible;
  candlelight flicker.

- Rendering notes: Balanced highlights; maintain warm key light and cool rim.

## Shot 7 – Insert of Cups (Night–Morning Transition)

- GPT Image prompt: "Close overhead view of two white ceramic mugs on a balcony table at night,
  DreamWorks-style 3D animated render. A small candle burns beside them. The mugs are nearly full. The
  city skyline is blurred in the background. 35 mm virtual lens, cinematic 3D animated lighting."

- Negative prompt: "No human figures, no messy table, no neon colours, no photoreal rendering."

- Veo prompt: "Begin with the reference image of the cups at night, DreamWorks-style 3D animation. Hold
  for 2 s, then slowly dissolve to the same composition at dawn. The liquid in the cups is unchanged.
  Maintain 35 mm virtual lens and static camera. Duration 5 s."

- Continuation: Dissolve into shot 8 establishing the kitchen.

- Motion notes: Use dissolve transition to convey passage of time.

- Continuity checklist: Cup positions unchanged; candle may have burned down slightly; mugs match props
  list.

- Rendering notes: Ensure seamless blend between night and morning colour temperatures. Night image
  uses cool blue shadows; morning uses soft warm daylight.

## Shot 8 – Establishing Shot (Kitchen)

- GPT Image prompt: "Wide vertical shot of a modern, open-plan kitchen in morning light,
  DreamWorks-style 3D animated render. Floor-to-ceiling windows flood the space with cool daylight. Two
  cups from the previous night sit on a wooden table. Sleek cabinets and a marble island are visible.
  35 mm virtual lens, cinematic 3D animated lighting."

- Negative prompt: "No people, no clutter, no harsh shadows, no trendy neon, no photoreal rendering."

- Veo prompt: "Start with the still frame of the empty kitchen at dawn, DreamWorks-style 3D animation.
  Hold for 2 s, then gently push in towards the table for 4 s, drawing attention to the cups. Use a
  35 mm virtual lens and tripod. Natural morning light shifts slightly as the sun rises."

- Continuation: Cut to shot 9 as Leo enters.

- Motion notes: Slow push-in; emphasise quiet morning atmosphere.

- Continuity checklist: Cups unchanged from balcony; window view matches World Bible; lighting
  consistent with time of day.

- Rendering notes: Colour temperature cool but softened; clean stylized render; highlights not blown.

## Shot 9 – Leo Cooking (Kitchen)

- GPT Image prompt: "Medium shot of Leo, DreamWorks-style 3D animated character, cooking breakfast in a
  modern kitchen. Russet/blond wavy hair, light sweater matching his reference sheet. The sun casts a
  cool morning glow through the windows while warm light from a pendant lamp illuminates him. 50 mm
  virtual lens, cinematic 3D animated lighting."

- Negative prompt: "No messy countertops, no futuristic appliances, no saturated toon colours, no
  photoreal rendering."

- Veo prompt: "Animate Leo cracking eggs and stirring food at the stove, DreamWorks-style 3D animation.
  The camera is virtual handheld, with slight micro-movement as if by a person watching him from a
  distance. Use a 50 mm virtual lens and maintain natural light interplay for 5 s."

- Continuation: Cut to shot 10 as Vanessa enters.

- Motion notes: Subtle handheld; keep focus on Leo's hands and face.

- Continuity checklist: Wardrobe, hair as per Character Bible and reference sheet; kitchen props in
  place; cups visible in background.

- Rendering notes: Combine cool daylight and warm stove light; maintain soft shadows.

## Shot 10 – Vanessa Enters (Kitchen)

- GPT Image prompt: "Medium shot of Vanessa, DreamWorks-style 3D animated character, walking into a
  modern kitchen in morning light. Long dark wavy hair matching her reference sheet. She notices two
  cups on the table and smiles softly. 50 mm virtual lens, cinematic 3D animated lighting."

- Negative prompt: "No exaggerated smile, no hurried cartoon movement, no unrealistic costumes, no
  photoreal rendering."

- Veo prompt: "Animate Vanessa walking into the kitchen, pausing to glance at the cups, then moving
  toward the table, DreamWorks-style 3D animation. The camera (virtual steadicam) follows from behind,
  panning to her side as she reacts. Use a 50 mm virtual lens; duration 5 s."

- Continuation: Cut to shot 11 for the breakfast conversation.

- Motion notes: Smooth follow; slight pan reveals her reaction.

- Continuity checklist: Vanessa's hair and clothing consistent with reference sheet; cups positioned as
  in shot 8; morning light consistent.

- Rendering notes: Maintain natural colour temperature; keep depth of field moderate to separate her
  from background.

## Shots 11–14 – Breakfast Dialogue and Close-ups

For the remaining shots (table conversation, close-ups and insert), follow similar structure:

- GPT Image prompts should describe both DreamWorks-style 3D animated characters seated at a modern
  kitchen table in the morning, with warm and cool light interplay. Close-ups focus on faces,
  emphasising micro-expressions and subtle mood shifts as shown on the reference sheets' emotion rows.

- Negative prompts should avoid photorealism, melodrama, theatrical lighting, or comedic/chibi
  proportions.

- Veo prompts should specify static or slight push-in virtual camera, maintain lens consistency (50 mm
  for two-shot, 85 mm for close-ups), and indicate the duration (4–5 s) with natural pauses for dialogue
  delivery. For the final insert of the cups (shot 14), specify an overhead static shot and a slow fade
  out.

- Motion notes should highlight small movements: hand gestures, head tilts, eye contact.

- Continuity checklist should ensure props (cups, plates), wardrobe and hair remain consistent with the
  character reference sheets; emotional progression aligns with Episode Design.

- Rendering notes should maintain the established DreamWorks-style 3D look, clean stylized shading and
  balanced lighting.

## General Notes

- All GPT Image prompts should be used to generate high-resolution keyframes that capture the
  composition, lighting, mood and DreamWorks-style 3D render of each shot. These images become the
  reference for the Veo animations, and must match the character reference sheets in Визуализации/.

- Negative prompts explicitly exclude photorealism/live-action rendering and comedic/chibi
  proportions to keep the tone consistent with a mature, cinematic animated drama.

- Veo prompts should describe movement, virtual lens, duration and mood succinctly. Use "start from the
  reference image" as a baseline.

- Continuity checklists should be consulted by the person responsible for visual consistency before and
  after each generation pass.

- Rendering notes remind the compositing team of the desired DreamWorks-style 3D look (no film grain,
  no photoreal skin) and aspect ratio (9:16 vertical for social media).
