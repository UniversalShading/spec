# Proposed Syntax 

---

#### Goals

* Easy to read
* Easy to write
* Easy to remember

Compiler is in progress, so this syntax may be changed over time. The whole language syntax and rules will be published later

---

Referenced Metal Shader (Vertex)

```metal
vertex ColorInOut vertexShader(Vertex             in [[stage_in]],
                               constant Uniforms& uniforms [[ buffer(0) ]]) {
    ColorInOut out;

    float4 position = float4(in.position, 1.0);
    out.position    = uniforms.projectionMatrix * uniforms.modelViewMatrix * position;
    out.texCoord    = in.texCoord;

    return out;
}

fragment float4 fragmentShader(ColorInOut         in [[stage_in]],
                               constant Uniforms& uniforms [[ buffer(0) ]],
                               texture2d<half>    colorMap [[ texture(0) ]]) {
    constexpr sampler colorSampler(mip_filter::linear,
                                   mag_filter::linear,
                                   min_filter::linear);

    half4 colorSample   = colorMap.sample(colorSampler, in.texCoord.xy);

    return float4(colorSample);
}
```

USL (Universal Shading Language):
```Swift
@vertex 
vertexShader(in: Vertex as stage_in, uniforms: Uniform(0)) -> ColorInOut {
  var out = ColorInOut()
  
  let position = float4(in.position, 1.0)
  out.position = uniforms.projectionMatrix * uniforms.modelViewMatrix * position
  out.texCoord = in.texCoord
  
  return out 
}

@fragment 
fragShader(in:       ColorInOut as stage_in,
           uniforms: Uniform(0),
           colorMap: texture2d<half>(0)) -> float4 {

  let colorSampler = sampler(.linear, linear, .linear)
  let colorSample  = colorMap.sample(colorSampler, in.texCoord.xy)
  
  return float4(colorSample)
}

```

I'll update the syntax proposal over time.
