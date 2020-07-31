# Proposed Syntax 

Referenced Metal Shader (Vertex)

```metal
vertex ColorInOut ShaderName(Vertex in [[stage_in]],
                             constant Uniforms & uniforms [[ buffer(BufferIndexUniforms) ]]) {
    ColorInOut out;

    float4 position = float4(in.position, 1.0);
    out.position    = uniforms.projectionMatrix * uniforms.modelViewMatrix * position;
    out.texCoord    = in.texCoord;

    return out;
}
```

USL (Universal Shading Language):
```Swift
[ShaderName]
vertex ColorInOut (in: Vertex) {
  var out: ColorInOut
  
  let position = float4(in.position, 1.0)
  out.position = uniforms.projectionMatrix * uniforms.modelViewMatrix * position
  out.texCoord = in.texCoord
  
  ^ out
}
```

I'll update the syntax proposal over time.
