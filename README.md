# JIZURA — Auto Lyric Video Builder (English edition)

> English translation of [852wa/JIZURA](https://github.com/852wa/JIZURA) by hakoniwa (MIT). The UI, part names and docs are translated; the engine still handles Japanese lyrics as well as English.
>
> The After Effects panel (`JIZURA_AE.jsx`) is **not** translated in this edition: its labels are still in Japanese.

A browser app that takes your lyrics, automatically builds cuts by combining techniques common in lyric videos (kinetic typography), and exports them to MP4. Layout, motion, decor, transitions and finish are stored as 707 small parts (plus 24 styles), and the combination changes every time, so a new seed always gives you a different structure. A panel (ScriptUI) for After Effects is included too.

**▶ Original (Japanese) version: <https://852wa.github.io/JIZURA/>** / AE panel: [download JIZURA_AE.jsx](https://852wa.github.io/JIZURA/JIZURA_AE.jsx) (right-click the link → "Save link as…")

- Nothing to install. Lyrics, songs and exports are all processed inside your browser and never sent to a server (the only thing loaded from outside is fonts from Google Fonts, and only the typefaces the current structure uses).
- The Auto button (key `R`) changes the style, mood, motion, colors and structure all at once, every time you press it.
- Aspect ratios 16:9 / 9:16 / 4:3 / 3:4 / 1:1 / 4:5 / 21:9, 720p to 4K, 24 / 30 / 60 fps.
- Load a song and it detects the beats and fits the cuts to them. You can also sync by hand by tapping.
- Export as MP4 (with the song), PNG sequence or transparent PNG. You can also export the structure as data (JSON) that you can edit in After Effects.

| File | Contents |
|---|---|
| `index.html` | The browser app itself (built, single file). This is what opens on GitHub Pages. You can also download it and open it locally |
| `JIZURA_AE.jsx` | The After Effects panel (built) |
| `src/` `app/` | Source of the browser app (engine, expression packs, UI) |
| `ae/` | Source of the AE panel |
| `docs/EXPRESSION_PACKS.md` | Guide for people adding expression parts (packs) |

### Requirements

- **MP4 export**: a browser that supports WebCodecs (Chrome / Edge recommended. Safari 16.4+ and Firefox 130+ also support WebCodecs, but whether they can export H.264 depends on the browser and OS). Without WebCodecs you can still use the preview and the PNG sequence export.
- Fonts are loaded from Google Fonts, only the typefaces in use and only when needed (offline, your computer's fonts are used instead).

---

## Terms of use (rights to your output and license)

- **The rights to the videos and images you make with this tool (the output) belong to you, the person who made them.** You can use them freely, commercially or not.
- The rights to the lyrics and songs you use belong to their respective owners.
- The tool itself is released under the MIT License. See [LICENSE](LICENSE) for details.
- The lyrics and songs you enter are processed only inside your browser and are never sent to a server.
- In the app, you can read the same information from the "Terms of use" button at the top right (in Simple mode, from the link under the Export button).

---

## Auto (Simple mode)

Switch screens with "Simple / Advanced" at the top right. The app opens in Simple mode.

- **Auto-create** (or `R` on the keyboard): each press re-rolls all of the following at random and plays from the start.
  - Style (never the same as the previous one)
  - Mood (Glitch / Mellow / Pop / Graphic / Editorial / Emotional / Everything). Each mood changes the motion strength, the amount of glitch, and which layouts and enter / exit techniques are used.
  - Typeface for headlines and Mincho frames
  - Colors (sometimes the accent color and offset colors A/B are randomized too)
  - Cut structure (seed)
- **◀ Previous take / Next take ▶**: move back and forth between the takes Auto has made. Go back to a take you like, then export it.
- **Change just one thing**: keep the current take and re-roll only one part of it.
  - Style / Colors (accent, offset colors A/B) / Mood (motion and techniques used) / Structure (combination of layouts and motion)
- Auto never changes the lyrics, song, timing or export settings. Lines you have locked in the line list stay as they are.

### What random picks can use

Two checkboxes under the Auto button (in Advanced mode, above the "Techniques" tab) decide which effects Auto, Shuffle and per-line re-rolls can pick.

- **Use Extras too** (default: off): when off, only the effects from the first public release (356 parts, 12 styles) are used. When on, the effects added later (351 parts, 12 styles, 6 typefaces) become candidates too.
- **Use Japanese-style effects** (default: on): Japanese-style graphics such as paper lanterns, postcards, shoji screens, folding fans, family crests, seigaiha waves and cherry-blossom petals, and the Japanese-style styles (Sakura, Ink & Vermilion). When off, they are never picked. This check is applied after the Extras check.
- Neither applies when you set a layout etc. by hand for a line, or choose a style yourself: those can always be used.
- In the "Techniques" tab and the style list, Extras carry a "+" badge and Japanese-style entries a "和" badge. Entries that random picks cannot choose with the current settings are shown faded.

## Random colors

Found under "Advanced" → "Style" tab → "Accent & offset colors".

- **Random palette**: picks a new combination of accent color and offset colors A/B (the two colors of the color offset).
  - A little under half the time it picks from combinations already tuned to work together (complementary colors and so on). Otherwise it builds a fresh one from the color wheel.
  - Brightness is corrected automatically to suit the background, keeping text dark or light enough to read (the accent keeps a contrast ratio of at least 3 against the background).
- You can also pick colors directly. Uncheck "Override with my colors" to go back to the style's own colors.

---

## Using the browser app

1. **Lyrics**: one line is one phrase. The syntax is:
   - `Hold the light/until morning` … `/` marks a cut break
   - `*glass*` … emphasis (bigger, high-impact effects are more likely to be picked)
   - `!` at the end of a line … adds a flash and a shake
   - `word|note` … small text shown in annotation layouts
   - `[01:23.45]lyric` … uses the LRC timestamp as is
2. **Song and timing**
   - Load a song and BPM and beats are detected automatically; cut breaks snap to the beats.
   - Press "Tap to sync" and the song plays. Press Space at the moment each line starts.
   - You can also edit the times in the line list directly.
3. **Choosing the structure**
   - "Shuffle" re-rolls everything.
   - The dice on each line re-rolls just that line.
   - The lock fixes that line's structure, and you can also set its layout directly.
4. **Style**: there are 24 sets of colors, typefaces and textures (including Sakura / Deep Sea / Sunset Gradient / Forest Notes / Vapor / Newsprint / Synth 80s / Kraft Paper / Candy / Acid / Ink & Vermilion / Golden Night). Within one video, the background color changes from cut to cut.
   - Typefaces are chosen from 18 Google Fonts families (including Reggae One / Rampart One / Potta One / Kiwi Maru / Klee One / Shippori Mincho B1). **Only the typefaces the current structure uses** are loaded, as needed, so more typefaces do not make startup or playback slower.
   - You can replace fonts by:
     - typing the name of a font installed on your computer
     - loading a .ttf / .otf file
5. **Effects and Techniques**
   - In the "Effects" tab, adjust motion strength, glitch, color offset, amount of decor, cut density, texture and frame stepping.
   - In the "Techniques" tab, you can turn each part in the 10 categories (Layout, Enter, Hold, Exit, Decor, Text treatment, Background, Camera, Screen effects, Transitions between cuts) on or off one by one (combined with the "Extras" and "Japanese-style" checkboxes above). Each category is collapsed, with "All on / All off / Invert" buttons and filtering by name.
6. **Export**
   - MP4 (H.264 in Chrome / Edge; the song can be included)
   - PNG sequence (ZIP)
   - Transparent PNG (ZIP, no background; for compositing in AE and similar)
   - Aspect ratio 16:9 / 9:16 / 4:3 / 3:4 / 1:1 / 4:5 / 21:9, resolution 720p to 4K, frame rate 24 / 30 / 60 fps (see "Exporting at 24 / 30 / 60 fps" below).
7. **Export for AE**: exports the current structure (timing, layouts, effects, colors) as JSON. Load it into the AE panel and you get comps with the same structure, ready to edit.

### Exporting at 24 / 30 / 60 fps

1. In the "Export" tab (in Simple mode, the "Export" box on the right), choose the aspect ratio, resolution and **fps**.
2. Press "Export MP4". It is exported with the frame count of the chosen fps (e.g. 6 seconds = 144 frames at 24 fps, 360 frames at 60 fps).
3. How choppy the motion looks is set separately from fps, by the **Animate on** setting in the "Effects" tab.
   - **Twos (12 drawings/s)**: the slightly jerky motion typical of lyric videos. Looks the same at any export fps (default).
   - **Threes (8 drawings/s)**: even more hand-animated, with more held poses.
   - **Ones**: moves on every frame at the output fps. 60 fps + Ones is the smoothest (camera moves and scrolling bands look clean).
4. Random switching in glitches and flicker runs at the same speed as at 24 fps whatever fps you choose. Exporting at 60 fps does not make the flicker twice as fast.
5. Rule of thumb: 24 fps (or 30 fps) for YouTube / music videos; 30 to 60 fps + Ones for smoother vertical social videos. 60 fps and 4K take a while to export.

In the AE panel, choose the comp frame rate with the panel's "fps" setting (24 / 30 / 60). When building from JSON, the comp uses the fps chosen in the browser app.

### Expression parts (combined automatically)

There are **707** parts in total (356 from the first public release + 351 Extras. Extras become random candidates when "Include Extras" is on). Each cut combines one part from each category (0 to 3 for decor).

| Category | Count | Examples |
|---|---|---|
| Layout | 140 | center, vertical, bleed off screen, lower-third caption, speech bubble, manuscript paper, letter rain, tunnel, neon, end credits, magazine spread, table of contents, newspaper, vinyl record, cassette, Polaroid, stamp sheet, ema votive plaque, paper lantern, noren curtain, tanzaku strip, omikuji fortune, hanging scroll, shoji screen, station sign, cube, cylinder, waving flag, pendulum, building blocks, letter balloons, LED board, signboard, crossword, puzzle, shadow play, kaleidoscope, zipper, stencil… |
| Enter | 100 | assemble, slice, flip, dominoes, iris, blinds, spiral gather, neon light-up, stamp, spring, slingshot, bouncing ball, fan open, cylinder roll, stop motion, sticker on, uncrumple, letter unfold, split-flap, magnifier, film advance, CRT power-on, loading, drum roll, data rain, brush sweep, ink drop, count-in, stroke by stroke… |
| Hold | 38 | jitter, float, sway, beat pulse, heartbeat, jelly, candle flicker, gust, dangle, stretch with loudness, beat invert, sheen, occasional flip, focus pull, string vibration… |
| Exit | 86 | explode, collapse, doors close, TV off, suck in, melt, backspace, sticker peel, crumple and toss, tear away, burn away, blackboard eraser, blow away as sand, shredder, float off on balloons, glass shatter, tornado, flutter down, shockwave, sink underwater, sword slash, blow out… |
| Decor | 115 | crosshairs, crop marks, radar, dimension lines, confetti, petals, light leak, bokeh, brush sweep, seal stamp, family crest, seigaiha waves, fireworks, lanterns, shimenawa rope, folding fan, autumn leaves, mist bands, circuit, registration marks, staples, paper clip, starry sky, moon phases, fireflies, Memphis, play button, like, music notes… |
| Text treatment | 52 | bold outline, edging, 3D, long shadow, glow, highlighter, halftone, emphasis dots, neon tube, chrome, rainbow, misregistration, multi-shadow, stencil letters, karaoke, circled, corner brackets, reflection, sticker edge, manuscript-paper style, ransom-note cut-outs… |
| Background | 62 | radial burst, concentric circles, spotlight, giant letters, retro grid, polka dots, aurora, mesh gradient, seigaiha, asanoha, houndstooth, tartan, contour lines, starry sky, moonlit night, cityscape, sunset, ocean waves, rainy window, fireworks, mountain range, VHS noise, marble, paper cutout… |
| Camera | 28 | slow push-in, pan, Dutch angle, handheld, beat zoom, crash zoom, orbit, barrel roll, pendulum, focus in, earthquake, vertigo, swirl zoom, snap pan… |
| Screen effects | 66 | slice / block glitch, invert, flash, RGB split, VHS roll, strobe, film burn, radial chromatic aberration, bloom, fisheye, pixel sort, 1-bit dither, kaleidoscope, anamorphic flare, TV static, film scratches, speed lines, sparkle, color bars, shattered glass, shutter… |
| Transitions between cuts | 20 | edge wipe, diagonal band wipe, clock wipe, iris in, push, cover, zoom through, double doors, blinds, checkerboard, breakout, whip pan, ink, tile collapse, cube, flash, mosaic… |

- Text treatments are used more often the higher "Decor amount" is. Backgrounds are chosen per line ("Background switching" makes them change more often).
- Transitions between cuts are inserted now and then, depending on motion strength, where one cut runs straight into the next (the last frame of the previous cut is composited with the next cut for the switch).
- Every part carries mood tags (Glitch / Mellow / Pop / Graphic / Editorial / Emotional), and Auto mostly uses parts that suit the chosen mood.

Below is the list of the base set (the parts that are also in the AE panel).

- **Layout (17)**: Center / Big-Small Mix / Vertical / Marquee / Tile / Scatter / Ring / Wave Path / Bleed Off Screen / Labels / Condensed / Annotation / Type / Diagonal Band / Round Window / Afterimage Stack / Capsule
- **Enter (13)**: Assemble (breaks each glyph into strokes or components) / Slice / Type / Pop / Drop / Stretch / Wipe / Blur / Spin / Flicker / Scramble / Zoom / Cut
- **Hold**: Jitter / Drift / Breathe / Wave / Glitch
- **Exit (11)**: Explode / Collapse / Dissolve / Slice / Wipe / Shrink / Blur / Stretch / Scatter / Glitch / Cut
- **Decor (15)**: Frame Marks / Coordinate Rings / Dot Ring / Arrows / Slashes / Sparks / Leader Lines / Waveform / Barcode / Grid / Stripes / Ink Blots / Rough Bars / Shapes / Big Number
- **Finish**
  - Time-lagged color offset (RGB split)
  - Full-screen slice glitch / block glitch
  - Invert / flash / zoom blur / mosaic
  - Shake / on twos / grain / paper texture / scanlines / bloom / vignette

---

## Using the After Effects panel

The panel is not translated in this edition, so its labels are in Japanese. The Japanese label is given in brackets where it helps you find it.

### Installing

1. Put `JIZURA_AE.jsx` in the following folder and restart AE.
   - Windows: `C:\Program Files\Adobe\Adobe After Effects <version>\Support Files\Scripts\ScriptUI Panels\`
   - Mac: `/Applications/Adobe After Effects <version>/Scripts/ScriptUI Panels/`
2. Open the panel from the menu with "Window" → "JIZURA_AE.jsx". It can be docked.
3. To just try it out, "File → Scripts → Run Script File" also works (it opens as a floating window).

### Usage

- **From lyrics** (「歌詞から」): set the lyrics, style, size and effects, then press "Generate comp" (「コンポを生成する」).
  - Timing can come from one of three sources:
    - Auto (calculated from character count and BPM)
    - Markers on the selected layer
    - Comp markers
  - Recommended workflow: select the song layer, play it, and press `*` on the numeric keypad at the start of each line to drop markers. Choose "Use selected layer's markers as line starts" (「選択レイヤーのマーカーを行頭に使う」) and generate.
- **Auto-generate** (「おまかせで生成」): each press randomly sets the style, mood, effect strength, on twos / flash / HUD, seed and colors, shows them in the panel, and builds a new comp. If you like the result, adjust the values from there and rebuild with "Generate comp".
- **Mood** (「雰囲気」, in the "Effects" (「演出」) section): when chosen, the build is limited to layouts and enter / exit techniques that suit that mood. Which techniques it narrows to is decided by the seed, so the same seed gives the same result.
- **Accent & offset colors** (「アクセント・ズレ色」): "Random colors" (「ランダム配色」) picks a new accent color and offset colors A/B. You can also type them directly as `#RRGGBB`. When "Override style colors" (「スタイルの色を上書き」) is checked, they are applied to every scene of the generated comp (brightness is corrected automatically to suit the background).
- **About the newer parts in the browser app**: the AE panel can only build with the base-set parts (17 layouts, 13 enters, 6 holds, 11 exits, 15 decor). The browser app's "Export for AE" replaces each newer part with the closest base part (text treatments, backgrounds, camera and transitions between cuts are not supported in the AE version and are not used). When something has been replaced, the status line at the bottom of the panel shows 「置換あり」 ("replacements made").
- **About the added styles**: structures made with the styles added in the browser app (the 12 from Sakura to Golden Night) keep their colors and typeface settings when loaded as JSON (if a typeface is not on your computer, a close typeface or the one set in the "Fonts" (「フォント」) tab is used). The AE panel's own style list and parts are still base set only. The Extras are planned for a future update.
- **Size**: 1920×1080 / 1080×1920 / 1080×1080 / 3840×2160 / 1280×720 / 1440×1080 (4:3) / 1080×1440 (3:4), or the same size as the active comp.
- **From JSON** (「JSONから」): loads JSON made with "Export for AE" in the browser app. The structure you set up in the browser is built as is in AE.
- **Fonts**
  - If Noto Sans JP / Noto Serif JP / Dela Gothic One etc. are installed, they are used automatically (automatic selection needs AE 2024 or later).
  - Otherwise the typefaces set in the "Fonts" tab are used. The defaults are Yu Gothic and Yu Mincho.

### What gets generated

- A precomp per cut (in the `JIZURA <song title> cuts` folder)
  - Text moves with text animators (Expression Selectors), so the motion survives if you retype the text.
- The color offset is made from ghost layers: each cut is duplicated with a time lag and colored with the "Tint" effect.
- The `JZ FX` adjustment layer at the top holds:
  - on twos (Posterize Time)
  - shake (Transform)
  - slice glitch (Wave Warp)
  - zoom blur / invert / glow / noise
- `JZ Flash`, `JZ Vignette` and a HUD (timecode, line counter) are generated too.

### Notes

- From AE 2020 on, the expression engine is expected to be JavaScript (the default for new projects).
- This panel has been tested in an environment that mimics AE's object model. Every style × every layout × every enter / exit combination, plus Auto generation and random colors, ran without errors. It has not yet been run in real AE, though. If something unexpected happens with an effect's settings etc., those items are listed after generation and the rest of the build carries on.

---

## Development & build

```
python3 build.py              # src/ app/ vendor/ → index.html
node tools/export_ae_data.js  # after changing styles etc.: updates ae/data.json
python3 build_ae.py           # ae/ → JIZURA_AE.jsx
```
All you need to build is Python 3 and Node.js (no npm packages). To add expression parts, see `docs/EXPRESSION_PACKS.md` (test tools are in `dev/`).

### Publishing from your own repository (e.g. a fork)

1. Push with `index.html` at the repository root.
2. In **Settings → Pages**, set Source to **Deploy from a branch** and Branch to `main` / `/ (root)`, then save.
3. A few minutes later it opens at `https://<username>.github.io/<repository>/`.

## License

[MIT License](LICENSE). You may use, modify and redistribute it, commercially or not (on condition that the copyright notice and license text are included).
The rights to videos and images made with this tool belong to the person who made them (and to the owners of the lyrics and songs). This software's license does not extend to the output.

For bundled third-party software, see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
