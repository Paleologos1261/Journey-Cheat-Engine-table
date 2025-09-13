# CE Table Manual

> [!IMPORTANT]  
> The table works ONLY with 15.07.2020 Steam release - Journey.exe, size: 58514KB

Made on Cheat Engine 7.1 (and later versions...) \
You'll probably need to know some very basics of Cheat Engine to use this. \
Outdated but still somewhat relevant video tutorial: https://www.youtube.com/watch?v=_Fjq8qJ9AWY

## 1. Acknowledgments

I included some of Rebi's codes (like time or movespeed). Props to him for these incredible findings. \
Wayfarer's symbol color and nametag position codes are courtesy of Seele. Thank you for your contribution! \
Shoutout to Alazar88 and Yupa_Miralda735 for figuring out how to use that table to play multiplayer in CS and Credits! \
Many thanks to Discord Journey community server for motivations, ideas and feedback. \
I absolutely DO allow sharing/copying/modifying this memory table. If you can improve it, go on and do it!

Have fun!

## 2. Quick Introduction

Address table is the main part of the hack(1). Code list (2) is something that you'll need in order to easily disable or restore instructions that write to certain addresses. You can access it by clicking Advanced Options (3) in Cheat Engine (bottom left). Codes that are there can be disabled by clicking RMB and choosing the option "replace with code that does nothing" or restored by choosing "restore the original code" (4). The option "find out what addresses this code accesses" will be crucial for some of the lighting modifications, when you'll need to find proper address (5).
![cheat engine usage explanation](/docs/images/ce-manual.jpg)
Since this is just a CE table, some of the addresses might work in a wrong way, cause strange anomalies in game or (temporarily) don’t work at all. I did test all of them but I can’t guarantee that they will always function 100% correctly. Addresses that need pointers are especially unstable in Journey and often stop working after level transitions.

## 3. Address list

- `LevelID` - shows current level ID number

### Physics

- `gravity <0.002499999944> moon = -0.04`- changes gravity (by Rebi)
- `Gravity <4.5>` - changes gravity. 0 is no gravity. Negative values invert it.
- `Flying Gravity? [depends on gravity] <-0.75>` - has something to do with coasting/gliding. Higher value makes you fly longer.
- `Jump gravity [lower=jump higher] <-3.450000048>` - defines jumping gravity
- `Diving Speed <2.5>` - defines diving speed
- `Boosting gravity [lower= fly higher] <1.399999976>` - defines boosting gravity.
- `Running speed <2.400000095>` - self explanatory. Negative values makes you run backwards. BUGGED! Loading level changes colors. Revert to inital value (2.40) to change levels safely.
- `movespeed <1>` - speed of movement (by Rebi)
- `time <1>` - controls game speed (by Rebi)
- `Wind speed? <0.3000000119>` - changes the wind physical force?
- `Cloak wind <1>` - defines cloak wind force.
- `General speedometer` - shows your current speed.
- `Boost powermeter` - shows how much boost power you have accumulated.

### Player WF

- `Scarf flying power` - blank address for copying flying power address from pointer if pointer is unstable.
	- `Scarf flying power` - pointer that shows flying power address. Should be mostly stable.
- `Scarf length` - blank address for copying flying power address from pointer if pointer is unstable.
	- `Scarf length` - pointer that shows scarf length address. Should be mostly stable.
- `Cloak color` - changes color and tier of wayfarer. 0-6
- `Player Symbol <0-20>` - changes the player's symbol. 0-20 [Higher values crash the game!]
- `WF Symbol Color [by Seele]`: \
	- `ChangeChirpSymbolColor` - script you can enable by clicking on the checkbox. You can modify RGB values for WF chirp symbol in the script.
	- `ChangeNametagBackColor` - script you can enable by clicking on the checkbox. You can modify RGB values for neck/torso WF symbol in the script.
	- `ChangeNametagFrontColor` - as above.
	- `Nametag (symbol) position` - inside this category you’ll find 3D position matrices that define the exact offset of WF symbols.
	- Seele provided his settings which go like this:
	```lua
		Vars.Dude.kJointNametagFront("R_wingAbend");
		Vars.Dude.kJointNametagBack("hip");
		Vars.Dude.kNametagFrontOffset({ { 0, 0, -1.2, 0 }, { 1.2, 0, 0, 0 }, { 0, -0.6, 0, 0 }, {-0.5, -0, 0, 1 } }); \
		Vars.Dude.kNametagBackOffset({ { 0, 0, -1, 0 }, { 1, 0, 0, 0 }, { 0, -0.8, 0, 0 }, { -0.5, -1, 0, 1 } });
	```
	- And some other joint names that one can use: \
	`R_wingAbend`, `hip`, `neck1`, `spineA`, `spineB`, `R_ankle`, `R_kneeA`, `M_Clo_backroot`, `M_Clo_upbackroot`
- `Scarf color <0-2>` - changes the color of scarf. Value range 0-2.
- `WF Scale <0.1000000015>` - blank address for copying flying power address from pointer if pointer is unstable.
	- `WF Scale` - changes the scale of player's WF. Setting it to high values breaks some cutscenes. Try also negative values. Slightly unstable pointer. Better to write down the address at the start of the game.
- `kHeadTurnMaxSpeed [WF head speed] <0.349>` - controls the head turning speed
- `kSymbolGlowOverbrightMlt [WF cloak symbol brightness] <2>` - brightness of the WF symbol below the head
- `kGlowOverbrightMult [WF glow brightness] <1.5>` - brightness of cloak glow effect
- `kGlowLerpSpeed [WF glow time] <7>` - decay time of the glow effect

### Chirping

- `ShoutRadInitial [Big shout size] <4>` - changes the radius of big chirp bubble.
- `ShoutRadInc [Big shout time] <1>` - changes the speed of big chirp bubble.
- `Chirp speed <0.4499999881>` - changes the speed of quick chirp.
- `Chirp radius <0.1000000015>` - changes the radius of quick chirp.
- `kShoutMinOpacity <0.174999997>` - changes the opacity of chirp bubble.
- `kShoutHDRInt [chirp brightness] <1>` - brightness of the chirp bubble.
- `kShoutDurMin <0.44>` - minimal time of the chirp bubble extension
- `kHitByShoutRadMult <1.2>` - ?
- `kFluidMass <0.25>` - the mass of chirp bubble (when it touches the sand/snow).
- `kFluidPushMagnitude <0.5>` - the strength of chirp bubble sand/snow push.
- `kFluidRadius <0.5>` - the radius of chirp bubble physics effect.
- `Chirp symbol size <0.07500000298>` - changes the size of chirp symbol
- `Chirp symbol size <0.075>` - the size of the symbol in chirp bubble.

### Uncategorised

- `Sand density <0.1000000015>` - controls the sand density.
- `Sand density sitting <0.05000000075>` - same as above but for meditating.
- `Colission checks per frame <8>` - controls collision system. Setting it to 0 makes you ignore vertical collision boxes. Sometimes it allows for walking on walls.

### Teleport XYZ

- `Pos X Z Y` - changes your position in game.
- `Push X Z Y` - controls the force vector in game.

### Nick

- `Pos X Z Y Nick` - controls the position of Nick (or companion as Nick is just a container for any companion. No, changing this DO NOT teleport your online companion, since his position is updated every frame).
- `Scale Nick` - scale of Nick (...or companion. This one works even in multiplayer, but it will only be visible on your end)
- `Nick robe color` - changes the color and tier of Nick robe (not working for companion)
- `Nick scarf length` - changes the length of Nick scarf (not working for companion)
- `Nick symbol` - changes Nick's symbol (not working for companion)

### Lighting (EnvNodeInstances and others)

- `Simple code replacement` - these codes need only one code to be replaced. Refer to the code list and disable the code if you want to change something here. For example if you want to change fog start, end or height values, disable the code that is named accordingly. Alternatively you can use one of the hotkeys that automatically disable lighting codes (see: Advanced Options [Hotkeys])
	- `Tint R G B` - changes the color tint. Also changes the brightness.
	- `FogStart` - changes how far should the fog start.
	- `FogEnd` - changes how far should the fog end.
	- `FogCloseColor R G B` - changes the color of fog in a close distance.
	- `FogFarColor R G B` - changes the color of fog in a long distance.
	- `FogCloseAlpha` - changes the brightness of near fog.
	- `FogFarAlpha` - changes the brightness of distant fog.
	- `FogHeightStart` - changes the starting height of fog.
	- `FogHeightEnd` - changes the ending height of fog.
	- `Env_LightDir` - controls the direction of light.
	- `Env_LightColor R G B` - changes the color of environmental color.
	- `Env_SpecularColor R G B` - changes the color of sun reflection on sand.
	- `Env_SpecularInt` - changes the intensity of sun reflection on sand.
	- `Env_SpecularPower` - changes the size of sun reflection on sand [lower values makes it wide but weaker, higher values makes it thinner but stronger].
	- `DOF Blur Intensity` - depth of field/background blur intensity (0-2)
	- `DOF Focus Distance` - how far from the camera should be the point of perfect sharpness
	- `DOF Focus Apperture` - works similarly to aperture in photography. Defines how long should be the area with perfect sharpness.
- `Find proper address and then replace two codes` - These codes are only representations of values that are stored in a different part of memory. You need to look up the code list and choose the code that you want to modify. There are almost always two of them. One writes to a bunch of addresses while the other only to one address. DO NOT DISABLE THEM IMMEDIETELY! First, find out to what addresses does this code write. You need to find address that is changing to 0 from time to time and is accessed more frequently than others. Usually it's located around 09CXXXXX or 09DXXXXX. Add this address to the table (set it to float format, not default 4 bytes) and only then disable both codes in the list (no. 1 and no. 2). In case of RGB values you'll have to look for two other addresses. To do that use memory viewer by clicking "browse this memory region" in RMB menu for that address. In the memory viewer look for nearest values. Find out which one is red, green or blue (don't forget to change the display type of memory viewer to float values [ctrl+9]). Check the video tutorial (https://www.youtube.com/watch?v=_Fjq8qJ9AWY&t=330s) for a step-by-step showcase. Unfortunately as of now it is not possible to have these addresses stored permanently in the table (pointer scan is useless). Every time you start the game, you'll have to repeat this process :(
	- `SkyMin-MaxColor R G B` - sky in Journey has 5 layers. From "min" - the lowest one to "max" - the highest one. These values controls the RGB color of each layer.
	- `SkyLow-HighHeight` - changes the height of three sky layers.
	- `BloomSize, Intensity` and Overbright - controls the bloom lighting. Try also negative values.
	- `ChromaticAbberation` - controls chromatic aberration post processing effect.
	- `VelvetRatio, VelvetInt` - not sure what exactly it changes.
	- `ClothAmbientColor R G B` - not sure if this is cloth or something else.
	- `EnvLightColor R G B` - not sure. This is probably environment light.
- `No code replacement needed` - just as it says. Enjoy the hacking without disabling any codes.
	 - `AoScalar` - changes the brightness of the sand.
	 - `F0spec` - changes the specular intensity of sun reflection.
	 - `MipTapBias` - changes the sun reflection filtering in the distance
	 - `NoiseFadeBias` - changes the distance of sand grains.
	 - `NoiseFaceScalar` - changes the size of sand grains.
	 - `SandSpecScalar` - changes the sand reflection intensity.
	 - `VelvetSpecularCorrection` - changes the shining effect of the sand.
	 - `Shading 1-6` - changes some shading values. Not exactly sure what. Set it to negative and positive values interchangeably to have a nice, trippy color effect on all surfaces in the game.

### Free Cam Options

- `Overwrite Camera Position Script` - check the box to detach camera from WF. You can still rotate it with mouse/controller.
- `Free Camera Mode With Rotation and Tilt Freeze` - check the box to freeze both camera movement and rotation.
- `Free Camera Control [numpad keys]` - check the box to enable my janky script that allows you to move camera around with numpad keys. You can only move it on XYZ axes. Numpad8/2 is Z axis (north-south), Numpad4/6 is X axis (east-west), Numpad 9/3 is Y axis (up-down). Hold E to slow down movement. Hold C to speed up movement.
- `Cam PosX` - Camera position on X axis
- `Cam PosZ` - Camera position on Z axis
- `Cam PosY` - Camera position on Y axis
- `Cam Zoom` - Camera zoom

### Camera

- `Idle timer <60>` - [In sec.] Defines when the game should enable screensaver.
- `Meditate time <40>` - [In sec.] Defines when WF starts meditating.
- `kControlTimer [Cam recenter speed] <3>` - [In sec.] Defines after how much time the camera will recenter automatically.
- `FOV <45>` - changes the field of view. You can try negative values.
- `FOV fast <75>` - also changes the field of view. You can try negative values.
- `Camera side screen pos <0.3330000043>` - controls the off-center position of the camera.
- `kScreenPosLandY [Cam pos Y] <-0.150000006>` - changes the height of the camera.
- `Camera pos Y 2 <0.200000003>` - similar to above.
- `kYawTiltSpeed [cam L-R sensitivity] <1.299999952>` - changes the sensitivity of left-right camera movement.
- `kStickYSpeed [cam up-down sensitivity] <1>` - changes the sensitivity of up-down camera movement.
- `kPitchStandingRange <60> `- changes how much you can look up.
- `Camera distance <0.5>` - changes the distance of the camera from WF.
- `Dive camera? <0.5>` - unsure. Has something to do with camera while diving...
- `Objects clipping camera <0.150000006>` - changes how far from the camera should everything disappear.
- `Cam shaking speed <0.006000000052>` - controls camera shakiness.
- `Cam shaking <0.5>` - controls camera shakiness.
- `Cam shaking position <0.03999999911>` - controls camera shakiness.
		
Added a bunch of camera variables in 1.4. I don't know what exactly every single one does. You can experiment on your own.

- `kTerrainPitchScale <0.6>` - defines how much you can pitch the camera during a flight.

### Video & Audio

- `Resolution Width` - rendering resolution width.
- `Resolution Height` - rendering resolution height.
- `Dune & Sand & Fluid quality` - same as in graphics options.
- `MSAA` - same as in graphics options.
- `Anisotropy` - Anisotropic filtering (goes up to 4, beyond that you’ll get graphics corruption).
- `Music volume & Effects volume & Master volume` - 1-10 is normal setting. You can set it to 20 or more if you want to hurt your eardrums.

### Advanced Options [Hotkeys]

That category is reserved purely for hotkeys. Don't change anything here. Refer to the [Hotkeys](#5-hotkeys) part of this readme to see how to use it.

### Corruptions
FUN :D
Be careful with changing values here. Anything can easily crash the game.

## 4. Code list

Open it by clicking "Advanced Options" at the bottom left of Cheat Engine window.

### Simple Code replacement

These are codes that when disabled will allow you to change some lighting values. In this version of the table there are hotkeys that automatically enable manual lighting modifications. Refer to the list below.

### Find proper address and then replace two codes

These codes will allow you to find the right values. Click RMB on code and choose "find out what addresses this code writes to". Add the address that you'll see to the table (it's always the one that is changing to 0 from time to time and has much higher count of overwrites than rest of them). Then you can disable both no. 1 and no. 2 codes by choosing an option to "replace with the code that does nothing". Now you should be able to modify the value to your likings. If you do something wrong then the option will just not work and set the value to 0, so you'll have black sky or no bloom. Bloomoverbright shares a code with BloomIntensity 2. 
Check the video tutorial (https://www.youtube.com/watch?v=_Fjq8qJ9AWY&t=330s).

### Others

Bunch of other codes that I found. Most notable are:
- `Sliding on/off` - use that before entering SC to disable sliding.
- `Coldness on/off 1 & 2` - disables coldness effect in Snow.
- `Triggers freeze on/off` - freezes all triggers. Allows connection in all levels. Also under hotkeys: alt+T, alt+Y.
- `Unlock Cutscene Camera` - use that before entering cutscene (HL for example) to unlock camera (by Alazar88).
- `Objects no clip` - disables collisions from objects.
- `Terrain no clip` - disables collisions from terrain.
- `Disable Objects` - makes all objects invisible.
- `Invisible WF` - makes WF invisible.
- `Bayblade WM` - sometimes makes WM spin like crazy (not 100% reliable).
- `WF Head Horizontal Movement Hold 1 & 2` - stops WF head movement in horizontal axis.
- `WF Head Vertical Movement Hold 1 & 2` - stops WF head movement in vertical axis.

## 5. Hotkeys

The table comes with some hotkeys already set up. You can change them by clicking RMB on an address and choosing "set/change hotkeys".

### Various hotkeys

- `shift+A` - resets all gravity settings to normal.
- `ctrl+3 to 9` - sets robe color and tier.
- `ctrl+1 or 2` - sets scarf color.
- `shift+. or >` - sets WF scale to 10. (Breaks some cutscenes and allows to walk around)
- `shift+, or <` - sets WF scale to 0.1000000015 (normal on most of the levels)
- `alt+- or _` and `alt+= or +` - sets CollisionCheksPerFrame to 0 or 8.
- `alt+W` - every time you use this the game will speed up by x2 (You can skip HL. Suprisingly stable)
- `alt+Q` - reset game speed to normal
- `alt+E` - super flying mode. (may cause glitches; reset with shift+A)
- `alt+R` - DISCO MODE! (reset with panic hotkey - ctrl+tab+home)
- `alt+T` - triggers freeze ON - You can use that to freeze all triggers. Alazar88 found out that it can be used to play online in ALL levels including CS!
- `alt+Y` - triggers freeze OFF - Restores normal triggers.
- `alt+G` - sliding off in SC (use that before entering level)
- `alt+H` - sliding on in SC
- `alt+O` - sets color tint option to manual mode.
- `alt+U` - sets simple lighting options to manual mode.
- `alt+I` - sets color tint and simple lighting options to automatic mode.

### Level Swap Hotkeys

Ever wanted to play in Credits? Now you can! With this simple trick you can enter otherwise inaccessible areas. All you need to do is to use hotkey and then enter one of three levels: BB, UG or Tower. Feel like a TGC developer and explore non-solid objects or beta version of Pink Desert. Everything with just one magical hotkey!

> "It's so simple. All I had to do is click right button and step into the portal in CS hub area. My life is different now!" - XxX_ProJourneyPlayer_XxX

> "When I discovered that with one click I can go to level09 I couldn't believe it. Thanks to this trick I don't have to change save file manually anymore. Now I have time for other things. I earned my PhD and found a solution to global warming. Thanks a lot!" - RandomWayfarer4261

- `alt+L` - reset all.
- `alt+K` - replaces UG with Level_Matt (Credits version of SC and PD; to move around use triggers freeze option).
- `alt+N` - replaces Tower with Level_Chris (CS and BB at night).
- `alt+M` - replaces Tower with Level09 (beta PD).
- `alt+J` - replaces BB with Level_Credits (Credits version of Snow, Tower and UG; to move around use triggers freeze option).

### Other Hotkeys

- There are bunch of hotkeys for teleport. All are under Tab + something. For example `Tab+F1` up to `F8` teleport to the next level trigger (`Tab+F1` - CS>BB; `Tab+F2` - BB>PD; `Tab+F3` - PD>SC etc.)
- There are also bunch of presets that I made for simple code replacement lighting settings. They are mapped under `alt+A S D F Z X C V`. You can try them out. If you don't know or don't want to use manual method then just hit `alt+O` and `alt+U` to unlock these presets. Reset with `alt+I`

### Stupid easter egg hotkeys

- `Ctrl+Tab+F10` - RTX ON
- `Ctrl+Tab+F9` - Potato mode
- `Ctrl+Tab+F8` - No terrain collision
- `Ctrl+Tab+Home` - Panic key (use to reset if everything else fail)
- `Ctrl+Shift+F12` - No.
- `Ctrl+Shift+Tab+F12` - You can play as WM.
- `Ctrl+Shift+Tab+F11` - You can play as ancestor (RIP headphone users [WARNING: I'm not joking!])
