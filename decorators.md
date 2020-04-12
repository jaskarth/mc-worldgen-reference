# Decorators
Minecraft uses `Decorator`s to find the positions for `Feature` generation. This document will explain the behavior of these Decorators and help you choose the best one for your Feature.

# Count Decorators
Count decorators try to generate `count` number of times in a chunk, with different rules. The value for `count` is provided by the `CountDecoratorConfig`. The x and z values provided by these all follow the same format, being a random position within the chunk.

## `COUNT_HEIGHTMAP`
`COUNT_HEIGHTMAP` (in `CountHeightmapDecorator.java`) is the most basic Decorator - it will provide `count` positions at the top of a chunk. This position is above any non-air block.

## `COUNT_TOP_SOLID`
`COUNT_TOP_SOLID` (in `CountTopSolidDecorator.java`) does almost the exact same thing as `COUNT_HEIGHTMAP`, but provides positions above opaque and solid blocks.

## `COUNT_HEIGHTMAP_32`
`COUNT_HEIGHTMAP_32` (in `CountHeightmap32Decorator.java`) provides `count` positions, but the y-value of the position is a random range between `[0, <height> + 32)`. This means the position can be anywhere in the chunk from bedrock to 32 blocks above the topmost block in the chunk. This Decorator is used for providing places for grass and flowers to generate.

## `COUNT_HEIGHTMAP_DOUBLE`
`COUNT_HEIGHTMAP_DOUBLE` (in `CountHeightmapDoubleDecorator.java`) is very similar to `COUNT_HEIGHTMAP_32` but it's y-value is a random range between `[0, <height> * 2)`. This means the position can be anywhere from bedrock to the height of the chunk doubled. This Decorator is used for grass, like the prior one, but berry bushes as well. Grass generation from this decorator is less common compared to `COUNT_HEIGHTMAP_32` because of the larger range.
