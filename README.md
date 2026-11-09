# Fish Club — browser build

PixiJS client for game `fsc1` at `wss://dev.skyline-api.net/wss`. Currency and wallet are supplied by the server. Local FUN demo is available from the separate source project.

Play: https://vadimbrainshell-sketch.github.io/Fish-Club-build/

Latest update (November 1, 2026):

- Performance window opens on the right by default, with frame/CPU/GPU timings (when supported), memory estimates, draw calls, texture uploads, Spine/pool counters, last-spin statistics and WebGL context-loss state. Close removes profiling hooks; PERFORMANCE reopens it; `?perf=0` starts without instrumentation.
- Balanced rendering limits resolution to 1.5x on desktop / 1x on coarse-pointer devices. High (up to 2x) and Performance (1x) can be selected without restarting the session. Water filter renders at 1x.
- Reel filler updates existing sprites in place without detach/attach or repeatedly configuring neighbours; spare rolling sprites are prepared during loading.
- Spine backdrop applies its transparent initial animation pose before becoming visible. Collect fades are cancelled correctly when symbols are reused.
- Bonus free spins now require the player's SPIN / Space input. The remaining count and manual quick stop are retained. Base-game autoplay, game rules, orientation, loader and server endpoint are unchanged.

Validation: 111 automated tests, including the actual fish-background Spine data and uneven-frame reel settlement, TypeScript and production build. Browser profiling in this session was affected by heavy host load and WebGL context loss; a stable frame rate and a complete interactive rerun were not confirmed. Physical iPhone validation and unfinished-session restoration remain outstanding.

No captured signin tokens, user cookies, TypeScript sources or source maps are included. Source and technical continuation notes are maintained separately.

Latest shader refinement: the water effect shares identical ripple calculations between temporal samples, keeping four texture samples and the same rendering resolution. The performance panel now displays the WebGL GPU device name. TypeScript and production build passed; the three panel tests passed. FPS improvement is not yet measured.

GPU selection refinement: WebGL now requests `powerPreference: high-performance`. This is a browser hint; inspect GPU device after a full reload to verify adapter selection. No rendering-quality, resolution or antialias settings were changed by this refinement.

Bug fixes (November 10, 2026): captions reset on pooled-symbol reuse; the tail plays on completed spins with a 30% cosmetic chance; the bonus reward counts up using the final server payout, including terminal receipts with zero placeholders; stopped-cell borders use four preallocated rope Spine parts and stop CPU updates when their animation ends. Shared cell borders are drawn once without stencil masks. Raw Spine frame parts are included in performance counters.

Validation: 116 automated tests passed, including caption reuse, real bonus reward count-up, tail probability and rope lifecycle; TypeScript and the production RGS build passed. Computer Use remains disabled; live visual inspection of the new rope layout is pending.
