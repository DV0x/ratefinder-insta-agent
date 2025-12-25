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

### Current 6-Shot Pattern

```
┌─────────────────┬─────────────────┬─────────────────┐
│  Frame 1        │  Frame 2        │  Frame 3        │
│  Beauty Portrait│  High-Angle 3/4 │  Low-Angle Full │
├─────────────────┼─────────────────┼─────────────────┤
│  Frame 4        │  Frame 5        │  Frame 6        │
│  Side-On Profile│  Intimate Close │  Extreme Detail │
└─────────────────┴─────────────────┴─────────────────┘
```

### Alternative Shot Patterns

#### Product-Focused (Accessories/Shoes)
```
1. Full outfit with product highlighted
2. Product close-up on model
3. Product detail macro shot
4. Product in action/movement
5. Alternative angle of product
6. Lifestyle context shot
```

#### Movement/Dance Editorial
```
1. Static pose establishing shot
2. Mid-motion blur capture
3. Peak action freeze
4. Floor-level dynamic angle
5. Overhead bird's eye
6. Silhouette backlit
```

#### Portrait-Heavy (Beauty Campaign)
```
1. Classic beauty headshot
2. Three-quarter face, dramatic lighting
3. Profile silhouette
4. Eyes detail close-up
5. Lips/makeup detail
6. Hair texture close-up
```

#### Streetwear/Urban
```
1. Full body urban context
2. Low angle power pose
3. Action walking shot
4. Detail on sneakers/accessories
5. Over-shoulder environmental
6. Candid interaction
```

### How to Edit Camera Angles

Edit the `CONTACT_SHEET_PROMPT` in `tim-workflow-templates.md`:

```markdown
Required 6-Frame Shot List (All Resting Frames)

1. [YOUR FIRST SHOT DESCRIPTION]
Camera positioned [position details], using [angle/lens details].
This frame should [purpose and what it reveals].

2. [YOUR SECOND SHOT DESCRIPTION]
...
```

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
