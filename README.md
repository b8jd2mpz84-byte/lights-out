# Lights Out

A reaction-time game: five red light pairs, then darkness. Tap the instant they drop.
Plain HTML/CSS/JS, no build step, installable on iOS and Android as a PWA.

## Modes

- **Practice**: free runs, chase a personal best.
- **Qualifying**: five starts, your quickest clean one is pole.
- **Sprint**: ten starts, each jump adds 0.500 s.
- **Race**: five starts against five AI drivers. Points for P1 to P6 (25, 18, 15, 12, 10, 8), nothing for a jump.
- **Season**: an eight-round championship against the same five drivers. Each round is three starts; lowest total time wins (a jump adds 0.6 s), F1-style points build the standings, and the field gets quicker every round. Win the Club title to unlock the Pro field.

After every Season round a card shows your three starts with their average, the round result and the standings. Tap any round in the R1–R8 strip to reopen its card, or **Review** for season stats (average and best start, jumps, wins, podiums), a per-round log and your past seasons.

Anticipating the lights is allowed: a tap of 15 ms or more after they go dark counts. Any earlier is a jump start, so guessing is high risk, high reward.

## Run locally

    npx http-server . -p 8765     # then open http://localhost:8765

Service workers need `http://localhost` or HTTPS; opening the file directly still plays, just without offline support.

## Host on GitHub Pages

1. Repo **Settings > Pages > Build and deployment**: source **Deploy from a branch**, branch `main`, folder `/ (root)`.
2. The game is then at `https://<user>.github.io/lights-out/`.
3. All paths are relative, so it also works from a sub-folder.

Note: Pages on a **private** repo needs a paid GitHub plan (Pro, Team or Enterprise). On a free plan, make the repo public first.

## Install on iPhone

Open the Pages URL in **Safari**, tap Share, then **Add to Home Screen**. It then runs full screen and offline,
and Safari stops expiring its saved records (browser tabs lose site data after about 7 days of non-use).

## Shipping updates

Installed copies refresh from cache in the background. After changing any file, bump `VERSION` in `sw.js`
so installed copies pick up the new files on their next launch.

## iOS notes

- Audio unlocks on the first tap's release and is routed as "playback", so the ringer switch does not mute it.
- Haptics: Android uses the Vibration API. iOS 17.4+ uses a hidden `<input switch>` trick (best effort, result ticks only).
- Times include screen and touch latency, so compare scores on the same device.
