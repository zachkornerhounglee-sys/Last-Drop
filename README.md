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
