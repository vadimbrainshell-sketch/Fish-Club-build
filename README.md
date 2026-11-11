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

Further fixes (November 10, 2026):
- Rope animation runs at 2x speed. Pooled symbols clear their previous Spine tracks/pose; mines stay idle until every reel and bounce has stopped, then result presentation triggers crush.
- Turquoise line highlights are retained as requested. Fish background filter bounds cover both animations, stabilizing intermediate target dimensions while keeping the shader, antialiasing and render resolution. Current GPU average now uses the most recent reporting window. FPS improvement has not been measured interactively.
- Collect waits for a confirmed server receipt and the amount pulse before releasing fish. Send/disconnect errors do not escape as unhandled rejections, the matrix is retained for unconfirmed cashout, and monetary requests are never retried automatically. Minimal cashout receipts with omitted/null reels and events are supported only for a correlated cashout and require a numeric final win. Missing wallet leaves the last confirmed wallet intact.
- The left SOCKET LOG panel captures inbound/outbound frames and connection/runtime errors locally, including rejected frames and socket close code/reason. Pause, Clear, Hide and Save JSONL are available. History is bounded to 500 records / 2 MiB; the panel shows the latest 100. Credentials are masked. Connection lost also shows the actual fault and offers log export.

Validation: all 126 automated tests passed, plus a repeated focused check for minimal cashout without wallet. Final TypeScript/production RGS build passed. Computer Use remains disabled. The user's original Connection lost reason cannot be confirmed until its wire frame or close code is captured; real-money cashout was not exercised.

Confirmed Collect protocol fix (November 10, 2026): fsc1 returns manual cashout payouts in events[type=cashout].win with total:{bet:0}, omitting total.win. The client previously rejected that valid receipt and closed its own socket. Validation now accepts an explicit total.win or the unique explicit cashout-event win, including zero; it never derives settlement from regular fish wins, possible_win or wallet differences. UI normalization uses that same server payout.

Validation: all 129 automated tests passed, TypeScript and production build passed. Offline replay of the supplied 146-record session accepted all 69 bet replies, including the cashout, with no faults and a connected socket. No live monetary requests were made. User logs, opaque contexts and credentials are not included in this repository.

Bonus result and exit lifecycle (November 10, 2026): terminal fsc1 bonus receipts can omit every final payout field while retaining regular and multiplier_symbol monetary awards. The reward display now uses those explicit server award amounts once, with no repeated multipliers or client wallet credit. Captured case 0.10 + 0.50 + 4.80 displays 5.40. Explicit final payouts, including zero, retain priority.

Bonus exit now clears HUD captions/flights and line effects, releases settled bonus symbols through the shared pool, empties bonus cells/locks/frames, resets retrigger state and closes reward animation/audio resources during the curtain. Retained base symbols resume in idle rather than continuing frozen landing/fade. All Spine objects are constructed with autoUpdate:false. Turquoise highlighting and visual resolution are preserved.

Validation: all 134 tests, TypeScript and production build passed. A real Spine hidden behind an inactive bonus root received no updates over 600 frames and had no independent ticker subscription. Thirty repeated exits with the real SymbolPoolService produced no prefab growth after warmup. These checks establish lifecycle behavior; they do not measure browser FPS or prove the original FPS cause.

Suspense presentation (November 11, 2026):
- A transform-only camera gently zooms up to 1.14x toward a lingering tail of 1–3 spinning cells. It waits for a genuinely long stop, eases back afterward and resets on modals/resize. Ordinary reel timing, results and requests are unchanged. No extra WebGL filters or render targets are added.
- The circular iris is replaced by an inline vector fish-skeleton sprite aperture. The viewport-sized SVG luminance mask shrinks to fully closed before the scene swap, then opens again, retaining the existing transition durations. Portrait/landscape coverage is preserved.
- Bonus Buy now starts the existing matrix bounce on each actual cell stop. The normal BounceSystem applies the same authored duration/curve as regular spins; cells are locked and frames presented after bounce completion, and bonus entry waits for the final bounce.

Validation: all 139 automated tests, TypeScript and production RGS build passed. Tests cover camera activation/reset, complete fish aperture closure/coverage, and the real BounceSystem during purchase. The new sprite was inspected using a local SVG thumbnail. Computer Use and live monetary gameplay were not used.
