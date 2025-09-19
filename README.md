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

E.g.,
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
"architecture\\winterhold\\winterholdstowerintwall01.nif",
"architecture\\winterhold\\winterholdstowerintwall02.nif"
"architecture\\winterhold\\winterholdtowerintwall01.nif"
"architecture\\winterhold\\winterholdtowerintwall02.nif"
"architecture\\winterhold\\winterholdtowerintwall04.nif",
"architecture\\winterhold\\winterholdtowerintwall05.nif"
"architecture\\winterhold\\winterholdtowerintwall06.nif",
"architecture\\winterhold\\winterholdtowerintwall07.nif",
"architecture\\winterhold\\winterholdtowerintwall08.nif",
"architecture\\winterhold\\winterholdtowerintwall09.nif"
"architecture\\winterhold\\winterholdtowerintwall10.nif"
"clutter\\blackreach\\blackreachbush01.nif",
"clutter\\blackreach\\blackreachbush02.nif"
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
"clutter\\obs_clutter\\obs_candleonly_01.nif",
"clutter\\obs_clutter\\obs_candleonly_02.nif",
"clutter\\obs_clutter\\obs_candleonly_03.nif"
"clutter\\obs_lightfixtures\\obs_silvercandelabrapenta_01.nif",
"clutter\\obs_lightfixtures\\obs_silvercandelabrasingle_01.nif",
"clutter\\obs_lightfixtures\\obs_silvercandelabrasingle_02.nif",
"clutter\\obs_lightfixtures\\obs_silvercandelabrasingle_03.nif",
"clutter\\obs_lightfixtures\\obs_silvercandelabratriple_01.nif",
"clutter\\obs_lightfixtures\\obs_silvercandelabratriple_02.nif",
"clutter\\obs_lightfixtures\\obs_silvercandlesconce_01.nif",
"clutter\\obs_lightfixtures\\obs_silvercandlestick_04.nif",
"clutter\\obs_lightfixtures\\obs_silverchandelierlarge_01.nif",
"clutter\\obs_lightfixtures\\obs_silverchandeliermedium_01.nif",
"clutter\\obs_lightfixtures\\obs_silverchandeliersmall_01.nif",
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
"clutter\\shrines\\shrinebase.nif",
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
"creationclub\\asvsse001\\clutter\\velothi\\mwcandle01.nif",
"creationclub\\eejsse002\\clutter\\eej_remappedglazedcandlecup.nif",
"creationclub\\eejsse002\\clutter\\eej_remappedglazedcandleplate.nif",
"creationclub\\eejsse002\\furniture\\eej_enchanter.nif",
"creationclub\\eejsse003\\clutter\\eej_remappedglazedcandlecup.nif",
"creationclub\\eejsse003\\clutter\\eej_remappedglazedcandleplate.nif",
"creationclub\\eejsse004\\clutter\\eej_chandeliershort.nif",
"creationclub\\eejsse004\\clutter\\eej_remappedglazedcandlecup.nif",
"creationclub\\eejsse004\\clutter\\eej_remappedglazedcandleplate.nif",
"creationclub\\eejsse005\\clutter\\eej_remappedglazedcandlecup.nif",
"creationclub\\eejsse005\\clutter\\eej_remappedglazedcandleplate.nif",
"creationclub\\_shared\\dungeons\\ayleidruins\\interior\\arcandleplate01.nif",
"creationclub\\_shared\\dungeons\\ayleidruins\\interior\\arcandleplate02.nif",
"critters\\firefly\\firefly.nif"
"dlc01\\architecture\\snowelfruins\\seruinschandelier01.nif",
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
"dlc02\\effects\\telvannilifteffect02.nif"
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
"effects\\fxdwegreenflamecalm.nif"
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
"effects\\testcandleflame01.nif",
"effects\\tg09nocturnalfxfirepurple.nif"
"furniture\\blacksmithforgemarker.nif",
"furniture\\blacksmithforgemarkerwr.nif",
"furniture\\blacksmithingskyforgemarker.nif"
"furniture\\enchantingworkbench.nif",
"furniture\\enchantingworkstation.nif",
"furniture\\orcfurniture\\orcblacksmithforgemarker.nif"
"furniture\\smeltermarker.nif"
"furniture\\workbenches\\disenchantworkbench01.nif",
"furniture\\workbenches\\enchantingworkbench01.nif",
"furniture\\workbenches\\enchantingworkstation01.nif",
"magic\\lightspellstaticlight.nif"
"plants\\floranirnroot01.nif"
"plants\\floranirnroot01red.nif"
"plants\\glowingmushroom01.nif",
"plants\\glowingmushroomcluster01.nif",
"plants\\glowingmushroomsingle01.nif"
"_resourcepack\\clutter\\imperial\\impchandelliercandle01nochain.nif",
"rest by campfire\\rbc_campfire_burning.nif",
"rest by campfire\\rbc_campfire_landburning.nif"
"uskp\\clutter\\chandellier\\impchandelliercandle01uskp.nif"
```

I don't keep the list in this readme up to date, so check against jq.

## Further Reading

* [Light Placer Wiki](https://github.com/powerof3/LightPlacer/wiki)
* [Community Shaders Wiki](
    https://github.com/doodlum/skyrim-community-shaders/wiki
  )

## Thanks

Thanks a bunch to powerofthree for making Light Placer so I could write configs
for it. It's been fun to work with.

