# 🧊 Universal Shading Language

Universal Shading Language (USL) is new language for shading. `.usl` extension can be used for USL files. 
The main goal of USL is simplfy shaders, 
provide mixins (expecially for common tasks) and translate universal language to vendor specific shaders.

For instance, a simple shader that is written in USL can be compiled/translated to GLSL, HLSL or Mesal Shading Language (MSL)... 
This will help to write platform independent portable shaders. 
This is the main goal of the USL language.

Also a VM will be provided, so shaders will be able to run on CPU or GPU (by translated to GLSL, HLSL, MSL, SPIR-V...). USL will also provide library machanizm like Metal or better than Metal. 

Shader caching will also be provided by utilities or Database. Shaders can also be ASCII or binary...

## Expected Features

* You must be able to write shader faster
* Utilitis, mixins, functions... will be provided for common tasks, shading models...
* Cross platform, platform independent shaders
* USL can be translated/compiled GLSL, HLSL, MetalSL, Spir-V and its own IL
* VM will be provided 
* Compiler will be privided as library and as tool
* Shader caching will be provided with a library
* Shader library will be supported
* Lot of utilities, mixins, tools, documentations....... will be provided
* ...

## Proposals

1. [Syntax Proposals](https://github.com/UniversalShading/spec/blob/master/SyntaxProposals.md)
