# LAST DROP v4

A browser-based battle royale prototype built with Three.js and PeerJS. Upload `index.html` to the root of a GitHub repository and enable GitHub Pages to host it.

## Play

- **Play vs Bots**: start an offline match.
- **Host Game**: create a room and share the invite link or six-digit code. The host's browser runs the match simulation, so keep that tab open.
- **Join Game**: enter the host's room code or open their invite link.

## Default controls

| Action | Key |
|---|---|
| Move | W / A / S / D |
| Sprint | Left Shift |
| Jump / jump from bus | Space |
| Slide | Left Ctrl (while moving quickly) |
| Aim | Mouse movement |
| Fire / shoot | Left mouse button |
| Interact / pick up | E |
| Hotbar | 1–5 |
| Reload | R |
| Use health item | H |
| Use shield item | J |
| Build wall | F |
| Emote | G |
| Toggle map | M |
| Graphics quality | Q |

Open **Settings / Keybinds** on the main menu to rebind movement, slide, fire, inventory, building, and other actions. Actions can be assigned to a mouse button or keyboard key. Duplicate bindings swap with the previous binding. Keybinds are saved in the browser on that device.

## Match flow

The Battle Bus crosses the island. Jump, freefall, glide, land, loot, and fight while the storm closes in. The last player standing wins.

## Loot and movement weapons

- Weapons: Assault Rifle, Pump Shotgun, SMG, Sniper Rifle, Pistol, Rocket Launcher, Grappler, Shockwave Hammer, and Pickaxe.
- **Grappler**: spend a charge to pull yourself forward in the direction you are facing.
- **Shockwave Hammer**: spend a charge to launch yourself forward and upward.
- Health items: Bandages and Medkits. Use `H` by default.
- Shield items: Mini Shields and Big Shields. Pickups are stored in your inventory and show a pickup notice; use `J` by default to consume one. Mini Shields restore up to 50 shield, while Big Shields can restore shield up to 100.
- Ammo and materials are collected as pickups. Eliminated players drop their inventory.

## Island

The island contains named areas including Neon Heights, Pinewood, Rust Yard, Fort Cinder, Dune Bazaar, Sunny Acres, Hollow Peak, Lazy Lake, Vault 9, Willow Creek, and other points of interest. Many small buildings can be entered.

## Network notes

PeerJS is used for room discovery and WebRTC connections. The game also uses public STUN/TURN services as connection fallbacks. Some restricted networks may block peer connections. The host must keep the hosting tab open during the match.

## Compatibility and testing

The project uses CDN-loaded Three.js and PeerJS, so an internet connection is required. The updated inline JavaScript passes a Node syntax check and targeted checks for keybinds, slide state replication, movement weapons, and shield use. Real multiplayer across separate devices and performance on all browsers/networks have not been verified in this environment.
