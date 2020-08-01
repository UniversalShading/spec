# 🧊 Universal Shading Language

Universal Shading Language (USL) is new language for shading. `.usl` extension can be used for USL files. 
The main goal of USL is simplfy shaders, 
provide mixins and translate universal language to vendor specific shaders.

For instance, a simple shader that is written in USL can be compiled/translated to GLSL, HLSL or Mesal Shading Language (MSL)... 
This will help to write platform independent portable shaders. 
This is the main goal of the USL language.

Also a VM will be provided, so shaders will be able to run on CPU or GPU (by translated to GLSL, HLSL, MSL, SPIR-V...). USL will also provide library machanizm like Metal or better than Metal. 

Shader caching will also be provided by utilities or Database. 

## Syntax Proposals

1. [SyntaxProposals.md](https://github.com/UniversalShading/spec/blob/master/SyntaxProposals.md)
