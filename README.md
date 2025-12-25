# Lackofbindings' ORL Modules

This VPM provides custom modules for the [ORL shader suite](https://shaders.orels.sh/) 

## Included Modules:

See [Modules.md](Modules.md) for the full list of included modules.

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

