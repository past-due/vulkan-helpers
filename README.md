# vulkan-helpers
Small helper classes for Vulkan C++ apps

- [Requirements](#requirements)
- [VkhInfo](#vkhinfo)
- [VkhRenderPassCompat](#vkhrenderpasscompat)

## Requirements
- C++11 compiler
- Vulkan SDK / headers, with `vulkan.hpp`

## VkhInfo

Output information (inspired by the output of `vulkaninfo`) about Vulkan:
- Instance Extensions
- Surfaces
- Physical Devices

to a specified `outputHandler`.

The `outputHandler` receives a multiline, `\n`-separated string.

## VkhRenderPassCompat

A rough attempt at implementing the rules for determining [Vulkan Render Pass Compatibility](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#renderpass-compatibility).

> Framebuffers and graphics pipelines are created based on a specific render pass object. They **must** only be used with that render pass object, or one compatible with it.

Construct a `VkhRenderpassCompat` by passing in the `vk::RenderPassCreateInfo` used to create
a render pass. `VkhRenderpassCompat` will make a deep copy of the `vk::RenderPassCreateInfo`
information.

A `VkhRenderpassCompat` instance can be compared for compatibility with another via:
`bool isCompatibleWith(const VkhRenderpassCompat& other) const;`

### TODOs:
- Implement proper handling of the `pNext` member of `VkRenderPassCreateInfo`
   - Currently, if `pNext != nullptr`, `VkhRenderPassCompat::isCompatibleWith` will always evaluate to `false`.
- Handle `singleSubpassSpecialCase` _(optimization)_
   > As an additional special case, if two render passes have a single subpass, they are compatible even if they have different resolve attachment references or depth/stencil resolve modes but satisfy the other compatibility conditions.

## License

All helper classes in this repo are distributed under the MIT License.
