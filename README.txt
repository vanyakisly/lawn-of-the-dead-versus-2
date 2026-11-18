The Lawn of the Dead VERSUS - v20261118T

VERSION T EXPANDED GAME MODES
- Added Sun Shower: rapid falling sun and a stronger plant opening economy.
- Added Hyper Battle: a two-minute match with triple income and much faster recharge timers.
- Added Mini Mayhem: only inexpensive units are available, with faster resources and recharge.
- Added Heavy Hitters: only high-cost plants and zombies are available, with larger starting resources and boosted income.
- Added Random Arsenal: each side receives a locked, deterministic five-character loadout based on the room code.
- Added One-Lane Clash: only the middle lane is playable; the other lanes are visibly shaded.
- Added Nut Fortress: the plant side starts with a full defensive row of Wall-nuts while zombies receive extra brains.
- Added Graveyard Rush: the lawn starts with three active Gravestones that generate brains for the zombie side.
- Added Ten-Wave Last Stand for 3+ players: the team must defeat ten increasingly large waves with no match timer.
- Added Creative Garden for 3+ players: no timer, no computer opponent, unlimited sun, and no plant recharge delays.
- Organized the mode selector into Classic, Challenge, and 3+ Player sections, with explanations for every new ruleset in Help.

VERSION S DARK GREEN WAVE MENU
- Replaced the main menu lawn photograph with a fully opaque layered dark-green background.
- Added softly animated contour waves and emerald/cyan lighting drawn by a lightweight canvas effect.
- Moving the pointer bends nearby waves, adds a following glow, and leaves expanding elliptical ripples along the mouse trail; clicking creates a stronger ripple.
- The menu effect pauses while gameplay is visible, uses no new image files, and respects the device's reduced-motion preference.

VERSION R COUNTER AND PLANTING FIX
- Fixed the sun and brain HUD counter, which retained the correct game value internally but stopped writing it to the screen in Version Q.
- The counter now follows the correct resource pool for the host, guest, and both teams in mirrored modes, including shared group-mode resources.
- Added a synchronized 0.62-second planting animation to every plant: it rises from a soil ring, stretches slightly, and settles at its normal size.
- Planting remains immediately functional and keeps the original cost, recharge, health, attack timing, and online synchronization.

VERSION Q GROUP MODES
- Plants vs Plants and Zombies vs Zombies no longer have a time limit. Plants win by destroying all three enemy Tall-nuts; zombies win by reaching the opposite side.
- Added Garden Party for 3 or more plant players: share a garden, resources, and recharge timers while surviving increasingly large endless waves.
- Added Zombie Siege for 3 or more zombie players: coordinate different zombie loadouts against a faster, fortified computer-controlled garden before the selected round time ends.
- Added Last Lawn Standing for 3 or more players: the host is the lone plant defender and every joining player is on the zombie team.
- Added a host-controlled group lobby showing the room code and live player count. Group loadout selection unlocks at 3 players, and the match begins only after everyone is ready.
- Group rooms broadcast the authoritative game state to every directly connected player and support players disconnecting from the lobby without breaking the room.

VERSION P COOLER, SMOOTHER UI
- Added a floating animated brand emblem with a soft rotating halo and layered aurora lighting on the title screen.
- Added subtle pointer parallax between the title and menu, with a smooth return to center when the pointer leaves.
- Added staggered menu, picker, seed-card, and modal entrances plus richer hover, press-ripple, focus, and selection feedback.
- Polished the corner controls and resource display with gentle glow and pulse motion.
- Kept the Version O fast-loading system and every gameplay rule unchanged. The motion also respects reduced-motion device settings.

VERSION O FAST LOADING
- Added state-by-state priority loading: a character now downloads only the animation it is currently using instead of every idle, attack, eating, special, and death sheet at once.
- Added instant icon/silhouette fallbacks so newly spawned plants and zombies remain visible while their first animation sheet finishes decoding.
- The overeating sprite sheets now load only when that rare death occurs, with the next sheet prefetched during playback.
- PeerJS and MQTT multiplayer libraries now load only when Host or Join is pressed, and the large lawn music waits for the selected character sheets before using bandwidth.
- Changed music to streaming playback instead of asking the browser to preload the full track.
- Sound effects now load and decode when first used instead of opening dozens of audio downloads on the title screen.

VERSION N REBRAND
- Renamed the game to The Lawn of the Dead VERSUS in the title screen, browser tab, and installable app metadata.
- Added a new original leaf-and-undead-hand app icon designed to match the dark emerald glass interface.
- Added refreshed 192px and 512px icons for browser, mobile home-screen, and installed-app use.

VERSION M UI REFRESH
- Rebuilt the menus, settings, seed picker, and in-game controls with a clean glass-and-garden visual style.
- Added smooth panel entrances, button hover/press feedback, animated highlights, and clearer focus states.
- Kept every PvZ plant, zombie, projectile, lawn sprite, and gameplay rule unchanged.
- Added reduced-motion support for players who disable interface animations in their device settings.

FIXED IN L
- The overeating death now uses five transparent sprite sheets containing all 149 supplied frames. Frame selection is driven by the game timer, so the animation advances correctly instead of sticking on frame one.
- The animation is foot-anchored and scaled to 47% of its source size. Its standing character is about 135 pixels tall, matching the regular Zombie instead of growing to about 154 pixels.

NEW IN K
- A basic regular Zombie that continuously eats the same Wall-nut or Tall-nut for 20 seconds now dies from overeating and plays the supplied 149-frame transparent "zombie eaten too much" GIF once for 9.48 seconds.
- The 20-second overeating timer is tracked separately for each regular Zombie and resets if it stops chewing, is stunned or hypnotized, fights another zombie, changes targets, or starts eating a different plant. Other zombie types are unaffected.

NEW IN J
- Yeti Zombie now moves at 0.72 lawn units per second, over twice its previous 0.34 speed. Its retreat uses the same faster speed.
- Zomboni is fully immune to freezing and slowing from Snow Pea, Winter Melon, and Ice-shroom, while still taking their damage.
- Screen Door Zombie now uses the regular Zombie body-and-head death animation instead of holding its idle frame.
- Cabbage-pult, Kernel-pult, Melon-pult, Winter Melon, and Cob Cannon throwing animations play 2.4x faster. Their damage and firing cooldowns are unchanged.

NEW IN I
- Flag Zombie has been removed from zombie selection, random waves, scripted waves, and Sandbox.
- Surprise Zombie can no longer reveal as Flag Zombie or Bungee Zombie (the plant-stealing zombie).
- Added Single Player Sandbox. Choose any available plant or zombie from the two dropdowns. Plants can be placed on the left half of the lawn; zombies spawn from the right side in the chosen row. Sandbox has no timer, no computer player, no resource costs, no recharge delays, and a Clear Lawn button.

FIXES IN H
- Most added zombies now have the same 20 health as a regular Zombie. Screen Door and Ladder retain 40 health for their equipment, Zomboni retains 60, Surprise keeps its five-hit disguise, and Disco Zombie has exactly 30 health (1.5x a regular Zombie).
- Yeti Zombie is invulnerable to projectiles, explosions, crushing, Chomper and Tangle Kelp. It eats one plant, turns around, retreats off the right side of the lawn, and disappears without a death animation.

EARLIER FIXES
- Rebalanced every added zombie's health. They previously required as many as 160 normal pea hits and appeared immortal. Added zombies now require 10–50 pea hits depending on their role: light units die quickly, while Catapult, Yeti and Zomboni remain progressively tougher.
- Surprise Zombie now moves slowly, shows its disguise health bar before being revealed, and its 10 disguise health takes exactly five normal 2-damage pea hits to break. When the disguise breaks it becomes one random zombie from Imp through Yeti, excluding another Surprise Zombie.
- Split Pea's two heads and Threepeater's three heads now share the body animation phase, keeping every head attached and synchronized during idle and shooting animations.
- Peashooter Single has been removed from all seed-selection pools and can no longer be planted. Its unused artwork is excluded from this ZIP.
- Regular Dancing Zombies never summon other zombies. Only a Disco Zombie summons two Dancing Zombies. After the final Dancing Zombie dies, the Disco waits exactly 3 seconds. It continues walking for 2.5 seconds, stops and performs its summon animation for the final 0.5 seconds, then creates exactly two replacements.
- Gatling Pea fires four separate peas in a short staggered burst. All four projectiles move and deal damage independently.

Boss Raid has been removed. This build uses the original day lawn and the existing playable plant/zombie animation system.

NEW ONLINE MODES
- Endless Horde (co-op): both players are plants, there is no timer, and a larger special wave arrives every 45 seconds while the AI steadily becomes faster and stronger.
- Blitz Versus: host plays plants, joiner plays zombies, the match is locked to 2 minutes, both sides start with 300 resources, zombie income is doubled, sun falls faster, and seed/zombie recharges are 80% faster.
- Mystery Seeds Duel: both players are plants and receive the same five room-code-randomized seeds. Each player defends three Tall-nut goals and wins by destroying the opponent's three goals.

The original Plants vs Zombies, plant co-op, zombie co-op, Plants vs Plants, Zombies vs Zombies, and single-player modes are still available.

Online rooms use peer-to-peer connections through PeerJS plus the existing fallback relay.
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

Complete supplied roster (v20261115)
------------------------------------
- Added every one of the 49 plants in PvZ_Other_Character_Animations_Final.zip. The original optimized animations remain in use for plants already present; all newly added plants use their supplied rebuilt GIF animation. Repeater remains as an additional fiftieth plant.
- Added all 17 supplied additional zombie rigs: Screen Door, Flag, Dancing, Disco/Jackson, Balloon, Bobsled, Bungee, Catapult, Digger, Dolphin Rider, Jack-in-the-Box, Ladder, Pogo, Snorkel, Surprise, Yeti and Zomboni.
- Characters from other original stages were adapted to useful five-lane lawn abilities. Signature roles are preserved where the board supports them: Blover clears balloons, Magnet-shroom strips defenses, Ice-shroom freezes the field, Jalapeno clears a lane, Doom-shroom and Cob Cannon deliver heavy damage, Potato Mine arms before exploding, and jumping/vehicle/special zombies retain matching combat traits.
- The chooser scrolls and uses lightweight thumbnails; full supplied GIFs load only when their character appears on the lawn.

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
- Kernel-pult sometimes throws butter; butter deals extra damage and briefly stops the hit zombie. Cob Cannon now launches a visible cob that travels across the lane and deals heavy splash damage on impact.
- Catapult Zombie now launches the supplied basketball in a visible arc. Umbrella Leaf still blocks it at the target.
- The original sheet with its blue field removed, the individual transparent PNGs and a checkerboard preview are in assets/projectiles.

Character repair (v20261115repair)
----------------------------------
- Rebuilt Gatling Pea, Split Pea and Threepeater from their separate body/head animation layers, so their heads stay attached during idle and shooting animations.
- Fire Pea now uses a complete orange Peashooter character animation; its supplied fireball artwork is used only for the projectile and its chooser icon is a complete plant.
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
