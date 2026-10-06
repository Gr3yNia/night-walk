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

1. Build the basic lantern screen from the layout reference: a dark full-screen canvas, a warm soft glow sitting below the middle, and small “tap to start” text near the bottom. Keep the glow static for now. On both laptop and phone, I should see the basic lantern layout before adding motion.

2. Add the phone start interaction and motion sensor permission using the p5-phone functions provided by the project skills. After tapping to start on the phone, motion data should become available. On the laptop, keep the static fallback.

3. Read phone movement and reduce it to one movement value that can distinguish walking from being still. Put any movement threshold as a named value at the top of sketch.js so it can be adjusted. On the phone, walking should register as movement and standing still should register as still.

4. Connect the movement value to the lantern. While walking, make the glow brighter and slightly bigger. When movement stops, make it fade gradually toward almost dark. Put the brightness, size and fade values at the top of sketch.js so they can be adjusted.

5. Check the final behaviour on the phone while walking and stopping. Adjust only the named values if necessary so the lantern responds clearly without flickering between walking and still.

## Assumptions

- Each phone works independently.
- The person holds the phone with the screen facing outward.
- The phone provides motion sensor data after the person gives permission.
- The visual should follow the layout reference more closely than the mood reference.

## Changes
