# Proposed Syntax 

Referenced Metal Shader (Vertex)

```metal
vertex ColorInOut ShaderName(Vertex in [[stage_in]],
                             constant Uniforms & uniforms [[ buffer(0) ]]) {
    ColorInOut out;

    float4 position = float4(in.position, 1.0);
    out.position    = uniforms.projectionMatrix * uniforms.modelViewMatrix * position;
    out.texCoord    = in.texCoord;

    return out;
}
```

USL (Universal Shading Language):
```Swift
vertex ColorInOut ShaderName (in: Vertex as stage_in, uniforms: Uniform(0)) {
  var out: ColorInOut
  
  let position = float4(in.position, 1.0)
  out.position = uniforms.projectionMatrix * uniforms.modelViewMatrix * position
  out.texCoord = in.texCoord
  
  ^ out
}
```

or

```Swift
[ShaderName]
vertex ColorInOut (in: Vertex as stage_in, uniforms: Uniform in buffer(0)) {
  var out: ColorInOut
  
  let position = float4(in.position, 1.0)
  out.position = uniforms.projectionMatrix * uniforms.modelViewMatrix * position
  out.texCoord = in.texCoord
  
  ^ out
}
```

or 

```Swift
[ShaderName]
vertex ColorInOut (in: Vertex as stage_in, uniforms: Uniform(0)) {
  var out: ColorInOut
  
  let position = float4(in.position, 1.0)
  out.position = uniforms.projectionMatrix * uniforms.modelViewMatrix * position
  out.texCoord = in.texCoord
  
  ^ out
}
```

Alternatives:

```Swift
[vertex]
ShaderName: Vertex in as stage_in, Uniform(0) uniforms {

}

vertex ShaderName: Vertex in as stage_in, Uniform(0) uniforms {
  sum: a, b ^ a + b
}
```

```Swift
[phong]
- vertex in: Vertex as stage_in, uniforms: Uniform(0)) {
  var out: ColorInOut
  
  let position = float4(in.position, 1.0)
  out.position = uniforms.projectionMatrix * uniforms.modelViewMatrix * position
  out.texCoord = in.texCoord
  
  ^ out
}
- fragment in:       ColorInOut as stage_in,
           uniforms: Uniform(0),
           colorMap: texture2d<half>(0)) {

  let colorSampler = sampler(mip_filter::linear,
                             mag_filter::linear,
                             min_filter::linear)

  let colorSample  = colorMap.sample(colorSampler, in.texCoord.xy)
  
  ^ float4(colorSample)
}

```
(phong's vertex and fragment shaders are groupped, so accessing them, groupping them makes things simplier, syntax may change in the future)

Struct example:

```Swift
struct StructName {
  float4 position : POSITION;
  float2 texCoord : TEXCOORD0;
};
```

I'll update the syntax proposal over time.
