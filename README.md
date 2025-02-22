# lp_overhaul

[Nexus Mirror](https://www.nexusmods.com/skyrimspecialedition/mods/136870)
[Github Mirror](https://github.com/cyberrumor/lp_overhaul)

This document explains the reasons I made LPO, the problems it tries to solve,
how it differs in implementation from conventional lighting mods, why you might
want to whitelist or avoid whitelisting, and finally, provides a list of all
models that LPO attaches lights to.

This document is intended to be consumed by LPO users who want to know more
about the motivations of this mod, and who want to understand how it works so
they can make informed decisions about how to further customize their Light
Placer configs.

It does not cover the syntax or options available to the configs. For that,
refer to [official Light Placer documentation](
    https://github.com/powerof3/LightPlacer/wiki
).

Readers are expected to have at least the following prior knowledge:
* Opened xEdit (aka SSEEdit) at least once before.
* Opened the Creation Kit before.
* Used mod organizers to install mods before.
* Navigated to the Data directory via a file explorer before.

## Requirements

- [SKSE](https://skse.silverlock.org/)
- [Address Library for SKSE Plugins](https://www.nexusmods.com/skyrimspecialedition/mods/32444)
- [Community Shaders](https://www.nexusmods.com/skyrimspecialedition/mods/86492)
- [Light Limit Fix](https://www.nexusmods.com/skyrimspecialedition/mods/99548)
- [Light Placer](https://www.nexusmods.com/skyrimspecialedition/mods/127557)

## Mission Statement

LP Overhaul, or just LPO (short for Light Placer Overhaul) provides config files
which are consumed by Light Placer and Base Object Swapper. The configs are
intended to cause light sources which should provide illumination rather than
just FX actually produce light. This means LPO will cause Light Placer to attach
lights to things like fires, candles, and windows; but not things like glow
dust, eyes of draugr, etc.

I made this mod because I was excited about the release of Light Placer because
of how it could solve the problems that conventional (by which I mean
plugin-based) lighting overhauls can't.

Conventional lighting overhauls have these limitations:
* Lights must be hand placed via the Creation Kit, which is time consuming.
* Lights are only dynamic (by which I mean you can turn them on and off)
  when controlled via papyrus scripts.
* Skyrim is full of fake lights. They must either be manually disabled via
  the Creation Kit, light sources manually added via the Creation Kit so the
  light isn't fake anymore, or ignored.
* Placing objects like lights via a plugin causes cell records to be carried
  forward, which can cause compatibility issues.

The thing I'm most excited about is how Light Placer allows us to eliminate all
lights in the game that aren't placed by Light Placer via a simple ini setting.
Then, all LPO needs to do is add lights back to meshes that should produce
illumination. The result is a game with no fake lights.

The next thing I'm excited about is the support for Dynamic Lights. Once upon a
time, before Light Placer existed, I tried to write a Base Object Swapper config
that would replace all permanent torch sconces with the kind you can interact
with. To my dismay, adding a lit torch to the sconce didn't produce light! I
popped open the Creation Kit to discover that every single torch sconce in the
game has a manually placed light next to it, and a script attached to the torch
sconce to toggle the light. Disgusting.

With Light Placer, you can simply attach a light to the torch, disable all game
lights, and you're on your way.

This should also work for things like blowing out candles.

Writing LPO has allowed me to include an updated version of Eternal Flames (adds
blue fire to nordic dungeons) which utilizes Light Placer. This version is free
of the fake lights from the vanilla game which plagued the original.


## How Stuff Works

### Convention Mods

Conventional lighting mods typically attach lights to cells. The plugin will
contain data like position (which is stored as X, Y, and Z coordinates relative
to the origin of the cell), rotation (Euler angles or something? idk), etc. The
fade (brightness) and radius (size) of the light are stored under the light
object instead of the cell object.

If you added a light to Dragonsreach like this, you would have a plugin with
data stored like this:

```
cells:
  block_n:
    sub_block_n:
      dragonsreach: <--- vanilla dragonreach. Has to be included in order to
                         add a child record.
        placed_objects:
          temporary:
            my_placed_light <----- mod-added record
```
We can't include `my_placed_light` without also carrying forward the vanilla
record for `dragonsreach`. Without that `dragonsreach` record, there would be no
anchor for our light. This creates a compatibility issue. If you had another mod
which wanted to change the name of the cell from `Dragonsreach` to `Jarl's
Backside`, that data would go in the `dragonsreach` record, and it would
conflict with this plugin which places a light. Only one mod can win the
conflict of the `dragonsreach` record, so load order matters.

### Light Placer

Light Placer does not use plugins. It reads instructions from config files
written in JSON (this is what LPO provides) and injects lights directly in the
scene via SKSE during runtime. It also expects instructions via ini files for
how to disable game lights (LPO provides some of these too).

Light Placer configs expect instructions like which meshes to attach lights to,
what light object from the game should be added to it, and whether the
properties of that light should be overridden (like brightness, size, etc).

Light Placer treats configs as additive. That is, if two different config files
provide instructions for how to attach a light to the same mesh, that mesh will
receive lights from both configs. There is no conflict to resolve, though I
suppose you could call this "incompatible", depending on your definition.

For this reason, I do not recommend using LPO alongside other Light Placer
configs like CS Light or Placed Light. You can definitely do it, but things
won't look at all how it's intended unless you modify the inis and JSON files
to play nice with one another (e.g. remove duplicates). I don't provide support
for this, because it's really hard to actually mold configs to one another. For
instance, Placed Light attaches lights to fireplaces, and LPO attaches lights to
embers. It's impossible to read the configs of each mod and catch issues like
that, let alone solving this issue pragmatically.

CS Light at least sorts the various things they add lights to into different
categories. This enables using CS Light for FX light and LPO for sources that
should provide illumination. I'm not going to hold your hand through the fomod
options, but I will list the things that LPO adds lights to at the bottom of
this file. Can't promise I'll keep it up to date, but LPO is like 99% complete,
so it won't matter much either way.

## Whitelisting

LPO uses `bDisableAllGameLights=true` in
`Data/SKSE/Plugins/po3_LightPlacer.ini`. Specific vanilla game lights are
whitelisted via `Data/lightplacer/lpo/lpo.ini` by reference ID, which prevents
Light Placer from disabling them. These whitelisted references are mostly
simulating sunlight for interior locations, like the light that shines through
the holes in the ceiling in the entrance of Bleak Falls Barrow.

Every single plugin that adds light is disabled unless it's whitelisted (or
unless you set `bDisableAllGameLights=false`, which would give you a ton of fake
lights so it's not recommended).

Note that whitelisting plugins will probably give you fake lights. For some
plugins, like Lanterns of Skyrim (LOS), this is probably just fine, because most
of the lights LOS adds are outside and by lit lanterns. But whitelisting other
mods, especially other lighting overhauls, can cause issues.

Imagine this scenario. You've just installed LPO with the Eternal Flames option,
which extinguishes all candles in nordic dungeons and turns fire blue. You also
have Relighting Skyrim (or some other lighting overhaul) installed. The
Relighting Skyrim author, when making the plugin against the vanilla game,
noticed that there was a missing light by some candles in a dungeon, so they've
gone ahead and added a light there. This is fine without the whitelist, because
that light would be disabled. But if you whitelist Relighting Skyrim, the light
that Relighting Skyrim adds by those candles doesn't disappear; and since LPO
disabled those candles, you now have a fake light. Congrats.

It's possible to use conventional lighting overhauls alongside LPO both with and
without whitelisting them. If you don't whitelist the conventional mods, you'll
still benefit from level design changes they've made, like moving a lantern from
one side of the room to the other. If you do whitelist the conventional mods,
you'll get lights added by the conventional mod as well as from LPO.


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

```
"architecture\\highhrothgar\\hhlgbaylendl.nif"
"architecture\\highhrothgar\\hhlgbayr01.nif"
"architecture\\highhrothgar\\hhlgbayrangle.nif"
"architecture\\highhrothgar\\hhlgbaysm01.nif",
"architecture\\highhrothgar\\hhlgbaysm02.nif"
"architecture\\highhrothgar\\hhlgbaysmangle.nif"
"architecture\\highhrothgar\\hhlgbaysmcon01.nif"
"architecture\\highhrothgar\\hhlgbaysmcon02.nif"
"architecture\\highhrothgar\\hhlgbaysmend01.nif"
"architecture\\highhrothgar\\hhlgbaysment02.nif"
"architecture\\highhrothgar\\HHMainHallCon01.nif"
"architecture\\highhrothgar\\HHMainHallCon02.nif"
"architecture\\highhrothgar\\hhmainhalllgbaycon01.nif"
"architecture\\highhrothgar\\hhmainhalllgbaycon02.nif"
"architecture\\riften\\interior\\smallroomfirst\\rifrmsmfirstcorinwin02.nif"
"architecture\\riften\\interior\\smallroomfirst\\rifrmsmfirstwallwin01.nif",
"architecture\\riften\\interior\\smallroomfirst\\rifrmsmfirstwallwin02.nif"
"architecture\\riften\\interior\\smallroomsecond\\rifrmsmsecondwallwin01.nif"
"architecture\\solitude\\interiors\\slgcceiwin01.nif"
"architecture\\solitude\\interiors\\slgcdome01.nif"
"architecture\\solitude\\interiors\\slgcwalwin01.nif"
"architecture\\solitude\\interiors\\slgcwalwin02.nif",
"architecture\\solitude\\interiors\\slgftracon03.nif"
"architecture\\solitude\\interiors\\slgfwalsol01.nif"
"architecture\\solitude\\interiors\\slgfwalsol02.nif",
"architecture\\solitude\\interiors\\slgfwalsol03.nif"
"architecture\\solitude\\interiors\\slggwalsec05.nif"
"architecture\\solitude\\interiors\\smdastasol02.nif"
"architecture\\solitude\\interiors\\smdastasol03.nif"
"architecture\\solitude\\interiors\\smdcwinsol03.nif"
"architecture\\solitude\\interiors\\smdcwinsol04.nif",
"architecture\\solitude\\interiors\\smdcwinsol05.nif"
"architecture\\solitude\\interiors\\smddwinsol01.nif"
"architecture\\solitude\\interiors\\smdestasol01.nif",
"architecture\\solitude\\interiors\\smdestasol05.nif"
"architecture\\solitude\\interiors\\smdewinsol02.nif",
"architecture\\solitude\\interiors\\smdewinsol03.nif",
"architecture\\solitude\\interiors\\smdewinsol04.nif",
"architecture\\solitude\\interiors\\smdewinsol05.nif"
"architecture\\solitude\\interiors\\smdfflosol03.nif"
"architecture\\solitude\\interiors\\smdfwinsol01.nif"
"architecture\\whiterun\\wrinteriors\\wrcastle\\wrintcastlewallbasestr01win.nif"
"architecture\\whiterun\\wrinteriors\\wrcastle\\wrintcastlewallbasestrdouble02.nif"
"architecture\\whiterun\\wrinteriors\\wrcastle\\wrintcastlewallstrwin01double.nif"
"architecture\\whiterun\\wrinteriors\\wrcastle\\wrintcastlewallstrwin01.nif"
"architecture\\whiterun\\wrinteriors\\wrintwallcorwinl.nif",
"architecture\\whiterun\\wrinteriors\\wrintwallcorwinr.nif",
"architecture\\whiterun\\wrinteriors\\wrintwallstr01wina.nif",
"architecture\\whiterun\\wrinteriors\\wrintwallstr01winblow.nif"
"architecture\\whiterun\\wrinteriors\\wrjorvaskr\\wrintchentrancel.nif",
"architecture\\whiterun\\wrinteriors\\wrjorvaskr\\wrintchentrancer.nif"
"architecture\\whiterun\\wrinteriors\\wrjorvaskr\\wrintchrooftopstrchim01.nif"
"architecture\\whiterun\\wrinteriors\\wrjorvaskr\\wrintchstr01.nif",
"architecture\\whiterun\\wrinteriors\\wrjorvaskr\\wrintchstrslopel.nif",
"architecture\\whiterun\\wrinteriors\\wrjorvaskr\\wrintchstrsloper.nif"
"architecture\\whiterun\\wrinteriors\\wrtemple\\wrtempintcor01.nif",
"architecture\\whiterun\\wrinteriors\\wrtemple\\wrtempintpromalcove01.nif"
"architecture\\whiterun\\wrinteriors\\wrtemple\\wrtempintpromcustom01.nif"
"architecture\\whiterun\\wrinteriors\\wrtemple\\wrtempintroofmidwin.nif"
"architecture\\whiterun\\wrinteriors\\wrtemple\\wrtempintstr01.nif"
"architecture\\windhelm\\interiorkits\\castle\\whintcastlelroomwallwindow01.nif"
"architecture\\windhelm\\interiorkits\\castle\\whintcastleroomwallwindow01.nif"
"architecture\\windhelm\\interiorkits\\wood\\whintwoodbackwallwindow01.nif"
"architecture\\windhelm\\interiorkits\\wood\\whintwoodroofleftwindow01.nif"
"architecture\\windhelm\\interiorkits\\wood\\whintwoodroofrightwindow01.nif"
"architecture\\windhelm\\interiorkits\\wood\\whintwoodwallstonewindow02.nif",
"architecture\\windhelm\\interiorkits\\wood\\whintwoodwallstonewindow03.nif",
"architecture\\windhelm\\interiorkits\\wood\\whintwoodwallstonewindow04.nif",
"architecture\\windhelm\\interiorkits\\wood\\whintwoodwallstonewindow06.nif",
"architecture\\windhelm\\interiorkits\\wood\\whintwoodwallstonewindow07.nif"
"architecture\\windhelm\\interiorkits\\wood\\whintwoodwallwindow01.nif",
"architecture\\windhelm\\interiorkits\\wood\\whintwoodwallwindow02.nif",
"architecture\\windhelm\\interiorkits\\wood\\whintwoodwallwindow03.nif"
"architecture\\winterhold\\winterholdtowerintwall01.nif"
"architecture\\winterhold\\winterholdtowerintwall02.nif"
"architecture\\winterhold\\winterholdtowerintwall04.nif",
"architecture\\winterhold\\winterholdtowerintwall05.nif"
"architecture\\winterhold\\winterholdtowerintwall06.nif",
"architecture\\winterhold\\winterholdtowerintwall07.nif",
"architecture\\winterhold\\winterholdtowerintwall08.nif",
"architecture\\winterhold\\winterholdtowerintwall09.nif"
"architecture\\winterhold\\winterholdtowerintwall10.nif"
"clutter\\blackreach\\blackreachepicmushroom01.nif"
"clutter\\blackreach\\blackreachgiantmushanim01.nif"
"clutter\\blackreach\\blackreachgiantmushanim02.nif",
"clutter\\blackreach\\blackreachgiantmushanim03.nif"
"clutter\\blackreach\\blackreachgiantmushanim04.nif",
"clutter\\blackreach\\blackreachgiantmushanim05.nif"
"clutter\\blackreach\\blackreachgiantmushhoriz01.nif"
"clutter\\blackreach\\blackreachgiantmushhoriz02.nif",
"clutter\\blackreach\\blackreachgiantmushhoriz03.nif"
"clutter\\blackreach\\blackreachgiantmushhoriz04.nif"
"clutter\\blackreach\\blackreachsmallmushroom01.nif",
"clutter\\blackreach\\blackreachsmallmushroom02.nif",
"clutter\\blackreach\\blackreachsmallmushroom03.nif",
"clutter\\blackreach\\blackreachsmallmushroom04.nif",
"clutter\\blackreach\\blackreachsmallmushroom05.nif"
"clutter\\blackreach\\blackreachsun01.nif"
"clutter\\blacksmith\\blacksmithforge01\\blacksmithforge01.nif",
"clutter\\candles\\candlehornchandelier01.nif",
"clutter\\candles\\candlehornchandelier02.nif",
"clutter\\candles\\candlehornfloor01.nif",
"clutter\\candles\\candlehorntable01.nif",
"clutter\\candles\\candlehornwall01.nif",
"clutter\\chauruseggs\\eggsacs01.nif",
"clutter\\chauruseggs\\eggsacs02.nif"
"clutter\\chauruseggs\\eggsacs.nif",
"clutter\\common\\candlelanternwithcandle01.nif"
"clutter\\common\\removabletorch01.nif",
"clutter\\common\\torchpermanent01.nif"
"clutter\\daedric\\daedricreliquary\\daedricreliquary01.nif"
"clutter\\eyeofmagnus\\eyeofmagnus01.nif"
"clutter\\giant\\giantcampfire01burning.nif",
"clutter\\giant\\giantcampfire01burningnoland.nif",
"clutter\\giant\\wbbcfgiantcampfire01burning.nif",
"clutter\\giant\\wbbcfgiantcampfire01burningnoland.nif"
"clutter\\glazedcandles01.nif",
"clutter\\glazedcandlesstatic02.nif",
"clutter\\imperial\\impcandelabracandle01.nif",
"clutter\\imperial\\impcandelabracandle02.nif",
"clutter\\imperial\\impcandelabranocandle.nif",
"clutter\\imperial\\impcandle01.nif",
"clutter\\imperial\\impchandelliercandle01.nif",
"clutter\\imperial\\impchandelliercandle02.nif",
"clutter\\imperial\\impchandelliercandle03.nif",
"clutter\\imperial\\impchandelliernocandle01.nif",
"clutter\\imperial\\impwallsconce02candleon01.nif",
"clutter\\imperial\\impwallsconce02nocandle01.nif",
"clutter\\imperial\\impwallsconcecandle01.nif",
"clutter\\imperial\\impwallsconcecandle02.nif",
"clutter\\imperial\\impwallsconcenocandle01.nif",
"clutter\\quest\\tggoldencandlestick01.nif",
"clutter\\quest\\tggoldencandlestickstatic01.nif",
"clutter\\quest\\tgtq01silvercandlestick.nif",
"clutter\\ruins\\ruinscandlesconcenocandle01.nif",
"clutter\\ruins\\ruinscandlesconceon01.nif",
"clutter\\ruins\\ruinscandlesconceon02.nif",
"clutter\\ruins\\ruinsfloorcandlelampmidon02.nif",
"clutter\\ruins\\ruinsfloorcandlelampmidon.nif",
"clutter\\ruins\\ruinsfloorcandlelampmidstand.nif",
"clutter\\ruins\\ruinsfloorcandlelampsmon02.nif",
"clutter\\ruins\\ruinsfloorcandlelampsmon.nif",
"clutter\\ruins\\ruinsfloorcandlelampsmstand.nif",
"clutter\\silver\\silvercandlestick01.nif",
"clutter\\silver\\silvercandlestick02.nif",
"clutter\\silver\\silvercandlestick03.nif",
"clutter\\sovngarde\\sovcandlestick01.nif",
"clutter\\sovngarde\\sovcandlestick01static.nif",
"clutter\\sovngarde\\sovcandlestick02.nif",
"clutter\\sovngarde\\sovcandlestick02static.nif",
"clutter\\sovngarde\\sovcandlestick03.nif",
"clutter\\sovngarde\\sovcandlestick03static.nif",
"clutter\\woodfires\\campfire01burning.nif",
"clutter\\woodfires\\campfire01landburning.nif",
"clutter\\woodfires\\cookingstand01.nif",
"clutter\\woodfires\\fireplacewood01burning.nif",
"clutter\\woodfires\\wbbcfcampfire01burning.nif",
"clutter\\woodfires\\wbbcfcampfire01landburning.nif",
"creationclub\\_shared\\dungeons\\ayleidruins\\interior\\arcandleplate01.nif",
"creationclub\\_shared\\dungeons\\ayleidruins\\interior\\arcandleplate02.nif",
"dlc01\\dungeons\\castle\\animated\\candlestick\\",
"dlc01\\dungeons\\castle\\animated\\candlestick\\cascandlesticklever01.hkx",
"dlc01\\dungeons\\castle\\animated\\candlestick\\cascandlesticklever01.nif",
"dlc01\\effects\\dlc1falmervalleybrazierlight.nif"
"dlc01\\plants\\caveworm\\cavewormlarge.nif",
"dlc01\\plants\\cavewormgroup\\caveworm3group.nif",
"dlc01\\plants\\cavewormsmall\\cavewormsmall.nif"
"dlc01\\plants\\dlc01glowplant01.nif"
"dlc02\\architecture\\ravenrock\\dlc2blacksmithforge01rr.nif",
"dlc02\\clutter\\dlc2darkelflantern02.nif"
"dlc02\\clutter\\dlc2darkelflantern04.nif"
"dlc02\\clutter\\dlc2darkelflantern05.nif"
"dlc02\\clutter\\dlc2darkelflantern06.nif"
"dlc02\\clutter\\riekling\\dlc2rieklingcandle.nif",
"dlc02\\dungeons\\apocrypha\\animated\\aposconces\\apoheadscone02ani.nif",
"dlc02\\dungeons\\apocrypha\\animated\\aposconces\\apoheadscone03ani.nif",
"dlc02\\dungeons\\apocrypha\\animated\\aposconces\\apomouthsconce02ani.nif"
"dlc02\\dungeons\\apocrypha\\animated\\aposconces\\apomouthsconce03ani.nif"
"dlc02\\dungeons\\apocrypha\\animated\\aposcryetrigger01\\aposcryetrigger01.nif",
"dlc02\\dungeons\\apocrypha\\clutter\\apohoverlight01.nif"
"dlc02\\dungeons\\apocrypha\\clutter\\apolightpost01.nif",
"dlc02\\dungeons\\apocrypha\\clutter\\apolightpost02.nif"
"dlc02\\effects\\telvannitorchlightfx.nif"
"dlc02\\landscape\\dlc2firecrater02.nif",
"dlc02\\landscape\\dlc2firecraterround.nif"
"dlc02\\landscape\\dlc2fxsmokingplant02.nif",
"dlc02\\landscape\\dlc2fxsmokingplant.nif",
"dlc02\\landscape\\dlc2fxsmokingplantwithdirt.nif"
"dlc02\\landscape\\trees\\dlc2treepineforestlogsm01flaming01.nif"
"dlc02\\landscape\\trees\\dlc2treepineforestlogsm01smoking01.nif"
"dungeons\\dwemer\\animated\\astrolabe\\armillary\\dweastrolabearmillary01.nif"
"dungeons\\dwemer\\animated\\observatory\\armillary\\dweobservatoryarmillary01.nif"
"dungeons\\dwemer\\dwechandelier01bareon.nif"
"dungeons\\dwemer\\dwechandelier01bareonsputter.nif",
"dungeons\\dwemer\\dwechandelier01on.nif",
"dungeons\\dwemer\\dwechandelier01onsputter.nif",
"dungeons\\dwemer\\dwechandelier01simpleon.nif",
"dungeons\\dwemer\\dwechandelier01simpleonsputter.nif",
"dungeons\\dwemer\\dwechandelier02on.nif"
"dungeons\\dwemer\\dwechandelier02onsputter.nif",
"dungeons\\dwemer\\dwechandelierextension.nif"
"dungeons\\dwemer\\dwefloorlanternon.nif",
"dungeons\\dwemer\\dwefloorlanternonsputter.nif"
"dungeons\\dwemer\\dwewallsconce02on.nif"
"dungeons\\dwemer\\dwewallsconcesmall01on.nif",
"dungeons\\dwemer\\dwewallsconcesmall01onsputter.nif",
"dungeons\\dwemer\\dwewallsconcesmall02on.nif"
"dungeons\\dwemer\\dwewallsconcesmall02onsputter.nif"
"effects\\c06fxfirebluewithembersheavy.nif",
"effects\\fxfirepit01.nif",
"effects\\fxfiresovngarde.nif",
"effects\\fxfirewithembers01_cheap.nif",
"effects\\fxfirewithembers01_lite.nif",
"effects\\fxfirewithembers01.nif",
"effects\\fxfirewithembers02.nif",
"effects\\fxfirewithembers02toggle.nif",
"effects\\fxfirewithembers04.nif",
"effects\\fxfirewithembers05.nif",
"effects\\fxfirewithembersheavytoggle.nif",
"effects\\fxfirewithemberslogs01.nif",
"effects\\fxfirewithemberslogs03.nif",
"effects\\fxfirewithemberslogs04.nif"
"effects\\fxsplashlargechurn.nif"
"effects\\mgmagicfirepillar01.nif",
"effects\\mgmagicfirepillarmidden01.nif"
"effects\\mgmagicfirepillarsmall.nif"
"effects\\tg09nocturnalfxfirepurple.nif"
"furniture\\blacksmithforgemarker.nif",
"furniture\\blacksmithforgemarkerwr.nif",
"furniture\\blacksmithingskyforgemarker.nif"
"furniture\\enchantingworkbench.nif",
"furniture\\enchantingworkstation.nif"
"furniture\\orcfurniture\\orcblacksmithforgemarker.nif"
"furniture\\smeltermarker.nif"
"magic\\lightspellstaticlight.nif"
"plants\\floranirnroot01.nif"
"plants\\floranirnroot01red.nif"
"plants\\glowingmushroom01.nif",
"plants\\glowingmushroomcluster01.nif",
"plants\\glowingmushroomsingle01.nif"
"_resourcepack\\clutter\\imperial\\impchandelliercandle01nochain.nif",
"rest by campfire\\rbc_campfire_burning.nif",
"rest by campfire\\rbc_campfire_landburning.nif"
```

## Further Reading

* [Light Placer Wiki](https://github.com/powerof3/LightPlacer/wiki)
* [Community Shaders Wiki](
    https://github.com/doodlum/skyrim-community-shaders/wiki
  )
* [Creation Kit Wiki](https://ck.uesp.net/wiki/Light)
* [Tome of xEdit](https://tes5edit.github.io/docs/)

## Thanks

Thanks a bunch to powerofthree for making Light Placer so I could write configs
for it. It's been fun to work with.

