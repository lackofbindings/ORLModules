# Lackofbindings' ORL Modules

This VPM provides custom modules for the [ORL shader suite](https://shaders.orels.sh/) *(and accompanying variants of the ORL Standard shader which include said modules)*.

## Included Modules:

### Stencil Options

This Module provides the standard stencil masking options (stencil mask value, pass/fail/comparison, etc.)

### AudioLink Pathing

This module ports the AudioLink code from [Silent's Cell Shading Shader](https://gitlab.com/s-ilent/SCSS) to ORL Standard. This provides Furality/Poiyomi-Pathing style AudioLink. 

**It supports three different styles of pathing maps:**
1. SCSS/Poiyomi-style AudioLink pathing with a Color/Mask map and a Channel/Direction map.
2. Furality-style with a separate channel (AL band) map and sweep (direction) map.
3. A simplified Furality-style mode that loses the 4th AL band in favor of packing in the sweep (direction) map into the alpha channel, thus only requiring one texture.
 
This module also features a toggle to flip the direction of the sweep, since some shaders (Poiyomi) interpret the sweep map differently.

### 2nd Emission

This module adds a secondary emission texture slot. It provides its own tint color, UV channel, and RGB channel options. It shares the same tiling, offsets, sampler, and keyword with the base emission slot. 

### Gradient Map (Grab Pass)

This module multiplies the albedo by a grab pass, where the grab pass has been mapped to a color gradient based on its luminance value (think "Color Ramp" in Blender or "Gradient Map" in Photoshop). This is mostly a novelty, but could be used to make a glass surface that stylizes other objects viewed through it.

### UDIM Tile Discard

> ⚠️ This module is still a work in progress and may not work as intended and may break with future updates.

This module ports the "Inventory System" from SCSS. This is also known in Poiyomi as "UV Tile Discard". This allows you define sections of you mesh that can be toggled during runtime by offsetting their UVs along whole numbers of U or V (UDIM tiles). This module attempts to be compatible with both formats *(16x1 and 4x4) or any other format as long as the max tiles is 16 (not including 0)*, though that is unstable at the time of this writing. 

### RGBA Color Mask

This module allows you to supply a mask texture and 4 colors, where each channel of the mask defines the region where the color will be mixed with the base color. Each color is applied in-order of the channels of the mask. The alpha of each color swatch can be used to control intensity.

## How to Install

### Dependencies

This package is made with the ORL Shader Generator and extends ORL Standard, and thus depends on all 3 of the ORL Shader packages:
1. ORL Shaders
2. ORL Shader Generator
3. ORL Shader Inspector

These will be installed automatically by the VCC when you add this package to your project. However you will need to add the ORL Shaders repo to your VCC before using this package.

### Install

1. If you do not already, ensure you have the [ORL Shader Suite](https://shaders.orels.sh/#quick-start) repo added to your VCC.
2. Go to the [VPM Listing](https://lackofbindings.github.io/ORLModules/) for this repo and hit "Add to VCC".
   
If the "Add to VCC" button does not work you can manually enter the following url into the Packages settings of the VCC `https://lackofbindings.github.io/ORLModules/index.json` 

If you do not have access to the VCC, there are also unitypackage versions available in the [Releases](https://github.com/lackofbindings/ORLModules/releases/latest).

## Usage
 
#### As a shader

Ready-to-use variants of ORL Standard can be found when making a new material:
- `orels1/Standard Stencil`
- `orels1/Standard Audiolink Pathing`
- `orels1/Standard 2nd Emission`
- ...etc.

See the [Shaders Directory](Packages/com.lackofbindings.orlmodules/Runtime/Shaders/) for all pre-made shaders.

#### As a module

The modules can also be included in any `.orlshader` or `.orlsource` by listing the module in your Includes block:
```
%Includes()
{
    "@/Shaders/ORL Standard",
    "/Packages/com.lackofbindings.orlmodules/Runtime/Modules/AudiolinkPathing",
    "self"
}
```
See the [Modules Directory](Packages/com.lackofbindings.orlmodules/Runtime/Modules/) for all available modules.

See the official [ORL Shader Generator documentation](https://shaders.orels.sh/docs/generator/development-basics) for more info info on building your own shaders.

