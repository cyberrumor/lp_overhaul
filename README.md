# lp_overhaul

## Features

- Remove all fakes lights from the game.
- Add lights to light emitters with precise offsets.


## Planned Features

- Add window glow
- Add atronach glow
- Make glowing mushrooms / chaurus eggs / Nirnroot stop emitting light when you pick them
- Add enchanting and alchemy tables
- Add torchbugs
- DLC support (I haven't gone through and checked Dragonborn locations yet)


## Glossary (yes I am pedantic)

- Light - The energy that your eyes use to provide the sense of sight.
- LIGHT - Game objects with the form type LIGH. These game objects produce light.
- Emitter - Something that should be casting light, e.g. fires, candles, embers, torches, etc.
- Particle light - A type of light injected into the game by Community Shaders. These don't contribute to the light limit and aren't occluded by walls.
- Fake LIGHT - LIGHT without an associated emitter. E.g. "Why is this table so bright?! There's no candles anywhere!"

## Description

LP Overhaul sets `bDisableAllGameLights` in `Data/SKSE/Plugins/po3_LightPlacer.ini`, and places new LIGHTS only where it makes sense to. This is achieved pragmatically, which guarantees you'll never see a fake LIGHT again (regardless of your load order) and makes light only come from places it should.

## What sets LP Overhaul apart from mods like Relighting Skyrim and Placed Lights?

A narrow scope, and an indiscriminate, surgical precision when re-adding LIGHTS. LP Overhaul does not add, change, move, or remove any emitters, period. LP Overhaul's focus is on correct LIGHT placement, sensible LIGHT brightness/radius for a particular emitter, and a narrow color spectrum so that reshade/vkbasalt presets are represented consistently from one interior to another.

## Design Decisions

I decided to set all lights produced by fire to the same color: LightCampFire01. This saturate and warm light will breathe life into your interiors. Using the same light for all fire-based  emitters gives a sort of monochromatic/noir atmosphere, reinforcing the fantasy genre while still playing along the edges of realism.

Until Light Limit Fix unlocks support for any number of shadow casting lights, most lights do not cast shadows. Some do, but I can only do this for models which I know are only used in a select few locations (E.g. only two magic pillars in the College of Winterhold). For example, making all embers cast shadows might be fine in Bleak Falls Barrow, but it would have crazy flickering problems in Dragonsreach kitchen. Therefore shadow casting lights are currently few.

You may ask why I'm not just replacing lights for embers and campfires, then leaving candles and such to the responsibility of particle lights. The reason is occlusion. Particle lights aren't occluded by walls or other objects, so if you try to fill a room with a particle light, you'll end up with light bleeding into adjoined rooms. You can most easily witness this behind Farengar's enchanting table (if you make his enchanting table candles glow with particle lights, they'll shine through the wall). This doesn't happen with lights placed by Light Placer.


## Compatibility

- Compatible and recommended to be used with lighting template mods like [Standard Lighting Templates](https://www.nexusmods.com/skyrimspecialedition/mods/66943) or [KreatE](https://www.nexusmods.com/skyrimspecialedition/mods/83757)
- Not intended for use with particle lights on candles or fire. It should be fine to put particle lights on other emitters. Just don't use particle lights as a primary light source, or you'll have issues with occlusion. You might be able to get away with low radius particle lights on candles/embers though.
- Not intended for use with other Light Placer overhauls like [Placed Light](https://www.nexusmods.com/skyrimspecialedition/mods/135488). I haven't tested but I assume Light Placer would add more lights per mesh than Placed Light or LP Overhaul intended.
- Mods that add new emitter meshes to the game require Light Placer configs for those meshes, or they won't produce light.


## Requirements

- [SKSE](https://skse.silverlock.org/)
- [Address Library for SKSE Plugins](https://www.nexusmods.com/skyrimspecialedition/mods/32444)
- [Community Shaders](https://www.nexusmods.com/skyrimspecialedition/mods/86492)
- [Light Limit Fix](https://www.nexusmods.com/skyrimspecialedition/mods/99548)
- [Light Placer](https://www.nexusmods.com/skyrimspecialedition/mods/127557)
