# Tencent Hy4 vs DeepSeek V4.1 Flash 1017: race, voxel diorama, channel intro

Two Chinese models at almost the same price, the same short prompts, the same agent. No hints from me: each model writes, runs and checks its own work.

**▶ Play in your browser:** https://kostikoneuro.github.io/hy4-vs-deepseek/
**🎬 Video (Russian):** https://youtu.be/n5gRqTFIYSc
**💬 Telegram:** https://t.me/kostik_neuro

> Русский: все игры и диорамы можно открыть прямо в браузере по ссылке выше. Промпты в папке [`prompts/`](prompts/).

## The tests

| # | Test | Hy4 | DeepSeek |
|---|---|---|---|
| 1 | **Neon Night Racer**: 80s arcade racer in the browser | [play](1-race/hy4/) | [play](1-race/deepseek/) |
| 2 | **Night market voxel diorama** in Shenzhen: Three.js, 30-second fly-through, `C` = free camera | [open](2-diorama/hy4/) | [open](2-diorama/deepseek/) |
| 3 | **Channel intro**: 10 s, the model studies the channel by itself and makes the intro in [OpenMontage](https://github.com/calesthio/OpenMontage); $5 for everything | [video](3-intro/hy4.mp4) | [video](3-intro/deepseek.mp4) |

Controls in the race: Hy4: arrows / WASD, **Shift** = nitro, Enter = start. DeepSeek: arrows / AD, **Space** = nitro, ↓ = brake.

The exact prompts (Russian, short on purpose) are in [`prompts/`](prompts/).

## Time and cost

Costs at CometAPI prices (80% of the official list price). Official list per 1M tokens: Hy4 $0.834 in / $2.501 out; DeepSeek V4.1 Flash $0.15 in / $0.60 out. Token counts come from the session logs; test 3 includes paid images, video, music and sound effects.

| Test | Hy4 | DeepSeek |
|---|---|---|
| 1 Race | 28 min · $0.52 | 38 min · $0.29 * |
| 2 Diorama | 30 min · $0.69 | 80 min · $0.43 |
| 3 Intro | 52 min · $2.62 (assets $0.84) | 62 min · $0.75 (assets $0.54) ** |
| **Total** | **110 min · $3.83** | **180 min · $1.47** |

\* 61 min wall clock; 23 min of it the run was stuck on my harness (a local server kept a tool call open), not on the model.
\** Includes the one allowed fix: DeepSeek's sound-effect requests had failed on the provider side, so after the route was fixed I asked it once to add real sound effects (9 effects via CometAPI, Kling audio).

## How it was run

- **One harness for both: OpenCode 1.19**, headless, with a headless Playwright browser so the model can play and check its own work. A clean config folder per run: no personal instructions, no skills, no other API keys.
- Reasoning at the top level each model accepts: DeepSeek `max`, Hy4 `high`. DeepSeek only outside its peak hours.
- One prompt per test, at most one fix (used once: DeepSeek, test 3, sound effects), $5 and 3 hours per model per test.
- Test 3 (intro): the only paid generation allowed was CometAPI through OpenMontage's `comet_*` tools. DeepSeek's first sound-effect requests were refused by the provider ("not enough credits" on the ElevenLabs route); I added a Kling text-to-audio fallback to `comet_sfx` and used the one allowed fix to ask DeepSeek to add real sounds. Before starting, DeepSeek also read the files of older intro projects in the OpenMontage folder (from earlier videos); Hy4 did not.
- Test 2: Hy4 said it cannot see images and checked its fly-through by pixel statistics; DeepSeek downloaded a small open captioning model (BLIP) to describe its own screenshots and made 11 versions.

## Bonus: the disqualified DeepSeek run

[`bonus/deepseek-disqualified-race/`](bonus/deepseek-disqualified-race/) is an earlier DeepSeek race run (on the older, long English prompt) that I did not count: in the middle of the run it found another provider's API key on my computer and sent its screenshots to Gemini for art-direction scores (the critiques are in the folder), and its local server briefly opened Hy4's game on the same port (`our_menu.png`). After that I closed every outside key and separated the ports, and all runs above are clean.

[▶ play the disqualified version](bonus/deepseek-disqualified-race/)
