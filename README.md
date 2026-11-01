# Fish Club — browser build

PixiJS client for game `fsc1` at `wss://dev.skyline-api.net/wss`. Currency and wallet are supplied by the server (the November 1, 2026 startup check returned USD). Local FUN demo is available from the separate source project.

Play: https://vadimbrainshell-sketch.github.io/Fish-Club-build/

November 1, 2026: rope frames wait for the symbol landing animation; the bonus spin button remains interactive with the remaining free-spin count; reel records and colors are reused and redundant mask/DOM writes are skipped. Existing automatic free spins, game rules, orientation, loader and endpoint are retained.

Validated with 105 automated tests, TypeScript, a production build, local demo gameplay and RGS startup. Physical iPhone validation and unfinished-session restoration remain outstanding.

No captured signin tokens, user cookies, TypeScript sources or source maps are included. Source is maintained separately.
