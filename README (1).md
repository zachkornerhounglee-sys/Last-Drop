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

## v8 changes
- Guns nerfed ~25% (AR 30>22, Shotgun 11>8 per pellet, SMG 17>12, Sniper 92>70, Pistol 24>18, Rocket 95>75). Bots aim a bit worse (more spread and aim wobble).

## v9
- Bot cap raised from 30 to 100 (menu and host lobby). Very high counts may lower framerate.

## v10 (built on your optimized index_1.html)
- Multiplayer movement: clients send inputs at 60 Hz with their predicted position; the host follows it when it is plausible (<5 units off) and overrides it during knockback, blink, grapple, jetpack and slam. Remote players use velocity extrapolation on top of smoothing.
- Shaders: rim light + saturation/contrast grade injected into every Lambert material (onBeforeCompile).
- Houses: foundations, corner posts, eave trim, chimneys, window frames + shutters, door frames, awnings, steps, steeper roofs.
- Shockwave Hammer: grounded = jump-slam with launch + small blast; airborne = dive slam that detonates a large shockwave on landing (radius/damage scale with rarity). Double ring, dust, light flash, shake.
- Audio: procedural WebAudio sounds (shots, hits, explosions, shockwave, blink/grapple, building) with distance falloff. Click once on the page to unlock audio.
- Untested: real GPU shader compile, rendering, and two-machine play.

## v11
- Shockwave Hammer movement: cooldown 0.8s; ground use = higher jump-slam with forward launch and half gravity for 0.75s (floaty arc); air use = dive slam in the direction you look at 46 u/s, landing blast grows with fall height and bounces you up. Chain jump-slam into dive-slam.
- ESC pause menu: FOV, sensitivity, volume sliders (saved in localStorage), resume, controls.
- Footstep and chest-opening sounds.
- Progression: level + XP bar and career stats (matches/wins/elims) on the main menu, XP awarded at match end (saved in localStorage).
- Not implemented from the master prompt: duos/squads, interiors with stairs, cosmetics/locker, quests, crouch/mantle/swim, real TURN fallback, host migration. Untested: rendering and two-machine play.

## v12
- Teams: SOLO / DUOS / SQUADS selector in the host lobby (before START). Teams are filled in join order, bots fill empty teammate slots. No friendly fire, bots ignore teammates, team panel on the left of the HUD, win condition is last team standing (XP awarded to the winning team). No knockdown/revive yet.
- Crouch (Ctrl): half speed, shorter model, visible to others. Vault: hold jump against a low obstacle (under ~2.4 units, not walls) to hop over it. Swim: in water your model sinks and splashes, movement is slowed (no stroke animation).
- Interiors: large buildings (tall + long, e.g. Rust Yard / military halls) get a ramp-style staircase and a walkable second floor along the back wall. Floors/stairs are walkable but do not block bullets.
- Locker (main menu): 8 outfits, 4 headwear, 4 back blings. Saved in the browser, synced to other players at match start. Cosmetics are visual only.
- Bot cap 100 applied to this file too.
- NOT done: host migration (needs full simulation state transfer + peer reconnection; if the host leaves the match ends), mantle animation, TURN fallback, other master-prompt items.
- Untested: rendering and two-machine play.

## v13
- Fixed held items: the arm rotations had the wrong sign (arms swung backwards while the gun floated in front). Armed arms now point forward with both hands on the weapon; unarmed/pickaxe follows the right hand; heal and slide poses fixed too. Crouch scale now applies (animChar was resetting it).
- Host migration (lobby-level): the host broadcasts the successor (lowest player id) every 2s. If the host disconnects, the successor opens a new room at a code everyone can compute, the others reconnect automatically (retries ~50s). The match in progress ENDS; the party returns to the new host's lobby. Full mid-match migration is not implemented.
- Fortnite-style lobby: party list on the left, chat bottom-left, big START/READY button bottom-right with mode tabs, 3D hero visible in the middle, room code top bar.
- Untested: rendering, and migration between real machines.

## v14
- Held items: arm and elbow rotations had the wrong sign, so arms pointed backward and guns floated in front. Fixed for every pose (armed, pickaxe, heal, slide, dive, glider, emote, dead). Gun now sits between both hands, pickaxe is in the right hand and swings on use.
- Facing: slide legs pointed backward and dive/dead/emote arms crossed over the body; fixed. The menu/lobby hero now always faces the camera (it used to show its back).
- Fortnite-style lobby: party list on the left (skewed cards, host star, READY badges, empty slots), chat bottom-left, big START/READY button bottom-right, room code top bar, 3D hero visible in the middle.
- Host migration: host broadcasts an ordered successor list. If the host disconnects, the lowest-id successor opens a new room at a code everyone can compute; the others auto-reconnect (falling through to the next successor if one is gone). A match in progress ENDS and the party regroups in the new lobby; full mid-match migration is not implemented.
- Untested: real rendering and real multi-machine play. Verified: syntax check, and hand positions checked numerically with three.js.

## v15 (features pulled from the master prompt)
- **ESC pause menu** (opens when the pointer lock is released, or press Esc again to resume): FOV, mouse sensitivity, ADS sensitivity and master volume sliders, saved in localStorage; Resume, Controls, Leave. The match keeps running while paused (online game).
- **Progression**: level + XP bar and career stats (matches / wins / elims) on the main menu. XP per match: 50 + 25 per elim + placement bonus + 300 for a win. Client placement is only known for the winner, so clients get no placement bonus unless they win.
- **Daily challenges** (reset each day): eliminate 3 players, play 2 matches, finish top 5. Each gives +150 XP.
- **Crouch** (hold X, rebindable): half speed, lowered pose visible to others. Hitbox is unchanged.
- **Locker**: 8 outfits and 4 back blings (none, cape, wings, jet pack). Saved in the browser and sent to the host on join, so everyone sees them. Cosmetics are visual only. Bots get random outfits.
- Bot cap is 100 everywhere (menu and host lobby). Very high counts may lower framerate.
- Still not implemented from the master prompt: duos/squads/trios, knockdown/revive, item shop/currency, quests beyond the daily three, mantle/climb, building edits/roofs/materials, bot building, weather, voice chat, graphics presets beyond Q, controller support.
- Untested: real rendering and real multi-machine play. Verified: syntax check only.

## v16 (merge of index__10_ and my v15)
Base is your index__10_ (teams SOLO/DUOS/SQUADS, locker with headwear + blings, pause menu, XP/level, crouch, Fortnite-style lobby). Added on top:
- Rig: dive, glider, emote, dead, slide and heal poses fixed (arm/elbow/leg signs); pickaxe is held in the right hand and swings on use.
- Menu/lobby/locker hero now faces the camera.
- Host migration upgraded: host broadcasts an ordered successor list; if the host drops, the lowest-id successor opens a new room at a code everyone can compute, others reconnect automatically and fall through to the next successor if one is gone. A match in progress ENDS and the party regroups in the new lobby.
- Daily challenges (eliminate 3, play 2 matches, top 5; +150 XP each) added to the level/XP panel.
- Bot cap 100 for PLAY VS BOTS as well (it was still 30).
- Skipped from my v15 because index__10_ already has better versions: pause menu, locker, crouch, progression, lobby layout.
- Untested: rendering and two-machine play. Verified: syntax check only.

## v17 (more of the master prompt)
- **Knockdown + revive** (team modes): when you would die and a teammate is still standing you go DOWN (crawl, slow, can't shoot, bleed out in ~25s, shown as DOWN in the team panel and orange on the map). A teammate presses E within 3 units and stays near for 4s to revive you to 40 HP. If your whole team is down, everyone dies. Bots stay down and bots revive downed teammates.
- **Trios** mode tab; **bot difficulty** (Beginner to Expert) in the host lobby and next to PLAY VS BOTS; **Lock lobby** button for the host.
- **Practice mode**: 5 beginner bots, no storm damage, no win condition, 500 mats.
- **Pause menu settings**: toggle sprint / crouch / aim, auto pickup, ADS sensitivity, crosshair colour and size (saved).
- **Floating damage numbers**, bigger for headshots.
- **Weekly quests** (+400 XP) and **achievements** (+100 XP) in a new CAREER screen.
- **Weather**: some matches (seed based, same for everyone) have rain.
- **Ping / marker**: Y places a shared team marker where you look (beam in the world, pin on the map); teammates are blue on the map.
- Still not implemented: item shop/currency, supply drops, creative mode, spectator camera controls, building edits/roofs/materials, bot building, voice chat, controller support, graphics settings beyond Q.
- Untested: real rendering and two-machine play. Verified: syntax check only; the knockdown logic has not been run.

## v18 (vehicles, bigger map, better buildings)
- **Vehicles**: Sedans, Pickups, Vans and **Reboot Vans** spawn at POIs and along roads (same positions for everyone, host-driven). Press E near one to drive, E again to exit. W/S accelerate/reverse, A/D steer, Space brakes, mouse looks (camera drifts behind the car). Running people over hurts them; trees/walls slow you; water drags you down. You can't shoot while driving. Bots do not drive.
- **Reboot Van** (cyan beam + label, team modes): stand next to it with a fallen teammate and press E to bring them back (100 HP, fresh loadout, 12s cooldown per van). Disconnected players can't be rebooted.
- **Bigger island**: radius 620 -> 950 (about 2.3x the area), 5 new POIs (Speedway, Airstrip, Coastal Resort, Oil Field, Quarry), 4 extra lakes, longer river, more roads, ~2.5x the hamlets/trees/loot, landmarks spread across the whole island.
- **Structures**: Neon Heights now has glass-and-concrete towers (podium, window grid with lit windows, mullions, crown, antenna). Houses gain window mullions, gutters, driveway and picket fence. Roads have shoulders and a center line.
- Not done: passengers, vehicle damage/fuel, bots driving, map icons for vans (they show as a cyan beam in the world). Untested: rendering and two-machine play. Verified: syntax check only.

## v19
- **Passenger seats**: Sedan 4, Pickup 3, Van 6, Reboot Van 4. E near a vehicle takes the next free seat (driver first). Passengers can shoot; if the driver leaves, the next passenger takes the wheel. Seated players are hidden inside the vehicle.
- **Reboot Van battery**: 100% max, a reboot costs 50%. It recharges slowly when parked and 4x faster while someone drives it. Green/orange bars on both sides show the charge and the beam only shows when a reboot is available.
- **Map**: square with rounded corners. POI names are no longer floating over the world; they appear on the big map (M), and a banner shows when you enter a POI.
- **Hills**: ~34 hills (terrain mesh, walkable, bullets and camera collide, trees/loot/vehicles follow the ground, cars tilt). They avoid POIs, roads, lakes and rivers and show shaded on the map.
- **Graphics UI**: P or pause menu > GRAPHICS (quality, shadows, auto-lower, FPS chip, resolution scale, view distance, saved). A small FPS/quality chip shows at the top during play.
- **Death fix**: the pause menu no longer pops up over the elimination screen and the mouse is released; the pause menu also has LEAVE MATCH.
- Untested: rendering and two-machine play. Verified: syntax check only.
