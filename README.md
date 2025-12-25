# Lackofbindings' ORL Modules

This VPM provides custom modules for the [ORL shader suite](https://shaders.orels.sh/) *(and accompanying variants of the ORL Standard shader which include said modules)*.

## Included Modules:

### Stencil Options

> ⚠️ The Stencil Options module is deprecated with ORL 7.0.0+, stencil options are now included by default.

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

### UV Tile Discard

This module is based on code from the ["Inventory System"](https://gitlab.com/s-ilent/SCSS/-/wikis/Manual/Inventory-System)  from Silent's Cell Shading Shader as well as [Orels' UV Discard Module](https://shaders.orels.sh/docs/toon/uv-discard). 

This allows you toggle sections of your mesh during runtime by animating the corresponding checkbox in the material. Sections can be defined by offsetting their UVs along whole numbers of U or V (UDIM tiles). It is recommended to use a secondary UV set for this, as to not mangle the UVs used for texturing. Please ensure your UV islands have a small gap between tile boundaries, otherwise vertices may end up accidentally assigned to the neighboring tile.

It is intended to maintain compatibility with the following similar features:
1. SCSS "Inventory System":
   - Set `X Tiles` to **17** and `Y Tiles` to **1** 
   - Animated property names have been retained for drop-in compatibility. 
2. Poiyomi "UV Tile Discard":
   - Set `X Tiles` to **4** and `Y Tiles` to **4**
3. ORL "UV Discard":
   - Set `X Tiles` to **10** and `Y Tiles` to **1** 

Also note that a more simple module that serves the same purpose is already included with the ORL Shader Suite under `@/Modules/Toon/UVDiscard`. The focus of this module is compatibility with existing avatar meshes.

This module is also available in a variant that uses the Poiyomi property naming conventions, for use as a drop-in for animations created against a Poiyomi material.

### RGBA Color Mask

This module allows you to supply a mask texture and 4 colors, where each channel of the mask defines the region where the color will be mixed with the base color. Each color is applied in-order of the channels of the mask. The alpha of each color swatch can be used to control intensity.

### Color Adjust

This module provides Hue, Saturation, and Brightness sliders to adjust both the Albedo colors and Emission colors (if enabled). It shares the same mask texture and sampler with ORL Standard. It also allows you to select a channel of the mask texture to use to mask the effect. Color adjustment algorithms from [Poiyomi Toon Shader](https://github.com/poiyomi/PoiyomiToonShader).

### AO UV Channel Select

This module provides an extra dropdown to select which UV channel of the main mask map you'd like to sample for AO. This is useful if your AO map has been baked to a secondary UV set, but you'd still like to take advantage of packing it with the rest of the standard mask maps. It shares the same mask texture and sampler with ORL Standard. 

### Detail Normal Layers

This module adds 4 detail normal texture slots. Each texture slot has individual controls for tiling, offset and strength. It features one mask texture slot where each of the 4 RGBA channels corresponds to one of the normal texture layers, similar to the [RGBA Color Mask Module](#rgba-color-mask). Based on the code from the official Details module.

### Detail Metallic

This module adds an input for a packed texture containing metallic and smoothness detail maps. Each layer is added to the corresponding base metallic/smoothness values, with a slider to control the strength of each (or invert it). This is useful for adding tiled detail to your PBR surfaces.

### Decal Layer PBR 

This module adds an extra set of PBR properties (Albedo, Metallic, Smoothness, Normal) that is blended on top of the base material. Similar to a Poiyomi "Decal" module, but with PBR properties.

### LOD Dither Fade

This module enables dithered cutout cross-fading support for use with [LOD groups](https://docs.unity3d.com/2022.3/Documentation/Manual/class-LODGroup.html). The LOD group must have its Fade Mode set to `Cross Fade` and Fade Transition Width must be greater than 0. Uses the built-in UnityApplyDitherCrossFade() based on [the example created by keijiro](https://github.com/keijiro/CrossFadingLod/).

### Std Fallback Properties

This module does nothing but expose some of the default Unity Standard shader properties that are not in ORL. These have no effect and are only for the sake of providing those properties to fallback shaders that expect those property names.

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

The easiest way to use a module is to create a new Configurable Shader and include any combination of modules that you want:

1. Create > Shader > orels1 > **Configurable Shader**.
2. Change the **Base Shader** to `ORL Standard` *(or whatever you want, many modules may rely on PBR lighting model and/or ORL Standard though)*.
3. In the **Modules** list, check the Custom Module checkbox and select any module you want. You can include as many as you need for whatever features you want.
4. Give your shader a unique name in the **Shader Name** box.
5. Hit apply and you can start using your new custom shader.

If you prefer working with code, the modules can also be included in any `.orlshader` or `.orlsource` by listing the module in your Includes block:
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

