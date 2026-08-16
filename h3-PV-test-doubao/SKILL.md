---
name: h3-style-clone
description: "Extract visual style DNA from reference images and generate complete MiniMax H3 video prompts (I2VA, FL2VA, Ref2VA) for high-density PV-style content. Replicates rendering, color, graphic vocabulary, and pacing while generating original subjects and narratives. Default output 18-25 shots per 15s with timeline-synced audio arc."
sources: [chat]
aliases: [style-clone, h3-pvg, pvg]
---

# H3 Style Clone — PV Prompt Generator

## Core Principle

Reference images provide **visual style only** — color system, rendering medium, graphic vocabulary, pacing language, and visual prohibitions. All subjects, characters, actions, and narrative content come from the user's direction or from suggestions based on the identified subject in the reference.

**Reference → style DNA extraction**  
**User direction → every character, action, scene in the output**

---

## Workflow

```
1. Multi-Image Intake   → detect role (style / first frame / last frame / character)
2. Style DNA Extraction → color, rendering, graphic design, pacing, prohibitions
3. Content Direction    → user provides OR model suggests based on identified subject
4. PV Structure         → map to flexible PV framework (Hook → Build → Climax → Freeze)
5. H3 Prompt Assembly   → I2VA / FL2VA / Ref2VA with 2000-3000 word detailed_description
6. Output Validation    → check style consistency, shot density, audio arc
```

---

## Step 1 — Multi-Image Intake

Detect each image's role before extraction:

| Role | Trigger | Mode |
|---|---|---|
| **Style reference** | Default; no keyframe signal | Ref2VA |
| **First frame** | "start from this" / "开头用这张" | I2VA |
| **Last frame** | "end on this" / "结尾用这张" | L2VA |
| **First + Last** | Two images as open + close | FL2VA |
| **Character reference** | "this character" / clearly shows subject | Ref2VA multi-subject |
| **Environment reference** | "this setting" / "这个场景" | Ref2VA multi-subject |

**Multi-image configs**:
- 2+ style references → merge Style DNA
- 2+ characters → all appear in the same PV, mix-cut montage style
- Style + multiple characters → Ref2VA with separate `<Subject N>` per character

When role is ambiguous, default to Style reference.

---

## Step 2 — Style DNA Extraction

Extract only visual language across five dimensions:

### A. Color System
- Palette (name every color precisely: "pure black, fluorescent pink, pure white")
- Structure (monochrome+accent | duotone | limited 3-4 colors | full-color)
- Accent role (structural | highlighting | decorative | dominant)
- Background treatment (solid | paper grain | flat texture | absent)
- Color prohibitions (excluded hues)

### B. Rendering Language
- Medium (2D cel | flat vector | pixel art | watercolor | photorealistic | 3D CG | collage)
- Outline (thick black | thin | variable-weight | colored | none)
- Fill (flat color | cel shading | gradient | stipple | realistic lighting)
- Texture (halftone dots | paper grain | scan noise | digital noise | clean)
- Prohibitions (no 3D depth | no volume light | no realistic skin | no lens blur | etc.)

### C. Graphic Design System
- Typography style (brushed | stencil | pixel | handwritten | bold sans) — extract form, NOT content
- Symbol vocabulary (hearts | stars | skulls | crowns | smileys | warnings | barcodes) — generic categories only
- Layout logic (centered | editorial | scattered | grid)
- HUD/UI layer (game UI | meter bars | counter labels | menu overlays | none)

### D. Pacing & Cinematic Language
- Implied pacing (slow | medium | fast/kinetic | beat-locked)
- Cut vocabulary (hard cuts | glitch breaks | paper-tear wipes | shape wipes | fades)
- Motion graphics (speed lines | accent trails | particle bursts | symbol orbits | compression pulses)

### E. Subject Treatment
- Character rendering style within this visual system
- Subject-background relationship (integrated | silhouette | layered collage)
- Proportion style (realistic | stylized | chibi | abstract)

---

## Step 3 — Content Direction

### If user provides direction → proceed to Step 4

### If no direction provided → Fallback Protocol

**NI-1**: Show 3-line style summary in plain language  
Example: *"平面朋克插画风:纯黑白加荧光粉,厚描线,完全没有立体感,节奏感很强,适合做高速剪辑的角色 PV。"*

**NI-2**: Ask one question  
> "你想自己描述要拍什么,还是我根据这个风格给你几个方向?"

**NI-3A**: User provides own direction → proceed to Step 4

**NI-3B**: Model suggests directions
1. Identify subject from reference image (character | animal | product | scene | abstract)
2. Generate 2-3 PV direction options varying **only in visual flow**, all using the same subject:
   - Opening strategy (eye close-up → action | run entry → freeze | glitch burst → reveal)
   - Build rhythm (fragment montage → full body | slow single-take → explosion | beat-sync cuts)
   - Climax approach (panel split → compression | symbol flood → poster | UI takeover → freeze)

Example:
> 图里的主角是一只法斗犬,以下是 3 个 PV 方向:  
> 1. 眼睛特写开场 → 碎片蒙太奇(爪子/耳朵/项圈快切) → 全身动作 → 符号爆炸 → 海报定格  
> 2. 奔跑进入 → UI 图层叠加 → 漫画分格 → 压缩到核心 → 粉色爆裂  
> 3. 黑屏→故障闪现 → 贴纸撕裂转场 → 高速滑行 → 正脸坏笑定格

User selects or modifies → proceed to Step 4

---

## Step 4 — PV Framework (Flexible)

All outputs follow PV macro structure but adapt segment timing and density to the user's direction and Style DNA pacing.

### PV Skeleton (15s default)

| Phase | Function | Visual Strategy |
|---|---|---|
| **Hook** | 0.00–1.00s | Black hold → burst + text sting OR glitch reveal OR extreme close-up. **Do NOT show the reference image's full pose or composition here** — the opening establishes style and energy, not the final poster layout. Save the reference pose for the Freeze. |
| **Identity/Build** | 1.00–6.00s | Fragment montage (detail cuts) + subject action + graphic layers |
| **Climax** | 6.00–13.00s | Panel splits, compression, symbol flood, UI takeover, beat pulses |
| **Freeze** | 13.00–15.00s | Final poster frame **matching the reference image's exact pose and composition**, with title/labels snapping into place |

**Shot density baseline**: 18-25 shots for 15s (adjust based on Style DNA pacing)

**Segment boundaries are flexible** — if user's direction or Style DNA implies slower pacing, stretch segments; if kinetic, compress and add more cuts.

**Visual Techniques** (apply where Style DNA permits):
- Monochrome flood → accent color infection
- Graphic text sting → labels/UI explode as flat elements
- Glitch corruption → noise bands, pixel scatter
- Speed lines → manga-style 2D motion lines
- Comic panel grid → frame splits 2-4 panels
- Sticker pop → instant scale-pop
- Beat pulse → scale/flash on music beats
- UI overlay → game HUD elements
- Tear/reveal wipe → physical transition
- Silhouette stack → offset accent layers
- Halftone field → screentone shadows/transitions
- Compression to core → all elements collapse inward
- Poster freeze → motion stops, text snaps in
- Extreme close-up → eye/detail fills frame
- Fragment montage → rapid detail cuts (hand, shoe, texture, logo)
- Accent trail → movement leaves color residue
- Wave burst → concentric rings from impact
- Symbol orbit → icons swarm around subject
- Hard graphic wipe → solid shape sweeps frame

---

## Step 5 — H3 Prompt Assembly

### Mode Selection

| Input | Mode |
|---|---|
| 1 image, first-frame signal | I2VA |
| 1 image, last-frame signal | L2VA |
| 2 images, first+last signal | FL2VA |
| Style / character / environment reference | Ref2VA |

### Style Statement

Write 1-2 sentences declaring rendering + prohibitions. Place before `[Shot 1]` in Ref2VA `detailed_description`, or inside `[Shot 1]` for I2VA/FL2VA/L2VA.

**Format**: `[Medium], [color system]; [outline and fill]; [texture]; [prohibitions].`

Example:
> *Flat 2D cel-animation and editorial graphic design; strict black, white, and fluorescent pink palette with no other colors; thick black outlines, pure flat color fills, halftone dot shadows; no 3D geometry, no realistic depth, no soft lighting, no cinematic lens blur, no standard fades.*

### I2VA Format

```
For the target video, at 0.00 seconds into the target video, <Picture 1> (from [Shot 1]) is fully referenced.

integrated_multimodal_description: [Shot 1] [STYLE STATEMENT]. The video opens with <Picture 1> as its first frame, establishing [SUBJECT/ENVIRONMENT AS VISIBLE]. [SEGMENT 1 ACTION].
[Shot 2] At 00:XX.XXX, the shot cuts to [NEXT COMPOSITION].
...

overall_soundscape: [Timeline-synced sound arc grouped by phase. Hook (0-1s): [key sounds]. Build (1-6s): [layered sound events with phase-relative timing]. Climax (6-13s): [peak density sounds]. Freeze (13-15s): [resolution sounds]. Target 800-1000 characters. Ambient + physical + non-verbal only.]

non_diegetic_music: [Complete musical arc: genre, BPM, core instruments in one sentence. Then phase transitions: Hook → Build (what drops at 1s, what layers in) → Climax (what peaks at 6s, breakdown/slam moments) → Freeze (what drops at 13s, fadeout). Target 800-1000 characters. N/A if none.]
```

### FL2VA Format

```
How the reference pictures align with the target video — Picture 1 (from Shot 1) aligns with the 0.00-second mark; Picture 2 (from Shot [N]) aligns with the [S.SS]-second mark.

integrated_multimodal_description: [Shot 1] [STYLE STATEMENT]. The video opens in the state of Picture 1: [DESCRIBE VISIBLE STATE]. [PATH TO PICTURE 2]. The final shot settles into Picture 2's composition.

overall_soundscape: [same as I2VA]
non_diegetic_music: [same as I2VA]
```

### Ref2VA Format — Single Style

```
subject_definitions:
<Subject 1> is the visual style in <Picture 1>: [MEDIUM], [COLOR], [GRAPHIC VOCAB], [PROHIBITIONS].
<Subject 2> is [USER'S SUBJECT]: [PHYSICAL DESCRIPTION IN STYLE TERMS].

summary:
[reference generation] The target video shows [CONTENT]. <Picture 1> provides visual style. <Subject 2> is new content built within that system.

retention_analysis:
<Subject 1> (all shots): fully_preserved — [STYLE ELEMENTS] consistent throughout.
<Subject 2> (appears in [Shot X, Y...]): fully_preserved — [DEFINING FEATURES] consistent.

detailed_description:
[STYLE STATEMENT].
[Shot 1] [CONTENT + STYLE + TECHNIQUES].
[Shot 2] At 00:XX.XXX, [NEXT].
...

overall_soundscape: [same structure]
non_diegetic_music: [same structure]
```

### Ref2VA Format — Multiple Characters

When multiple images show different characters, all characters appear in the same PV as mix-cut montage:

```
subject_definitions:
<Subject 1> is the visual style in <Picture 1>: [STYLE].
<Subject 2> is the [CHARACTER 1] in <Picture 2>: [APPEARANCE].
<Subject 3> is the [CHARACTER 2] in <Picture 3>: [APPEARANCE].

summary:
[reference generation] The target video shows [ALL CHARACTERS] in a mix-cut PV montage. <Picture 1> provides rendering system. <Subject 2> and <Subject 3> are placed within that system and appear in alternating/simultaneous shots.

retention_analysis:
<Subject 1> (all shots): fully_preserved.
<Subject 2> (appears in [Shot X, Y...]): fully_preserved.
<Subject 3> (appears in [Shot Z, W...]): fully_preserved.

detailed_description:
[STYLE STATEMENT].
[Shot 1] [CHARACTER 1 APPEARS — DESCRIBE FEATURES].
[Shot 2] At 00:XX.XXX, [CHARACTER 2 ENTERS — DESCRIBE FEATURES].
[Shot 3] At 00:XX.XXX, [BOTH CHARACTERS OR ALTERNATING CUTS].
...
```

---

## Step 6 — H3 Formatting Rules

**Shots**:
- `[Shot 1]` no timestamp
- `[Shot N] At MM:SS.SSS` for all subsequent, strictly increasing

**Shot counts**:
- 10s → 12-18 shots
- 15s → 18-25 shots  
- 20s → 25-35 shots

**Camera motion** (write as prose):
- `The camera pushes in with small amplitude at slow speed toward...`
- Types: Zoom In/Out | Push In/Pull Out | Pan L/R | Truck L/R | Tilt Up/Down | Pedestal Up/Down | Arc | Tracking | Static | Shake | POV | Roll

**Dialogue**: `(S1) says: <d>[English] Text.</d>`

**On-screen text**: wrap in English double-quotes, original language

**overall_soundscape**: Timeline-synced arc — Open (sparse signature sounds) → Build (layering density) → Peak (max simultaneous impacts) → Resolve (silence/sustained tone). **Write in phase blocks, NOT shot-by-shot timestamps**. Group sounds by framework phase (Hook 0-1s / Build 1-6s / Climax 6-13s / Freeze 13-15s). Within each phase, list key sound events with their phase-relative timing. Target 800-1000 characters total. Example structure: "Hook (0-1s): bass impact at open + glitch zap. Build (1-6s): layered percussion — chain clinks, boot stomps at 2s, leather creaks; sticker pops on each beat. Climax (6-13s): symbol swirl whoosh building, compression descending drone 9-10s, massive explosion boom at 10s with shrapnel pings. Freeze (13-15s): near-silence, sticker snap clicks 13-14s, final scan whoosh, neon hum fadeout."

**non_diegetic_music**: Complete arc with instrumentation, BPM, dynamic changes at segment boundaries. **Write as phase transitions, not detailed bar-by-bar**. State genre, BPM, core instruments in one sentence, then describe what changes at each phase boundary. Target 800-1000 characters total. Example structure: "Electro-punk, 150BPM. Distorted bass, synth leads, electronic drums, glitch samples. Hook: sparse bass stab + silence. Build (drops at 1s): full beat with kick/snare, bouncy synth riff enters at 3s, hi-hats layer at 4s. Climax (6s): intensity peak — saw-wave lead screams an octave up, double-kick drums, glitch breakdown at 8s strips to percussion then slams back at 10s with power chord. Freeze (13s): all instruments drop, single sustained drone fades to silence by 15s." `N/A` if none.

---

## Step 7 — Output Rules

1. **Style ≠ Content**: Extract typographic **style** (brushed, pixel, stencil) NOT words. If reference shows "REBEL CAT" sticker, output might use "WILD SPARK" in the same brushed rendering — match form, not content.

2. **Multi-character freedom**: Multiple character images can all appear in the same PV as mix-cut montage.

3. **Style DNA precision**: Every prohibition from DNA appears in style statement and is upheld in all shots.

4. **Fragment montage = separate shots**: Detail cuts must be split — one shot per detail (hand, shoe, eye, etc.).

5. **H3 field names**: Exact spelling — `integrated_multimodal_description`, `overall_soundscape`, `non_diegetic_music`, `subject_definitions`, `summary`, `retention_analysis`, `detailed_description`.

6. **Total output length**: The complete Ref2VA output (all fields combined: `subject_definitions` + `summary` + `retention_analysis` + `detailed_description` + `overall_soundscape` + `non_diegetic_music`) must NOT exceed **10,000 characters** (English). This is a hard ceiling. Allocate characters strategically across fields:
   - `subject_definitions`: 500-700 characters
   - `summary`: 300-400 characters
   - `retention_analysis`: 400-600 characters
   - `detailed_description`: 4000-5000 characters (the main allocation)
   - `overall_soundscape`: 800-1000 characters
   - `non_diegetic_music`: 800-1000 characters
   
   **Within `detailed_description`, compress all shots to 50-200 characters each**:
   - **Key shots** (first character reveal, climax burst, poster freeze): 150-200 characters — composition, core action, primary graphic element, transition
   - **Fragment montage shots** (hand/shoe/accessory close-ups): 50-80 characters — element + one sticker pop, one sentence
   - **Transition/action shots** (movement, mid-sequence): 80-120 characters — motion path + graphic event only
   
   **Compression strategy**: Most shots should be ONE sentence. Only key narrative shots get TWO sentences. Eliminate: detailed timing breakdowns within a shot, exhaustive accessory lists, camera parameter prose ("pushes in with small amplitude at medium speed"), redundant subject feature restatements. State only: what is visible, what moves, what graphic pops, what transitions.
   
   **Example of compressed shot**: "At 00:03.200, close-up of blue-nailed hand drumming on silver chain, skull ring visible. Cat-skull sticker pops top-right." (129 characters) — NOT a paragraph detailing each finger, ring material, chain texture, lighting, camera motion, and sound cues.
   
   **Self-check**: After writing, count total output characters (all fields). If over 10,000, compress every non-key shot to one sentence. Do NOT compress audio arcs.

7. **Language**: English throughout. Original language only inside `<d>` and on-screen text quotes.

8. **No fades** unless Style DNA supports them.

---

## Internal Planning Card (Silent)

Compile before writing:

```
IMAGES: [N images] [roles]
STYLE DNA: [color] [rendering] [graphic] [pacing] [prohibitions]
MODE: [I2VA/FL2VA/L2VA/Ref2VA]
DURATION: [Xs]
SHOT COUNT: [N shots estimated]
STYLE STATEMENT: [1-2 sentences]
SUBJECTS: [<Subject N> list]
```
