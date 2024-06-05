# Lackofbindings' ORL Modules

This VPM provides custom modules for the [ORL shader suite](https://shaders.orels.sh/) *(and accompanying variants of the ORL Standard shader which include said modules)*.

## Included Modules:

#### Stencil Options

This Module provides the standard stencil masking options (stencil mask value, pass/fail/comparison, etc.)

#### AudioLink Pathing

This module ports the audiolink code from [Silent's Cell Shading Shader](https://gitlab.com/s-ilent/SCSS) to ORL Standard. This provides Furality-style audiolink with separate channel (AL band) and sweep (direction) maps. The only new addition is a toggle to flip the direction of the sweep, since some shaders (Poiyomi, Furality, SCSS) interpret the sweep map differently.

#### 2nd Emission

This module adds a secondary emission texture slot. It provides its own tint color, UV channel, and RGB channel options. It shares the same tiling, offsets, sampler, and keyword with the base emission slot. 

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

If you do not have access to the VCC, there are also unitypackage versions avalible in the [Releases](https://github.com/lackofbindings/ORLModules/releases/latest).

## Usage
 
#### As a shader

Ready-to-use variants of ORL Standard can be found when making a new material:
- `orels1/Standard Stencil`
- `orels1/Standard Audiolink Pathing`
- `orels1/Standard 2nd Emission`

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
See the official [ORL Shader Generator documentation](https://shaders.orels.sh/docs/generator/development-basics) for more info.

