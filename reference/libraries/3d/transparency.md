# Transparency
Transparency and 3d rendering with depthbuffer is a tricky topic that isn't completely solved for the general case. The only thing you can do is to find the right rendering technique that suits your specific setup.

## Materials
The Stride render system has a render stage for transparent objects. This render stage is called directly after the normal opaque stage. In the transparent stage objects that have a transparency feature connected to the material get rendered. These objects usually only read from the depth buffer and blend themselves over the scene with additive or alpha blending.

There are 3 different transparency features: **Blend**, **Additive**, or **Cutoff**. See the 
[Stride Material doc](https://doc.stride3d.net/4.0/en/manual/graphics/materials/misc-attributes.html#transparency) for a detailed description of these modes and their parameters. You can find the nodes for these material features in the node browser in the category `[Materials.MiscAttributes.Transparency]`.

**Caution:** If an object gets moved into the transparent render stage by the render system, it will not write into the depth buffer anymore. This means that it will not occlude other objects.

## Custom rendering
If you render your own cusom shaders, you can control the blending and the interaction with the depth buffer via the nodes `BlendStateDescription` + `BlendStateRenderTargetDescription`  and `DepthStencilStateDescription`. The node RenderEntity also offers the possibility to specify the render stage, see [Rendering](rendering.md).

There are also preconfigured blend states like `Additive`, `AlphaBlend` and `AlphaBlendPremultiplied` in the category `[BlendStateDescription]`.

For further reading on this topic and the related problem, you can have a look at the [vvvv beta documentation](https://vvvv.org/documentation/transparency).
