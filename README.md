# Interstellar War

**One officer. One hundred mechs.**

A third-person browser shooter built with Three.js. You play as the Robot Police
unit **RX-9 Peacekeeper**, dropped alone onto a scorched alien plain while an
enemy mothership hangs in the sky and deploys 100 Pelter artillery mechs to
crush you. Overhead, fighter squadrons dogfight the whole time.

## Play

Open `index.html` through any static web server. It loads models from `assets/`,
so double-clicking the file won't work in most browsers.

```bash
# from the repo folder
python3 -m http.server 8000
# then open http://localhost:8000
```

It also works on **GitHub Pages**: Settings → Pages → Deploy from branch → `main` / root.

## Controls

| Action | Keyboard / mouse | Touch |
|---|---|---|
| Move | WASD | Left stick |
| Look | Mouse (click to lock) or Arrow keys | Drag right side |
| Fire plasma rifle | Left click, F, J, or Enter | FIRE |
| Justice Lance (hold to charge, release to fire) | Right click, G, or K | LANCE |
| Jump / hold for jet | Space | JUMP |
| Dash | Shift | DASH |
| EMP Nova (damages + stuns nearby mechs) | Q | EMP |
| Riot Overdrive (charged by kills) | E | RIOT |
| Auto-fire toggle | T | — |
| Pause | P / Esc | — |

Aim assist is on, and stronger when you aren't using a locked mouse, so it's playable
with keyboard only or touch.

## Gameplay

100 mechs arrive in drop waves. Each drop is fired from the mothership as a
burning streak, marked on the ground and radar, and lands with a shockwave.
Destroyed mechs sometimes leave green **repair cores**.

| Mech | Count | Role | Attacks |
|---|---|---|---|
| Pelter | 35 | Artillery | MG bursts, twin cannons, lobbed mortars (red ring = impact) |
| Haze Skirmisher | 22 | Fast flanker | 3-round rifle bursts, purple plasma caster |
| M-6K Blade | 18 | Melee | Sci-fi sword slashes and long lunges (triangles on radar) |
| Riot Bruiser | 12 | Heavy | Arm cannon, homing rocket salvos (dash to shake them) |
| Gatling Warden | 12 | Tank | Spin-up gatling stream, cannon |
| **The Heartblade** | 1 | **Final boss** | Legless; hovers on a bottom thruster with a red Iris Heart sword |

Heavier mechs unlock as the fight goes on.

### Damage you can see

Every mech's armor is real geometry split into plates. Shots tear the plate
nearest the hit right off the model. It flies away as a physical piece, and the
hole it leaves shows packed internal wiring (`assets/wires_cavity.webp`). Broken
wire strands (`assets/wire_*.webp`) hang out of each hole, swing as the mech
moves, and arc with sparks at their tips. Severed limbs show wiring at both ends
of the break. Badly damaged mechs smoke,
and below 30% health the new walkers limp. When a walker dies, its limbs blow
off and the rest of it collapses.

### Your shield and hull

Your robot has a **shield** (blue bar) over its **armor** (red bar). Each shot the
shield blocks lights up a hex-patterned energy shell, with a ripple spreading from
the point of impact. When the shield breaks, it shatters into shards. It recharges
three seconds after you stop taking damage and pulses when it's full again.

Damage that gets through to your hull uses the same plate system as the mechs:
pieces of your robot are torn off, leaving wired holes with sparking strands.
Picking up a repair core welds lost plates back on.

### Bullets

Machine guns, the Haze rifle, the Gatling and the Riot arm gun fire physical
rounds: glowing slugs you can see in flight. Each shot ejects a brass casing
that bounces and clinks on the ground. Rounds kick up dirt where they land,
spark off rocks, and whizz audibly when they pass close to you.

### How the new mechs move

The four new mechs and the boss ship as static models, so the game cuts each one
into jointed parts at load time: pelvis, torso, head, upper and lower arms,
thighs, shins and feet. Legs use two-bone IK with foot planting, so feet step
and stay put instead of sliding. Arms aim and recoil, torsos twist toward you,
and every melee swing runs on an eased keyframe timeline.

### The Heartblade

The final boss is a legless mech that hovers on a thruster and carries a red Iris
Heart sword. It has three phases. Each phase change sets off a roar that blasts
armor off it and makes its sword grow.

| Attack | Phase | How to survive it |
|---|---|---|
| Chained dash-slashes (2, then 3) | 1+ | A red line marks each path. Dash sideways. |
| Crimson Cyclone (spinning blade that pulls you in) | 1+ | Run or dash away from it. |
| Sword waves that skim the ground | 1+ | Jump over them. |
| Meteor Slam, followed by 2–3 shockwave rings | 2+ | Get out of the red ring, then jump each ring. |
| Heartstorm (spectral swords orbit, then launch) | 2+ | Keep moving. They explode where they land. |
| Judgement (sky beam, then a sweeping ground beam) | 3 | Jump the beam as it passes. |
| Blink Strike (teleports behind you) | 3 | Watch for the ring behind you, then dash. |

In phase 3 it also summons three M-6K Blades.

## Graphics settings

Low / Medium / High / Ultra on the title screen. The game also lowers its render
resolution on its own if the frame rate drops.

## Assets

The original Sketchfab models are kept at the repo root. The game uses compressed
copies in `assets/` (meshopt geometry plus WebP textures, about 7 MB instead of 262 MB),
made with [glTF-Transform](https://gltf-transform.dev):

```bash
npx gltf-transform optimize robot_police_unit_animated.glb assets/robot.glb --compress meshopt --texture-compress webp --texture-size 2048 --simplify false
npx gltf-transform optimize pelter_-_artillery_mech.glb assets/pelter.glb --compress meshopt --texture-compress webp --texture-size 1024 --simplify false
npx gltf-transform optimize light_fighter_spaceship_-_free_-.glb assets/fighter.glb --compress meshopt --texture-compress webp --texture-size 512 --simplify-ratio 0.15 --simplify-error 0.01
npx gltf-transform optimize mothership_platypus.glb assets/mothership.glb --compress meshopt --texture-compress webp --texture-size 1024 --simplify-ratio 0.25 --simplify-error 0.005
```

Check each model's Sketchfab page for its license and credit its author if you
publish the game.
