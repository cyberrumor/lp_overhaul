# lpo

[Nexus Mirror](https://www.nexusmods.com/skyrimspecialedition/mods/136870)
[Github Mirror](https://github.com/cyberrumor/lpo)

## Requirements

- [SKSE](https://skse.silverlock.org/)
- [Address Library for SKSE Plugins](https://www.nexusmods.com/skyrimspecialedition/mods/32444)
- [powerofthree's tweaks](https://www.nexusmods.com/skyrimspecialedition/mods/51073)
- [Community Shaders](https://www.nexusmods.com/skyrimspecialedition/mods/86492)
- [Light Limit Fix](https://www.nexusmods.com/skyrimspecialedition/mods/99548)
- [Light Placer](https://www.nexusmods.com/skyrimspecialedition/mods/127557)

## What Does LPO Add Light To?

You can install the CLI tool `jq` and run this command to generate this list:

Windows:
```
type Data\lightplacer\lpo\* | jq '.[].models' | sort /unique
```

Linux:
```
cat Data/lightplacer/lpo/* | jq '.[].models' | sort | uniq
```

## Further Reading

* [Light Placer Wiki](https://github.com/powerof3/LightPlacer/wiki)
* [Community Shaders Wiki](
    https://github.com/doodlum/skyrim-community-shaders/wiki
  )

## Thanks

Thanks a bunch to powerofthree for making Light Placer so I could write configs
for it. It's been fun to work with.

