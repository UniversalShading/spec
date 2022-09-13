# Proposed Syntax 

---

Compiler is in progress, so this syntax may be changed over time. The whole language syntax and rules will be published later

---

Referenced Metal Shader (Vertex)

```metal
typedef struct {
  float3 position [[attribute(0)]];
  float2 texCoord [[attribute(1)]];
} Vertex;

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

struct Vertex {
  position: float3 @attribute(0);
  texCoord: float2 @attribute(1);
}

/* alternative version which groups attributes and reduces attributes */
struct Vertex {
  @attributes {
    position: float3(0);
    texCoord: float2(1);
  }
}

/* this syntax may be improved in the future */
// struct Vertex: apply @attribute {
struct(attribute) Vertex {
  position: float3(0);
  texCoord: float2(1);
}

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

### new proposal

```swift

/* position is at 0, texCoord is at 1 */
vertex Vertex {
  position: float3;
  texCoord: float2;
}

fn sum(a: float, b: float) -> float { 
  return a + b
}

fn sum(a: float, b: float) -> float { 
  a + b
}

fn sum(a: float, b: float) -> a + b

fn sum<T>(a: T, b: T) -> a + b

kern computeShader() -> float4 {

}

vert vertexShader(in: Vertex) -> VertexOut {

}

frag fragmentShader() -> float4 {

}

vert vertexShader(in: Vertex, uniforms: Uniform(0)) -> ColorInOut {
  var out = ColorInOut()

  let position = float4(in.position, 1.0)
  out.position = uniforms.projectionMatrix * uniforms.modelViewMatrix * position
  out.texCoord = in.texCoord

  return out 
}

frag fragShader(in:       ColorInOut as stage_in,
                uniforms: Uniform(0),
                colorMap: texture2d<half>(0)) -> float4 {

  let colorSampler = sampler(.linear, linear, .linear)
  let colorSample  = colorMap.sample(colorSampler, in.texCoord.xy)
  
  return float4(colorSample)
}


```

I'll update the syntax proposal over time.
