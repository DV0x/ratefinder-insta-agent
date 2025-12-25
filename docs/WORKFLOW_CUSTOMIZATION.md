# Workflow Customization Guide

This guide explains how to tweak the fashion photoshoot pipeline to create different styles of photoshoots.

---

## Table of Contents

1. [Quick Reference: What You Can Change](#quick-reference-what-you-can-change)
2. [Customizing the Style Treatment](#1-customizing-the-style-treatment)
3. [Changing Camera Angles](#2-changing-camera-angles)
4. [Modifying Video Camera Movements](#3-modifying-video-camera-movements)
5. [Adjusting Video Transitions](#4-adjusting-video-transitions)
6. [Changing Image Settings](#5-changing-image-settings)
7. [Creating Alternative Workflow Presets](#6-creating-alternative-workflow-presets)
8. [Examples: Complete Alternative Workflows](#7-examples-complete-alternative-workflows)

---

## Quick Reference: What You Can Change

| Element | File to Edit | Impact |
|---------|--------------|--------|
| Film/Style treatment | `tim-workflow-templates.md` | Changes the visual aesthetic |
| Camera angles (6 shots) | `tim-workflow-templates.md` | Changes the contact sheet composition |
| Video movements | `tim-workflow-templates.md` | Changes how each clip animates |
| Transitions & easing | `stitch-videos.ts` call | Changes how clips blend together |
| Aspect ratio | Script `--aspect-ratio` flag | Changes image dimensions |
| Resolution | Script `--resolution` flag | Changes image quality (1K/2K/4K) |
| Video duration | Script `--duration` flag | 5 or 10 seconds per clip |
| Background | HERO_PROMPT template | Changes environment |

---

## 1. Customizing the Style Treatment

The current "Tim workflow" uses a Fuji Velvia film aesthetic. You can create completely different looks by modifying the style block.

### Current Style (Fuji Velvia)
**Location:** `agent/.claude/skills/editorial-photography/workflows/tim-workflow-templates.md`

```
The image is shot on fuji velvia film on a 55mm prime lens with a hard flash,
the light is concentrated on the subject and fades slightly toward the edges
of the frame. The image is over exposed showing significant film grain and is
oversaturated. The skin appears shiny (almost oily).
```

### Alternative Style Presets

#### Cinematic Black & White
```
The image is shot on Ilford HP5 Plus black and white film with a 85mm portrait
lens. Dramatic side lighting creates deep shadows and highlights. High contrast
with rich blacks and creamy whites. Visible film grain adds texture. The mood
is timeless and editorial.

3:2 aspect ratio
```

#### Modern Digital Clean
```
The image is captured on a Phase One medium format digital camera with a
110mm lens. Clean, even lighting with soft shadows. Colors are true-to-life
with subtle color grading. Skin appears natural with minimal retouching.
The look is contemporary high-fashion commercial.

3:2 aspect ratio
```

#### Warm Film (Kodak Portra)
```
The image is shot on Kodak Portra 400 film with a 50mm lens. Warm, golden
tones with soft contrast. Natural window light creates gentle shadows.
Colors are muted but rich. Skin tones are warm and flattering. The grain
is fine and organic.

3:2 aspect ratio
```

#### Harsh Flash Editorial
```
The image is captured with direct on-camera flash creating harsh shadows
and flat lighting. High contrast with blown highlights. Colors are punchy
and slightly desaturated. The aesthetic is raw, paparazzi-style editorial.

3:2 aspect ratio
```

#### Soft Diffused Glamour
```
The image is shot with large softbox lighting creating wrap-around
illumination. Skin appears luminous and smooth. Colors are soft and
pastel-toned. Minimal shadows with a dreamy, ethereal quality. Shot on
digital with subtle grain overlay.

3:2 aspect ratio
```

#### Moody Low-Key
```
The image features dramatic chiaroscuro lighting with deep shadows
dominating the frame. A single spotlight illuminates key features while
the background falls to pure black. High contrast, minimal fill light.
The mood is mysterious and theatrical.

3:2 aspect ratio
```

---

## 2. Changing Camera Angles

The default pipeline uses 6 fixed camera angles. You can customize these for different photoshoot styles.

### Current 6-Shot Pattern (Default Tim Workflow)

```
┌─────────────────┬─────────────────┬─────────────────┐
│  Frame 1        │  Frame 2        │  Frame 3        │
│  Beauty Portrait│  High-Angle 3/4 │  Low-Angle Full │
├─────────────────┼─────────────────┼─────────────────┤
│  Frame 4        │  Frame 5        │  Frame 6        │
│  Side-On Profile│  Intimate Close │  Extreme Detail │
└─────────────────┴─────────────────┴─────────────────┘
```

#### Full Descriptions of Current 6 Camera Angles

**Frame 1: High-Fashion Beauty Portrait (Close, Editorial, Intimate)**
```
Camera positioned very close to the subject's face, slightly above or slightly
below eye level, using an elegant offset angle that enhances bone structure and
highlights key wardrobe elements near the neckline. Shallow depth of field,
flawless texture rendering, and a sculptural fashion-forward composition.
```

**Frame 2: High-Angle Three-Quarter Frame**
```
Camera positioned overhead but off-center, capturing the subject from a diagonal
downward angle. This frame should create strong shape abstraction and reveal
wardrobe details from above.
```

**Frame 3: Low-Angle Oblique Full-Body Frame**
```
Camera positioned low to the ground and angled obliquely toward the subject.
This elongates the silhouette, emphasizes footwear, and creates a dramatic
perspective distinct from Frames 1 and 2.
```

**Frame 4: Side-On Compression Frame (Long Lens)**
```
Camera placed far to one side of the subject, using a tighter focal length to
compress space. The subject appears in clean profile or near-profile, showcasing
garment structure in a flattened, editorial manner.
```

**Frame 5: Intimate Close Portrait From an Unexpected Height**
```
Camera positioned very close to the subject's face (or upper torso) but slightly
above or below eye level. The angle should feel fashion-editorial, not
conventional — offset, elegant, and expressive.
```

**Frame 6: Extreme Detail Frame From a Non-Intuitive Angle**
```
Camera positioned extremely close to a wardrobe detail, accessory, or texture,
but from an unusual spatial direction (e.g., from below, from behind, from the
side of a neckline). This must be a striking, abstract, editorial detail frame.
```

---

### Alternative Shot Patterns

Below are complete 6-angle patterns for different types of photoshoots. Copy and paste these into your custom workflow template.

---

#### Luxury Accessories Campaign

Best for: Handbags, jewelry, watches, eyewear

```
1. Hero Product Shot with Model Context
Camera positioned at eye level, medium shot showing the model holding or wearing
the accessory prominently. The product is the clear focal point while the model
provides aspirational context. Clean composition with the accessory at the
intersection of thirds.

2. Intimate Product-Skin Interaction
Camera very close, capturing the tactile relationship between product and skin.
For jewelry: clasp against collarbone. For bags: hand gripping handle. Shallow
depth of field isolates the product. Texture of both product and skin visible.

3. Graphic Flat-Lay Detail
Camera positioned directly overhead (bird's eye). Product arranged with
complementary items in an editorial flat-lay composition. Strong graphic shapes
and negative space. Studio-perfect lighting revealing material quality.

4. In-Motion Lifestyle
Camera at waist height capturing the product in natural movement. Model walking,
turning, or gesturing. Slight motion blur on model, product remains sharp.
Conveys how the product lives in real moments.

5. Dramatic Low-Angle Hero
Camera very low, shooting upward. Product appears powerful and desirable.
Emphasizes sculptural qualities and craftsmanship. Strong rim lighting defines
edges and premium materials.

6. Macro Craftsmanship Detail
Extreme close-up of product detail: stitching, clasp mechanism, texture, logo
engraving. Camera angle reveals three-dimensionality. This frame proves quality
and justifies luxury positioning.
```

---

#### Streetwear / Urban Editorial

Best for: Sneakers, hoodies, graphic tees, urban lifestyle brands

```
1. Environmental Full-Body Power Shot
Camera at hip height, wide angle capturing full outfit in urban context. Concrete,
graffiti, or architectural elements visible. Model in confident stance. The
environment is as important as the clothing.

2. Low-Angle Sneaker Hero
Camera almost at ground level, shooting upward. Sneakers dominate the frame with
the outfit towering above. Dramatic perspective elongates the figure. Urban
ground texture visible.

3. Action Walking Shot
Camera tracking the model mid-stride. Slight motion energy in the frame. Clothing
moves naturally. Captures the outfit as it's meant to be worn — in motion, on
the street.

4. Over-Shoulder Environmental POV
Camera behind and slightly above the model's shoulder, revealing both the back
of the outfit and the urban landscape ahead. Creates narrative and journey.
Back graphics or details visible.

5. Detail Stack — Layering Focus
Camera medium-close on the torso, emphasizing layering: jacket over hoodie over
tee. How pieces work together. Textures and logos visible. Diagonal composition
creates energy.

6. Crew/Culture Moment
Camera captures a candid-feeling interaction — checking phone, adjusting cap,
leaning against wall. Authentic gesture that grounds the fashion in real
culture. Less posed, more lived-in.
```

---

#### Beauty / Makeup Campaign

Best for: Cosmetics, skincare, beauty brands

```
1. Classic Beauty Portrait — The Hero Face
Camera at eye level, perfectly centered, close crop on face. Flawless skin
visible. Makeup is the star. Eyes engage directly with camera. Even, beauty
lighting with minimal shadows. This is the campaign hero shot.

2. Three-Quarter Dramatic Lighting
Camera slightly to the side, Rembrandt or loop lighting creates dimension.
Cheekbone highlighted, one side of face in soft shadow. Shows how makeup
performs in dimensional light. Sophisticated and editorial.

3. Pure Profile Silhouette
Camera perpendicular to face, clean profile view. Emphasizes lip line, nose,
brow arch. Can be dramatically lit from behind for silhouette or softly lit
to show product on profile. Timeless beauty angle.

4. Eyes Macro — The Window Shot
Extreme close-up framing just the eyes and brows. Captures mascara, eyeshadow,
liner in exquisite detail. Catch lights in eyes. Skin texture visible but
flattering. May include partial nose bridge.

5. Lips & Chin Detail
Close crop on lower face: lips, chin, partial cheeks. Lipstick or gloss is
the hero. Slight parting of lips. Skin appears luminous. Angle slightly
below to emphasize lip shape.

6. Texture & Glow — Skin Close-Up
Macro shot of cheek or forehead showing skin texture and product glow.
Highlighter, foundation, or skincare visible on skin. Proves product
performance. Almost abstract in its closeness.
```

---

#### Movement / Dance Editorial

Best for: Activewear, performance wear, dynamic fashion

```
1. Static Tension — The Calm Before
Camera at full-body distance, model in held pose suggesting imminent movement.
Muscles engaged, weight loaded. The outfit at rest but charged with potential.
Clean studio or contextual background.

2. Peak Action Freeze
Camera captures the apex of movement — highest jump, fullest extension,
sharpest turn. Frozen in perfect clarity. Outfit performs under stress.
Dynamic lines and shapes. High shutter speed aesthetic.

3. Motion Blur Expressionism
Camera uses slower exposure, model in movement. Intentional blur conveys
speed and energy. Some elements sharp (face or key garment), others ghosted.
Artistic interpretation of motion.

4. Floor-Level Dynamic Angle
Camera on the ground shooting upward as model moves overhead or nearby.
Unusual perspective creates drama. Emphasizes verticality and athleticism.
Footwear and lower garments prominent.

5. Overhead Bird's Eye Choreography
Camera directly above, shooting down. Model on floor in dynamic pose or
mid-movement. Creates graphic shapes with limbs and fabric. Unexpected
angle reveals garment construction from above.

6. Silhouette Backlit Drama
Camera facing into strong backlight, model between camera and light source.
Figure becomes silhouette with rim lighting on edges. Movement implied in
pose. Fabric translucency possible. Theatrical and iconic.
```

---

#### Intimate / Lingerie Editorial

Best for: Intimates, loungewear, body-positive campaigns

```
1. Soft Portrait — Face & Décolletage
Camera close, capturing face and upper chest. Soft, diffused lighting wraps
the form. Expression is confident and comfortable. Garment neckline or strap
detail visible. Intimate but not overtly sexual.

2. Full-Figure Confidence
Camera at medium distance, full body visible. Model in natural, comfortable
pose — sitting, reclining, standing relaxed. Celebrates the body in the
garment. Soft shadows define form without harsh contrast.

3. Back Architecture
Camera behind the model, capturing the back of garment — strap details,
closures, how fabric drapes from shoulders. Model looking over shoulder
optional. Reveals construction and design from unexpected angle.

4. Fabric & Skin Texture
Camera very close, capturing where fabric meets skin. Lace edge, elastic
line, satin sheen against body. Tactile and sensual without explicit.
Shallow focus, warm tones.

5. Natural Movement — Caught Moment
Camera captures a gesture: adjusting strap, running hand through hair,
mid-laugh. Feels candid rather than posed. Garment moves with body
naturally. Lifestyle authenticity.

6. Detail & Craftsmanship
Macro focus on construction detail: embroidery, seaming, hardware,
pattern. Proves quality and design intention. Almost product-shot in
precision but on body for context.
```

---

#### E-Commerce / Catalog Standard

Best for: Multi-SKU product shoots, consistent brand imagery

```
1. Full-Body Front — The Primary Shot
Camera at chest height, straight-on, full body visible with space above
and below. Model in neutral stance, arms slightly away from body. Clean
white or grey background. The essential product shot — clear, accurate,
shoppable.

2. Full-Body Back
Camera behind model, same framing as front. Reveals back of garment —
closures, back design, how it drapes. Model's head may turn slightly.
Matches front shot for easy comparison.

3. Full-Body Three-Quarter
Camera 45 degrees to model's front, full body. Shows dimensional fit —
how garment curves around body. Side seams, pocket positions visible.
More dynamic than front/back while remaining clear.

4. Detail Shot — Key Feature
Camera close on the most important design element: collar, cuff, pocket,
logo placement, unique construction. The "zoom" shot for online product
pages. Sharp focus, accurate color.

5. Fabric Texture Swatch
Extreme close-up showing material quality, weave, print detail, or
finish. Almost abstract. Proves fabric hand and quality. Essential
for customer confidence in online shopping.

6. Lifestyle Context
Camera wider, showing garment in suggested use environment. Office,
casual, evening context appropriate to product. Helps customer imagine
wearing. Slightly more styled than pure e-comm shots.
```

---

### How to Edit Camera Angles

Edit the `CONTACT_SHEET_PROMPT` in `tim-workflow-templates.md`. Replace the "Required 6-Frame Shot List" section:

```markdown
Required 6-Frame Shot List (All Resting Frames)

1. [YOUR SHOT NAME]
[Full description of camera position, angle, lens feel, purpose,
and what this frame should reveal about the subject/garment]

2. [YOUR SHOT NAME]
[Full description...]

3. [YOUR SHOT NAME]
[Full description...]

4. [YOUR SHOT NAME]
[Full description...]

5. [YOUR SHOT NAME]
[Full description...]

6. [YOUR SHOT NAME]
[Full description...]
```

**Important:** Keep the descriptions detailed and specific. The AI uses these descriptions to understand exactly what camera position and composition you want.

---

## 3. Modifying Video Camera Movements

Each of the 6 frames gets a video with a specific camera movement. You can customize these.

### Current Video Movements

| Frame | Current Movement | Description |
|-------|-----------------|-------------|
| 1 (Beauty) | Push In | Camera moves toward face |
| 2 (High-Angle) | Orbital | Camera arcs around from above |
| 3 (Low-Angle) | Rise Up | Camera rises from low position |
| 4 (Profile) | Lateral Track | Camera slides left/right |
| 5 (Intimate) | Breath Movement | Subtle, nearly static |
| 6 (Detail) | Macro Drift | Slow drift across detail |

### Alternative Movement Sets

#### High Energy
```
Frame 1: "Camera rapidly pushes in with slight shake, creating urgency and intensity."
Frame 2: "Fast orbital sweep with motion blur, dynamic and energetic."
Frame 3: "Quick crane up with slight dutch angle, powerful and assertive."
Frame 4: "Fast lateral dolly with subject tracking, kinetic movement."
Frame 5: "Handheld micro-movements, documentary feel, raw and immediate."
Frame 6: "Quick zoom into detail with rack focus, punchy and bold."
```

#### Ultra Smooth Luxury
```
Frame 1: "Imperceptibly slow push in, floating quality, silk-smooth movement."
Frame 2: "Graceful orbital glide, weightless and elegant, like watching from a cloud."
Frame 3: "Gentle crane rise with no perceptible start or stop, liquid motion."
Frame 4: "Butter-smooth lateral slide, perfectly even speed, meditative."
Frame 5: "Near-static with breath-like micro-sway, intimate and precious."
Frame 6: "Glacial drift across texture, ASMR-quality precision."
```

#### Static/Tableau
```
Frame 1: "Camera holds perfectly still. Subject's eyes blink slowly."
Frame 2: "Locked-off shot. Fabric moves subtly in gentle breeze."
Frame 3: "Tripod-stable. Only the model's hair catches light movement."
Frame 4: "Static frame. Subject turns head slowly toward camera."
Frame 5: "No camera movement. Subject's breath visible in expression."
Frame 6: "Macro stillness. Light plays across texture."
```

### Editing Video Prompts

In `tim-workflow-templates.md`, find `PHASE 5: VIDEO GENERATION` and modify each frame's prompt:

```markdown
**Frame 1 (Beauty Portrait) - [Movement Name]:**
[Your movement description]
```

---

## 4. Adjusting Video Transitions

The stitch script supports multiple transition types and easing curves.

### Available Transitions

| Transition | Effect |
|------------|--------|
| `fade` | Cross-dissolve (default, best for fashion) |
| `fadeblack` | Fade through black |
| `fadewhite` | Fade through white |
| `wipeleft` | Wipe from right to left |
| `wiperight` | Wipe from left to right |
| `wipeup` | Wipe from bottom to top |
| `wipedown` | Wipe from top to bottom |
| `slideleft` | Slide next clip in from right |
| `slideright` | Slide next clip in from left |
| `circlecrop` | Circle iris in |
| `circleopen` | Circle opens to reveal |
| `circleclose` | Circle closes to reveal |
| `dissolve` | Dither/noise dissolve |

### Available Easing Curves

| Easing | Feel | Best For |
|--------|------|----------|
| `linear` | Constant speed | Technical, utilitarian |
| `smooth` | Classic smoothstep | General purpose |
| `cinematic` | Professional feel | Film-style edits |
| `luxurious` | Ultra-gentle end | High-end fashion |
| `cubic-in` | Slow start, fast end | Building energy |
| `cubic-out` | Fast start, slow end | Gentle landing |
| `cubic-in-out` | Smooth both ends | Elegant transitions |
| `sinusoidal-in-out` | Wave-like | Dreamy, organic |
| `quartic-*` | More pronounced | Dramatic |
| `quintic-*` | Very dramatic | Bold statements |

### Transition Duration

- `0.5s` - Quick, energetic
- `1.0s` - Standard
- `1.2s` - Smooth, luxurious (default)
- `2.0s` - Very slow, dreamy
- `3.0s+` - Extreme slow dissolve

### Example Commands

```bash
# High-end luxury (default)
--transition fade --easing luxurious --transition-duration 1.2

# Fast, energetic edit
--transition fade --easing cubic-out --transition-duration 0.4

# Dramatic black transitions
--transition fadeblack --easing cinematic --transition-duration 1.5

# Retro wipe
--transition wipeleft --easing quadratic-in-out --transition-duration 0.8

# Dreamy dissolve
--transition dissolve --easing sinusoidal-in-out --transition-duration 2.0
```

---

## 5. Changing Image Settings

### Aspect Ratios

| Ratio | Use Case |
|-------|----------|
| `3:2` | Classic photography (default) |
| `4:3` | Traditional photo frame |
| `16:9` | Widescreen/cinematic |
| `21:9` | Ultra-wide cinematic |
| `1:1` | Instagram square |
| `4:5` | Instagram portrait |
| `9:16` | TikTok/Reels/Stories |

### Resolutions

| Resolution | Pixels (approx) | Use Case |
|------------|-----------------|----------|
| `1K` | ~1024px | Preview, drafts, isolated frames |
| `2K` | ~2048px | Hero shots, contact sheets |
| `4K` | ~4096px | Final delivery, print |

### Video Duration

| Duration | Use Case |
|----------|----------|
| `5` | Standard clips (default) |
| `10` | Longer movements, more development |

---

## 6. Creating Alternative Workflow Presets

To create a completely new workflow preset, create a new file:

**Location:** `agent/.claude/skills/editorial-photography/workflows/[your-workflow]-templates.md`

### Template Structure

```markdown
# [Your Workflow Name] - Exact Prompt Templates

## PHASE 1: REFERENCE ANALYSIS

### Required Extractions
```
SUBJECT:      [What to extract]
WARDROBE:     [What to extract]
ACCESSORIES:  [What to extract]
POSE:         [What to extract]
BACKGROUND:   [What to extract]
```

## PHASE 2: HERO IMAGE GENERATION

### HERO_PROMPT Template
```
[Your hero prompt with {PLACEHOLDERS}]

[Your style block]

[Your aspect ratio]
```

## PHASE 3: CONTACT SHEET GENERATION

### CONTACT_SHEET_PROMPT
```
[Your contact sheet prompt with your 6 camera angles]
```

## PHASE 4: FRAME ISOLATION
[Same as default - row/column extraction]

## PHASE 5: VIDEO GENERATION
[Your 6 video movement prompts]

## PHASE 6: VIDEO STITCHING
[Your transition/easing preferences]
```

---

## 7. Examples: Complete Alternative Workflows

### Example A: Minimalist Black & White

**Style Block:**
```
Shot on Ilford Delta 3200 film, pushed two stops. Harsh directional
lighting creates deep blacks and bright whites. Heavy grain texture.
Minimal midtones. Dramatic and moody.
```

**6 Camera Angles:**
1. Dramatic silhouette profile
2. Overhead geometric shadow play
3. Low angle with strong rim light
4. Close portrait with split lighting
5. Full body with long shadow
6. Abstract limb/fabric detail

**Video Movements:** All slow, meditative, static or near-static

**Transition:** `fadeblack` with `luxurious` easing, 2.0s duration

---

### Example B: Vibrant Streetwear

**Style Block:**
```
Shot on digital with vibrant color grading. Punchy saturation with
teal and orange color palette. Sharp focus throughout. Urban grit
with clean execution. Mixed natural and neon lighting.
```

**6 Camera Angles:**
1. Wide environmental with urban backdrop
2. Low angle power pose
3. Walking/action shot
4. Sneaker/footwear detail
5. Over-shoulder POV
6. Graphic flat-lay accessories

**Video Movements:** Fast, energetic, with camera shake

**Transition:** `fade` with `cubic-out` easing, 0.5s duration

---

### Example C: Romantic Soft Focus

**Style Block:**
```
Shot through vintage glass with slight diffusion. Soft, dreamy
focus with gentle lens flare. Pastel color palette with warm
highlights. Natural window light with sheer curtains. Ethereal
and romantic.
```

**6 Camera Angles:**
1. Soft portrait with backlighting
2. Flowing fabric detail
3. Three-quarter through sheer fabric
4. Close-up with bokeh flowers
5. Full body in natural light
6. Hand/jewelry detail

**Video Movements:** All gentle, floating, with slow motion feel

**Transition:** `fadewhite` with `sinusoidal-in-out` easing, 1.8s duration

---

## Quick Start: Making Your First Customization

1. **Copy the template file:**
   ```bash
   cp agent/.claude/skills/editorial-photography/workflows/tim-workflow-templates.md \
      agent/.claude/skills/editorial-photography/workflows/my-workflow-templates.md
   ```

2. **Edit the style block** (search for "fuji velvia")

3. **Modify camera angles** (search for "Required 6-Frame Shot List")

4. **Update video movements** (search for "PHASE 5: VIDEO GENERATION")

5. **Test with a single image first** before running the full pipeline

---

## File Reference

| File | Purpose |
|------|---------|
| `agent/.claude/skills/editorial-photography/workflows/tim-workflow-templates.md` | Main prompt templates |
| `agent/.claude/skills/editorial-photography/SKILL.md` | Skill description and rules |
| `agent/.claude/skills/fashion-shoot-pipeline/SKILL.md` | Pipeline script documentation |
| `server/lib/orchestrator-prompt.ts` | System prompt (references templates) |
