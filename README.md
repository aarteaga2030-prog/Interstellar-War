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

- 100 mechs arrive in drop waves. Each drop is fired from the mothership as a
  burning streak, marked on the ground and on radar, and lands with a shockwave.
- Pelters fight with machine-gun bursts, twin cannons, and lobbed artillery
  (a red ring shows where it will hit).
- Destroyed mechs sometimes leave green **repair cores**.
- The 100th mech is a **Pelter Titan**.

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
