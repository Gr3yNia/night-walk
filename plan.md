# Plan: Night Walk Lantern

## Project

Phone as a lantern, to glow while walking and fade when stopping, for people walking together in the dark.

## The question

This prototype tests whether phone movement can make the lantern feel responsive while walking. It works if the glow becomes brighter while I walk and fades when I stop.

## The experience

One person holds the phone while walking, with the screen facing outward so people around them can see the glow. The lantern becomes brighter and slightly bigger while the person walks. When they stop, the glow slowly fades almost to black. Each phone works on its own.

## Input, transformation, output, fallback

- Input: Movement from the phone.
- Transformation: Movement makes the glow brighter and slightly bigger. When movement stops, the glow slowly fades.
- Output: A warm, soft glow on the phone screen.
- Fallback: On a laptop without phone movement, show the lantern layout so the visual can still be checked.

## References

| File | Use it as | Take | Leave |
|---|---|---|---|
| references/night-walk-layout.jpg | layout: match this | glow sits low on the screen, small text near the bottom, soft edges | handwritten drawing style |
| references/mood-night-lanterns.jpg | inspiration: the feel | warm colour, soft blurred light, dark atmosphere | multiple lights and background scene |

## Limits

- Change only sketch.js.
- Not now: phones communicating with each other, sound, or additional interactions.

## How I will check it

- On my laptop: I should see the dark screen, lantern glow and basic layout.
- On my phone: the glow should become brighter and slightly bigger while I walk, then slowly fade when I stop.

## Steps

1. Build the basic lantern screen from the layout reference: a dark full-screen canvas (`createCanvas(windowWidth, windowHeight)` plus `windowResized()`), a warm soft glow sitting below the middle with soft fading edges (layered ellipses with decreasing alpha), and small “tap to start” text near the bottom. Keep the glow static for now. On both laptop and phone, I should see the basic lantern layout before adding motion.

2. Add the phone start interaction and motion sensor permission with the p5-phone functions: `lockGestures()` in `setup()`, then `enableSensorTap('Tap to start')` only on mobile (`window.isMobile`), so no permission overlay is left waiting on the laptop. Gate all later motion reads on `window.sensorsEnabled`, add `mousePressed() { return false; }`, and hide the “tap to start” text once the sensors are on, since the layout says it shows only before start. On the laptop, keep the static lantern with no overlay.

3. Keep the screen on while walking, because only touches reset the phone's auto-lock timer and a motion sketch goes dark after about 30 seconds. Request a Screen Wake Lock from `mouseReleased()` (iOS refuses the first request without a finished tap), wrap the request in try/catch, and ask again on `visibilitychange` when the page comes back. On the phone, the screen should stay awake while the lantern runs; on the laptop nothing changes.

4. Read phone movement and show it: read the p5 globals `rotationX/Y/Z` and `accelerationX/Y/Z` (there is no `rotationRate*` in p5 — reading it throws every frame), use `angleMode(DEGREES)`, and display the raw value as small text or through `showDebug()` / `debug()` so it can be checked on the phone, only when `window.sensorsEnabled` is true. On the phone, tilting or walking should change the number on screen; on the laptop, the static lantern.

5. Reduce the raw reading to one smoothed movement value and a walking/still state, so walking and standing still are told apart without flickering: smooth over several frames, and use two named thresholds — one to switch to walking, a lower one to switch back to still. Put both thresholds and the smoothing amount at the top of sketch.js. On the phone, walking shows “walking”, standing still shows “still”, and the state does not flicker between them.

6. Connect the movement value to the lantern. While walking, make the glow brighter and slightly bigger. When movement stops, fade it toward almost dark over about 5 seconds, and when movement starts again, bring it back in about 1 second, timing the fade with `millis()` so the seconds are real. Put the brightness, size, and both fade times at the top of sketch.js as named values. On the phone, the glow rises while I walk and sinks slowly when I stop; on the laptop, the static lantern.

7. Check the final behaviour on the phone while walking and stopping. Adjust only the named values at the top of sketch.js if necessary, so the lantern responds clearly without flickering between walking and still. If something needs new code rather than new numbers, stop and tell me instead.

## Assumptions

- Each phone works independently.
- The person holds the phone with the screen facing outward.
- The phone provides motion sensor data after the person gives permission.
- The visual should follow the layout reference more closely than the mood reference.

## Changes
