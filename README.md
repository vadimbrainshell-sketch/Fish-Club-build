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
