# LAST DROP v3 (big island)
Host-authoritative PeerJS multiplayer (room code / `?join=CODE` link). Upload `index.html` to a GitHub repo, enable Pages, open the site.

## Play
PLAY VS BOTS (offline), HOST GAME (room code + invite link, keep tab open), JOIN GAME (type code).
Controls: WASD, Shift sprint, Space jump (and jump from the bus), mouse aim, click fire, E open chest / pick up, 1-5 hotbar, R reload, H heal, J shield, F build wall (10 mats), M big map. Pickaxe trees for materials.

## Match flow
Drop Bus crosses the island on a random route > press Space to jump > freefall > glider auto-deploys > land, loot, fight > storm shrinks > last one standing wins.

## POIs
Neon Heights (city), Pinewood (suburbs), Rust Yard (industrial), Fort Cinder (military), Dune Bazaar (desert + pyramid), Sunny Acres (farm), Hollow Peak (mountain + hermit shack), Lazy Lake, Vault 9 (secret bunker). Most small buildings are enterable.

## Loot
Chests (glow, open animation) and floor loot. Rarities: Common, Uncommon, Rare, Epic, Legendary, Mythic (damage scales per tier; military/secret chests roll higher). Weapons: Assault Rifle, Pump Shotgun, SMG, Sniper, Pistol, Rocket Launcher, Pickaxe. Heals: Bandage, Medkit, Mini/Big Shield. Eliminated players drop their loot.

## Network services (free, third party)
PeerJS public broker (handshake), Google STUN, openrelay.metered.ca TURN fallback. Strict networks may still fail.

## Not implemented
Duos/squads, knockdowns/revives, ADS, ramps/floors/edit, cosmetics, progression, settings, audio, bots building, host migration, reconnection, delta compression, full interiors with stairs/multiple floors, real animated 3D model files (characters are built from primitives).
Tested: syntax check + headless host simulation (bus, drop, glide, chests, loot, combat, storm, win). NOT tested: rendering, real multiplayer between two machines.


## v3 changes
- Island ~1240 units across (about 3x the v2 radius): 16 named POIs, roads, a river, a lake, ~46 hamlets, ~2,000 instanced swaying trees.
- Static buildings are batched into one mesh (fast); loot/chests/players are distance-culled.
- Bus is faster and higher (altitude 200). Dive is fast, glider auto-deploys. Bots pick far landing spots.
- Storm is now 7 phases with random safe-zone centers, a next-circle preview on the map, a countdown, and rising damage.
- Animation rig: knees/elbows, run/sprint lean, idle breathing, jump tuck, landing squash, freefall pose, glider pose, weapon recoil + muzzle flash, G emote, death fall.
- Effects: particles (muzzle, impacts, explosions, chest burst, landing dust, storm motes), camera collision/smoothing/shake, sprint/dive FOV, soft shadows (Q cycles quality), sky dome, animated water, textured ground, storm/low-health vignette.
- Menu: a 3D hero idles/emotes on the beach while the camera orbits.
- Headless test: world gen, bus drop, glide, chests, loot, combat, 7-phase storm, win condition, one render pass with stubbed graphics. NOT tested: real GPU rendering/performance, real multiplayer.

## v4 changes
- **Shields/heals are real consumables**: walking over them no longer vaults them into a hidden counter. Press E to pick up. A consumables bar (bottom right) shows Bandage / Medkit / Mini Shield / Big Shield counts. H and J auto-pick what to use; keys 6-9 use a specific item. Items are only used if they'd help (Mini caps shield at 50, Big at 100), and you see "Using ..." while it applies.
- **Slide (C)**: while moving, tap C for a fast, steerable slide with a low pose and dust. Jump out of it to keep your momentum.
- **Movement weapons** (found in chests / floor loot, hotbar slots, rarity improves range and recharge):
  - Grapple Gun: shoot a surface to reel yourself to it; jump mid-pull to release and fling. 4 charges that recharge.
  - Blink Rod: short teleport forward (stops at walls). 3 charges that recharge.
  - Jetpack: hold fire to rise, fuel bar shows as the ammo number, recharges on the ground. Bots ignore these.
- **Rebindable controls**: press K (or CONTROLS in the menu) to rebind every key. Saved in the browser (localStorage). Defaults: C slide, 6-9 consumables, K controls.
- Not tested: real rendering and real two-machine multiplayer. Client-side prediction is simple, so on a joined client the grapple and blink are host-authoritative and may look snappy/rubber-bandy.

## v5 changes (smoother / more Fortnite-like)
- Crosshair that blooms with movement and firing.
- Aim down sights (right-click): zoomed FOV (sniper zooms more), camera pulls in over the shoulder, tighter spread, slower move/look.
- Netcode smoothing: snapshots 30 Hz (was 15), client input 60 Hz (was 30), tighter remote interpolation.
- Still not implemented: ramps/floors/edit, crouch, squads, audio. Untested: real rendering and two-machine play.

## v6 changes
- **Builds**: F wall, V floor, B ramp (10 mats each, start with 100). Ramps and floors are walkable (stack ramp > floor to climb); walls/floors/ramps snap to a 4-unit grid at your current level. Floors/ramps don't block bullets yet and can't be destroyed.
- **8 unique landmarks** (random spots per match seed): Lighthouse (rotating beam), Old Windmill, Fun Fair (ferris wheel), Water Tower, Giant Tree, Stone Ring, Radio Tower, Shipwreck. Each has chests; they show on the map.
- **UI**: new left-aligned main menu over the 3D hero, styled lobby (room-code card, player chips, big start button), numeric HP/shield bars, panels behind HUD text, build hints. Fixed a leftover crosshair dot / filled-circle bug.
- Untested: real rendering/performance and two-machine play.

## v7 changes
- **Shockwave Hammer** (new, rechargeable: 3 charges, +1 per ~6s): slam launches you up/forward and blasts nearby enemies away with damage; cyan shockwave ring + light flash. Found in chests/floor loot.
- **Movement items tuned**: Grapple has a visible rope (all players see it), longer range, faster pull; Blink has 4 charges, faster cooldown and a particle trail; Jetpack has more thrust, better air control and bigger flames; slide unchanged.
- **Visuals**: glowing streak tracers that travel to the target, soft round particles (was squares), muzzle/impact/explosion light flashes, hit-marker colour on the crosshair.
- **Build mode with preview**: press F/V/B to pick wall/floor/ramp, a translucent outline shows exactly where it will go (green = ok, red = blocked or no mats), click to place, right-click or 1-5 to exit.
- Untested: real rendering/performance and two-machine play.
