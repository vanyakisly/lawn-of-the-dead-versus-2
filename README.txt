PvZ Versus - online 1v1. Host plays Plants, joiner plays Zombies (room code, peer-to-peer via PeerJS public broker).
Run it with a web server (python serve.py style) or upload to GitHub Pages. Needs internet for PeerJS.
Plants win by surviving 5 minutes; zombies win by reaching the house.
Music: menu theme (lobby), Choose Your Seed (waiting for opponent), lawn theme (match). Mute button top-right.
Seed selection: each player picks up to 5 seeds before the match (host: plants, joiner: zombies); the match starts when both click Ready.
Plants: Sunflower, Peashooter, Wall-nut, Snow Pea, Cherry Bomb, Repeater, Chomper, Squash, Puff-shroom.
Zombies: Zombie, Conehead, Buckethead, Football, Newspaper, Pole Vaulter, Gravestone (the zombies' "sunflower": makes 25 brains every 8s; placed on any free tile; they pop out brains that you click to collect (auto-collected after 6s)).
Help button (on the lobby screen only): Crazy Dave explains the rules in a speech bubble.
Widescreen 16:9 board using the real day-lawn background; own-style HUD and seed chooser screen.
Characters are animated live on a canvas from the game's animation data + sprite parts (assets/anim.js, assets/p/); no GIFs.
Zombies play their death animation (head pops off); Cherry Bomb plays its explosion animation.
UI: own-style wooden seed bar (sun/brain counter, packets with recharge + unaffordable states, shovel for plants), "Choose your seeds" panel with Let's Rock!, tombstone-style main menu, progress bar.
Breaking: cones/buckets/football helmets crack in 3 stages and fall off; Newspaper Zombie goes berserk (fast) when its paper is torn.
Chomper: bite -> chew animation for ~29s -> swallow, cannot eat for 30s total.
Sounds: eating (chompsoft), hat hits/breaks, newspaper rip/rage, ready-set-plant at start, win (prize) / lose (scream + evil laugh) at the end.
Files: sprite parts are packed in assets/atlas.png (57 files total, under GitHub's 100-file browser upload limit). If the music/sounds don't play, a warning icon appears on the sound button: make sure the whole assets folder was uploaded.
Network: uses STUN + TURN relay servers (see the ICE list near the bottom of index.html) so players on different/strict networks can connect.
If joining ever still fails, put your own TURN servers in that list (free account at metered.ca gives you an iceServers list).
Join/Host now show clear errors (wrong code, server unreachable, blocked network) and time out instead of staying on "Connecting".
Squash: spots zombies on either side, looks, jumps in an arc and lands on them (animated), then disappears.
Snow Pea: slowed zombies turn blue, and animate/walk/bite at half speed.
Robustness: data files are cache-busted (anim.js?v=..., atlas.png?v=...); a drawing/logic error no longer freezes the game and shows a red error line at the bottom-left instead.
The lobby shows the version (bottom-left). If something looks broken after updating, press Ctrl+F5 once to load fresh files and check the version matches.
New units (from the supplied GIFs, converted to frame animations in assets/atlas2.webp - no GIFs are used at runtime):
 Garlic: a zombie takes one bite then swerves one lane up or down (top-lane zombies can only go down, bottom-lane only up).
 Spikeweed: zombies walk over it and take damage; only a Gargantuar smashes it.
 Tall-nut: very tough; Pole Vaulters cannot jump over it.
 Gargantuar (zombie, 350 brains): slow giant, smashes any plant in one hit (club lands ~1.7s into the swing); Chompers cannot eat it, Cherry Bomb/Squash only wound it.
Sounds: gargantuar_thump.mp3, gargantuar_death.mp3 (converted from the supplied .ogg files).
Mobile: works in landscape on phones/tablets (portrait shows a "rotate" prompt). Everything (menus, seed chooser, help, HUD) scales with the game stage.
 - Tap a seed packet, then tap a tile. Tap sun/brain pickups (larger tap area on touch screens). Shovel works by tap too.
 - Sound: the first tap unlocks audio (required by iOS/Android). Sound effects use WebAudio so they play reliably on phones.
 - Fullscreen button (top-right) on Android/iPad; on iPhone use Share > Add to Home Screen for a full-screen app (manifest + icons included).
 - The screen stays awake during a match where the browser allows it.
Connection: players now connect through an instant relay (public MQTT brokers over WebSocket, assets/mqtt.min.js) and the game upgrades to a direct WebRTC link (assets/peerjs.min.js) if one succeeds. Both libraries are bundled (no CDN needed).
Voice chat: Host Game and Join Game request microphone permission and start a private PeerJS/WebRTC audio call when the direct peer connection opens. Use the microphone button to mute/unmute yourself and the headphones button to mute/unmute incoming voice. If microphone permission is blocked, you can still listen. Voice stops automatically when the opponent leaves or the page closes. Microphone access requires HTTPS or localhost in modern browsers.
Balance: longer seed cooldowns (see the table in the chat message); heavy seeds (cooldown >= 9-14s) start half-charged.
Added (from new_zombies_and_plants.zip; frames extracted into assets/atlas2.webp, no GIFs at runtime):
 Grave Digger (plant, 75 sun, 16s): only on a gravestone; digs it up in 5s then disappears; zombies can eat it meanwhile; removed if its gravestone is destroyed.
 Hypno-shroom (plant, 100 sun, 24s): a zombie that bites it turns purple, faces right and fights enemy zombies in the same lane (Gargantuar is immune and just smashes it); plant weapons ignore hypnotized zombies.
 Imp (zombie, 25 brains, 3s): small, 10 hp, speed 0.3 (normal 0.2).
Modes (lobby): 
 - Versus (online): host plays Plants, joiner plays Zombies.
 - Co-op (online): pick "Co-op" above Host Game; both players plant together (shared sun and seed cooldowns) against computer zombies.
 - Single Player: play Plants (computer sends zombies) or Zombies (computer plants). Works offline.
Settings: round length only (1-15 minutes, saved in the browser). Online, the host's round length is used.
The computer players follow the same costs, cooldowns and rules as a human.
Performance (for weak devices):
 - Each character animation frame is composed once into a bitmap and reused (1 draw call per character instead of 15-30); the bitmap cache has a memory limit chosen from the device's RAM (20-56 MB).
 - Chilled/hypnotized tints are cached too (they used to be recomputed every frame).
 - Automatic frame pacing: if the device can't keep up, the game draws every 2nd/3rd frame while the game logic keeps full speed.
 - The seed bar/timer update ~9 times a second and only when something changed; the game-over screen is built once; sounds can't pile up; Crazy Dave's animation only runs while Help is open; Gargantuar frames are stored at 75% size.
New online modes (pick one in the lobby's mode menu before pressing Host Game; the joiner is placed automatically):
 - Plants vs Plants: both plant. Own planting zone (host cols 1-5, guest cols 5-9). Shooters fire toward the enemy; peas hit enemy plants (3x damage vs plants), Snow Pea chills enemy plants, Cherry Bomb/Squash/Chomper work on enemy plants. Each side has 3 goal nuts (1800 hp = 3x a Tall-nut): your nuts are green, the enemy's red. Destroy all 3 to win; at time-up the side with more nut health wins. Roster: Sunflower, Peashooter, Repeater, Snow Pea, Puff-shroom, Wall-nut, Tall-nut, Cherry Bomb, Squash, Chomper.
 - Zombies vs Zombies: both play zombies with their own brain bank, cooldowns and gravestones (own half). The host leads the purple zombies (full health/armor) from the left, the joiner the normal zombies from the right. Zombies fight when they meet; first zombie to cross the other side wins; at time-up the side whose zombie advanced farther wins.
 - Co-op: Zombies vs computer: both play zombies (shared brains) against computer plants (stronger than in single player).
Economy balance (v20261105a): sky sun falls every 10s (was 6s); sunflowers make sun every 11s (was 8s); zombies start with 150 brains (was 100).
 Measured with a perfect-clicking, no-spending simulation on equal tiles, income ratio zombies/plants went from 0.70/0.68/0.82/0.88 (at 60/120/180/300s) to about 1.01/0.96/1.14/1.22.
Imp: cost 40 brains (was 25), 7 hp (was 10), speed 0.27 (was 0.30), cooldown 7s (was 3s).
Computer players re-tuned so single player stays about as hard as before (computer plants get an income bonus because they also lost sky sun).
Tuning knobs for these numbers live in the ECO and AIC constants in index.html.

Boss Raid and complete supplied roster (v20261115boss)
------------------------------------------------------
- Added every one of the 49 plants in PvZ_Other_Character_Animations_Final.zip. The original optimized animations remain in use for plants already present; all newly added plants use their supplied rebuilt GIF animation. Repeater remains as an additional fiftieth plant.
- Added all 17 supplied additional zombie rigs: Screen Door, Flag, Dancing, Disco/Jackson, Balloon, Bobsled, Bungee, Catapult, Digger, Dolphin Rider, Jack-in-the-Box, Ladder, Pogo, Snorkel, Surprise, Yeti and Zomboni.
- Pool/roof-only characters were adapted to useful five-lane lawn abilities. Signature roles are preserved where the board supports them: Blover clears balloons, Magnet-shroom strips defenses, Ice-shroom freezes the field, Jalapeno clears a lane, Doom-shroom and Cob Cannon deliver heavy damage, Potato Mine arms before exploding, and jumping/vehicle/special zombies retain matching combat traits.
- The chooser scrolls and uses lightweight thumbnails; full supplied GIFs load only when their character appears on the lawn.

Boss Raid mode:
1. The host chooses "Boss Raid: unlimited players", presses Host Game, and shares the room code.
2. Any number of guests can enter that same code. Everyone first waits in the Boss Raid Lobby. When all expected players are connected, the host presses Start Match; only then does plant selection open for the whole group.
3. After plant selection, the fight starts only when the host and every connected guest are ready. Every player fights as Plants with shared sun, shared cooldowns and a shared lawn. There is no time limit and no coded player cap; practical limits depend on the host browser/network.
4. Zomboss health scales with the number of directly connected players present when the raid starts. Zomboss attacks rows, stomps the lawn and summons increasingly large mixed zombie waves.
5. Projectiles that reach Zomboss damage him. Cherry Bomb, Jalapeno, Doom-shroom, Potato Mine and Cob Cannon also inflict boss damage. The raid ends when Zomboss is destroyed or a zombie reaches the house.
6. The supplied Zomboss theme plays for the raid. Supplied boss attack/death animations and the complete miscellaneous sound-effect archive are included under assets/boss and assets/sfx.

Boss multiplayer uses one authoritative host and broadcasts game state to every open PeerJS data connection, with the existing MQTT relay retained as fallback. Late connections receive the current configuration/state. Group voice preserves the earlier microphone/headphone controls: the host can hear all directly connected guests, and each guest can hear the host. Browsers still require HTTPS or localhost for microphone permission.

Full animation/gameplay correction (v20261115full)
--------------------------------------------------
- Imported all 265 supplied plant and zombie GIF clips, not only one idle clip per character. assets/extra_anim.js records every clip, duration and loop flag; full files are under assets/animextra.
- Animation playback is tracked per placed entity outside the synchronized game state, so multiple copies can independently restart shooting, attack, eating, jumping, special and death clips without breaking network serialization.
- New plants now switch to their supplied shooting/special clips when firing or activating. One-use plants leave their activation animation on the lawn for the clip's supplied duration instead of disappearing before it can be seen.
- New zombies switch among supplied walking/driving, eating, special-attack and death clips. Bungee, Catapult, Digger, dancers, Jack-in-the-Box, Ladder/Dolphin/Pogo jumpers and vehicle units also use their matching special states.
- Completed adapted mechanics for all added plants: multi-row/rapid/splash/slow/fire projectiles, global and lane attacks, mines, field freeze, balloon clearing, armor removal, sun support, Torchwood ignition, Umbrella blocking, Cattail targeting, Imitater copying and defensive plants.
- Completed adapted mechanics for all added zombies: armor/toughness, dancers summoning backups, airborne plant bypass, Bungee stealing, ranged Catapult attacks, reverse Digger movement, jumping/ladder bypass, Jack-in-the-Box explosion and Zomboni crushing.
- A few supplied rigs contain only an idle/full clip (not separate action clips), notably Flag Pole, Surprise and Credits Screen Door. Those units use every animation present in the source pack; no nonexistent action artwork was fabricated.

Transparent projectile artwork (v20261115projectiles)
----------------------------------------------------
- Extracted transparent flight sprites from the supplied projectile sheet: pea, snow pea, mushroom spore, fire pea, cactus/cattail spike, star, cabbage, kernel, butter, melon, winter melon, cob and basketball.
- Every ranged plant now draws its matching projectile instead of the generic pea graphic. Torchwood visibly converts pea and snow-pea shots into the supplied fire-pea sprite.
- Kernel-pult sometimes throws butter; butter deals extra damage and briefly stops the hit zombie. Cob Cannon now launches a visible cob that travels across the lane and deals heavy splash/boss damage on impact.
- Catapult Zombie now launches the supplied basketball in a visible arc. Umbrella Leaf still blocks it at the target.
- The original sheet with its blue field removed, the individual transparent PNGs and a checkerboard preview are in assets/projectiles.

Character and Boss Raid repair (v20261115repair)
------------------------------------------------
- Rebuilt Gatling Pea, Split Pea and Threepeater from their separate body/head animation layers, so their heads stay attached during idle and shooting animations.
- Fire Pea now uses a complete orange Peashooter character animation; its supplied fireball artwork is used only for the projectile and its chooser icon is a complete plant.
- Rebuilt Zomboss as a layered full machine with head, pilot and complete legs. Attacks and stomps retain their supplied animation while spawn/death effects keep the complete body visible instead of showing disconnected GIF pieces.
- Enlarged and repositioned Zomboss so both feet remain visible. The boss health bar is now a top-layer interface element that cannot be covered by the lawn, units or boss art.
- Boss sound effects and legacy sounds are both preloaded/decoded, with a normal audio-element fallback. Boss music begins after the user's match-start interaction, satisfying browser audio rules.
- Boss hosting now has a dedicated waiting lobby and a host-only Start Match button. Plant selection is locked until the host starts it, and gameplay remains locked until every connected raid member is ready.

Full-size animated Zomboss GIF rebuild (v20261115bossgif)
---------------------------------------------------------
- Replaced the runtime collection of separately drawn body pieces with five finished transparent animated GIFs under assets/boss/full: idle, attack, stomp, spawn and death.
- The finished GIFs contain 62, 80, 62, 44 and 214 frames respectively. The game displays them as actual browser GIF elements, so their motion does not depend on canvas handling of separate GIF layers.
- Zomboss is now intentionally much larger: his head, pilot and shoulder fill the right half of the screen like the original roof-battle framing. The rest of the machine naturally continues below/right outside the camera instead of ending at a disconnected sprite edge.
- Corrected the attack GIF's large source-stage translation so the animated face and pilot remain in view at the new size.
- Idle is automatically restarted after each complete GIF cycle for reliable continuous movement across browsers. Every state was tested by comparing two rendered frames and confirmed to change on screen.

Imported plant/zombie animation runtime fix (v20261115frames)
------------------------------------------------------------
- Fixed the shared renderer that caused imported plant and zombie GIFs to remain on one browser-decoded frame when drawn into the game canvas.
- Converted all 265 supplied clips into transparent, game-sized static WebP frame sheets under assets/animframes. assets/extra_frames.js records each source GIF's frame count, original proportions, exact frame delays and sheet locations.
- The game now selects the correct frame itself using a monotonic clock. Looping idle/walk/eat clips repeat continuously, while shooting, attacks, jumps, special abilities and deaths restart per entity and stop on their final frame when appropriate.
- The fix covers every imported character through the shared renderer, including the separately layered Gatling Pea, Split Pea and Threepeater heads.
- Automated motion checks placed Cabbage-pult, Cactus, Melon-pult, Winter Melon, Dancing Zombie, Catapult Zombie, Digger Zombie and Zomboni on the lawn and confirmed thousands of changed pixels per character. Additional checks confirmed advancing shooting, eating, digging, death, Gatling, Split Pea and Threepeater clips.

Stable action-animation sizing (v20261115scale)
------------------------------------------------
- Fixed characters becoming smaller when they switched from idle/walk to shooting, eating or another action. Supplied clips use different canvas dimensions, so fitting each full action canvas into the same lawn box incorrectly changed the character's scale.
- Every action now uses its character's idle/walk artwork as a permanent scale reference and stays bottom-center aligned. Extra room in an action clip can extend around the character without shrinking it.
- The same reference-scale rule is applied independently to the body and head layers of Gatling Pea, Split Pea and Threepeater.
- Automated size checks compare idle/walk with shooting/eating for Cabbage-pult, Cactus, Dancing Zombie, Ladder Zombie, Gatling Pea, Split Pea and Threepeater. All retain their normal height while their supplied action frames continue to advance.

Game-style animation playback rebuild (v20261115native)
-------------------------------------------------------
- Added characters now warm all of their supplied idle, walking, shooting, eating, special and death frame sheets when selected or first encountered. An attack can no longer appear frozen or disappear while its next animation image is still loading.
- State changes preserve the last successfully drawn frame until the new sequence is ready, then restart the new sequence at its first frame. Looping idle/walk/eat sequences use stable per-character phase offsets so multiple copies move naturally instead of in perfect synchronization.
- The five source clips that contain only one actual frame (Coffee Bean twitch, Lily Pad idle, and three Potato Mine states) receive subtle procedural breathing/twitch motion; every multi-frame source clip continues to use its original supplied frames and timing.
- Zomboss no longer depends on browser GIF playback. All 457 frames across idle, attack, stomp, spawn and death were converted into 26 timed frame sheets and are drawn by the main game renderer, behind the units and below the boss health interface.
- Full validation loads every one of the 265 supplied character clips and all five complete boss sequences. It verifies that every multi-frame clip contains changing rendered frames, that none is wholly blank, and that all boss states visibly advance in the actual game canvas.

Video-matched Zomboss battle (v20261116bossfight)
--------------------------------------------------
- Rebuilt the Boss Raid attack loop from the supplied Dr. Zomboss fight video: Zomboss alternates mouth attacks, zombie waves, a warned stomp, another mouth attack, another wave and an RV crush. The cycle becomes faster as his health falls.
- Added transparent fireball, cracked fireball, iceball, cracked iceball and RV artwork extracted from the supplied Dr. Zomboss Attacks sheet. Fire and ice balls visibly leave his mouth, travel down a chosen lane and destroy plants they reach.
- Ice-shroom counters an incoming fireball. Jalapeno counters an incoming iceball when planted in the same lane. A successful counter freezes and exposes Zomboss and deals bonus damage.
- Zomboss is armored while upright and takes only chip damage. His attack window, freeze window and counter window make him vulnerable to full damage, matching the protected/lowered-head rhythm of the original fight.
- Stomp and RV attacks display a target warning before crushing the selected part of the lawn. Zombie summoning waves grow with the boss's rage phase.
- Boss status is always shown in the top health interface as ARMORED, VULNERABLE or FROZEN. The fight keeps its no-time-limit multiplayer lobby, host-only Start Match button and post-start plant selection.
- Automated checks cover all six attack-cycle steps, armor/vulnerability damage, fire/ice counters, lane destruction, RV/stomp impacts, attack-asset transparency and dimensions, all 265 imported character clips and every Zomboss animation state.

Authentic boss and plant mechanics (v20261116authentic)
-------------------------------------------------------
- Boss Raid now uses a purple tiled roof with flower pots and the five plants from the original Zomboss battle: Cabbage-pult, Kernel-pult, Ice-shroom, Jalapeno and Melon-pult. Raid cards cost no sun but retain recharge timing.
- Zomboss is completely protected while his head is raised. He becomes vulnerable while lowering his head for a mouth attack. Fireballs move slowly down a full row and are countered by Ice-shroom; iceballs require a Jalapeno in the same row.
- The boss cycle includes escalating roof-compatible zombie waves, fireball and iceball attacks, a warned 2-column by 4-row stomp, and a warned 2-column by 3-row RV impact. His attack rate increases as health falls. The attack warning, counter hint and health status remain above the action.
- Mushrooms sleep on the daytime lawn and Coffee Bean now wakes the mushroom on its tile. Sun-shroom produces small sun before growing; Scaredy-shroom hides from nearby zombies; Fume-shroom pierces groups; Gloom-shroom attacks three rows.
- Split Pea fires one pea forward and two backward. Starfruit fires in five directions. Cattail requires a Lily Pad, fires two homing spikes and prioritizes Balloon Zombies. Cactus spikes pop Balloon Zombies. Winter Melon's splash chills every affected zombie.
- Pumpkin and Lily Pad are real same-tile layers. Zombies attack Pumpkin before the protected plant. The shovel removes the upper layer first.
- Upgrade plants require their real bases: Repeater to Gatling Pea, Sunflower to Twin Sunflower, Fume-shroom to Gloom-shroom, Magnet-shroom to Gold Magnet, Spikeweed to Spikerock and Melon-pult to Winter Melon. Cob Cannon requires two adjacent Kernel-pults.
- Cob Cannon no longer fires automatically: click a ready cannon, then click its impact tile. Doom-shroom leaves a timed crater. Marigold creates coins and Gold Magnet collects them. Magnet-shroom removes metal equipment. Lobbed shots bypass front shields, Jalapeno clears its complete lane and Spikerock/Spikeweed correctly damage Zomboni tires.
- The in-game Help pages explain the corrected mushroom, upgrade and boss-counter rules.
- The authentic gameplay test covers upgrades, layers, targeted Cob Cannon, Doom crater, mushrooms, multi-direction shots, coins, magnetism, balloon popping, elemental boss counters, full boss phases and exact crush footprints.
