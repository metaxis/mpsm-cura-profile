# mpsm-cura-profile
Monoprice MP Select Mini V1 and V2 profile, quality presets, and variants for Cura 3.

The included settings produce good results for a wide range of common printing needs, and it is easy to extend the profiles for specific cases.

## Instructions
You should be able to unpack these settings under the directory returned by "Show Configuration Folder" under the Cura "Help" menu.  You can also pick and choose files, dropping them into the subdirectories as shown below.

## MP Select Mini Profile
    definitions/mp_select_mini.def.json
The machine profile contains printer specifications, reasonable default speeds, start/end gcode.  The print volume is set to 125 x 125 x 123, as there have been reports of topping out at 124 in the Z axis, and some space is needed to lift the head off the print when finishing.  There is nothing specific to V1 or V2 editions of the printer that should need to change.

## Quality settings
    quality/mp_select_mini/mpsm_normal.inst.cfg
    ...
There are multiple conflicting goals with FFF quality settings.  Layer height, shell thickness, infill, print and movement speeds, all interact with quality and overall speed, and there isn't a single correct answer.  For example, a large layer height with slower print speed is ideal for reasonably fast dimentionally accurate printing of low-detail parts.  

The provided default qualities are a *small* sampler of the most common goals.  It is quite likely you will run into special cases for which none of these are suitable, but any are a reasonable starting point for your particular print job.


| Quality | Height (mm) | Speed (mm/s) | shell (mm)* | infill |
| --- | --- | --- | --- | --- |
| Extra Fine | **0.0875** | 30 | 0.8 | 25 |
| Fine | **0.175** | 30 | 0.8 | 20 |
| Normal | **0.175** | 40 | 0.8 | 20 |
| Coarse | **0.2625** | 40 | 0.8 | 20 |
| Draft  | **0.2625** | 50 | 0.4 | 15 |
| Very Draft | **0.35** | 55 | 0.4 | 5 |

\* includes top and bottom thickness.

### Magic Number Layer Heights

From  Michael O'Brien's excellent [X, Y, Z, A Motors & Stepper Driver Investigation](https://hackaday.io/project/12696-monoprice-select-mini-electro-mechanical-upgrades/log/44772-x-y-z-a-motors-stepper-driver-investigation) we have derived for us layer heights that align slices correctly with what the Z motion system in the Mini can actually do.

Unfortunately, in Cura this value is rounded to 4 digits - for instance *0.13125* becomes *0.131****3***.  That loss of precision will become a slow cumulative error, making the magic numbers requiring more than 4 decimal places potentially worse than more "round" numbers due to aliasing harmonics.  I'm happy to have someone prove me wrong.  In the meantime, if you'd like quality settings of those or other layer heights, it's easy enough to do within Cura.  Magic Numbers not included: 0.04375 0.13125 0.21875 0.30625


## Nozzle Width Variants
    variants/mp_select_mini_0.4.inst.cfg
    ...
How many different nozzles are people actually using?  Nine seems excessive.  How about 0.2, 0.3, 0.4, 0.6, 0.8?


## Motivation

While trying to use the [updated profiles for Cura](https://downloads.monoprice.com/files/software/21711_Software_171026.zip) recently (October 2017) put up on Monoprice's [MP Select Mini product page](https://www.monoprice.com/product?p_id=21711), it seems like something got lost in translation.  For instance, "Traditional Layer heights" are actually variants of nozzle size. It also turns on non-standard, sub-optimal, and/or experimental settings like coasting by default, and has mutually conflicting or redundant overrides. Coasting, in addition to being experimental, needs settings very specific to material & temperature. Printing speeds are redundantly set to different, conflicting values in profile, variant, and quality settings, such that it's unclear which will take precedence. It was an awesome motivator to finally dig in to Cura's profiling/settings system.

## Settings not included

There are many settings that are inappropriate to defaults: specific to the part, the material, the bed adhesion method in use, or experimental or other anecdotally favorite settings that work only with special tuning or conditions.  For lack of a better home and poor othogonality, they have snuck into the wrong places.  These settings try to avoid this.
  
Ultimaker uses "quality" for bundling settings for different materials, to the extent that the Ultimaker 3 has ***101 quality profiles***.  Besides being ripe for refactoring in Cura, per-material quality sets is out of scope for this first release.

