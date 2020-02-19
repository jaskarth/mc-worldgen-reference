# Biome Layers
Biome layers are used to place biomes based on a voronoi tesselation. This reference sheet will talk about new biome layers (1.13+) and will use Fabric's Yarn names. If you are using Forge's MCP names, please see the attached MCP2Yarn conversion document.

## CoordinateTransformer
CoordinateTransformer specifies a way to change the given x and z coordinates.

### Uses
`IdentityCoordinateTransformer`, `NorthWestCoordinateTransformer`, `ScaleLayer`

### When to use this
All biome layers use this, usually you would want to use `IdentityCoordinateTransformer` unless you are scaling layers, in which case you should override this and use a bit shift.

## InitLayer
InitLayer is used to initialize a layer with values for operation by further layers.

### Uses
`ContinentLayer`, `OceanTemperatureLayer`

### When to use this
Whenever you need to start a new layer, this is the layer you will need to use. The layer is passed in an x and z coordinate and is asked to return an int representing the biome ID. The `ContinentLayer` uses this to initialize the plains/ocean distribution, which is then changed to include all of the biomes later.

## ParentedLayer
ParentedLayer is the default layer that provides the implementation for sampling at a given x and z coordinate. ParentedLayer will be at the core of every layer after the initlayer. 

## IdentitySamplingLayer
IdentitySamplingLayer gives you a biome id sampled at the given x and z coordinate.

### Uses
`AddClimatesLayer.AddSpecialBiomesLayer`, `SetBaseBiomesLayer`, `SimpleLandNoiseLayer`

### When to use this
IdentitySamplingLayer is good for replacing biomes at specific areas regardless of the neighboring biomes. For example, you could write an IdentitySamplingLayer to return a biome variant randomly for a given biome. Other examples: [Ecotones' special biome layer](https://github.com/SuperCoder7979/ecotones/blob/master/src/main/java/supercoder79/ecotones/layers/generation/BaseSpecialBiomesLayer.java) and [Ecotones' volcanism layer](https://github.com/SuperCoder7979/ecotones/blob/master/src/main/java/supercoder79/ecotones/layers/generation/VolcanismLayer.java)

## CrossSamplingLayer
CrossSamplingLayer is a layer that provides the biome ID for the north, east, south, west, and center (the given x and z coordinate). A way to visualize this is by thinking of a 3x3 chessboard with a rook/castle in the middle. All the places that the rook could move is where the CrossSamplingLayer samples, including the place the rook is.

### Uses 
`AddClimateLayers.AddCoolBiomesLayer`, `AddClimateLayers.AddTemperateBiomesLayer`, `AddDeepOceanLayer`, `AddEdgeBiomesLayer`, `AddIslandLayer`, `EaseBiomeEdgeLayer`, `NoiseToRiverLayer`, `SmoothenShorelineLayer`

### When to use this
CrossSamplingLayer is good for checking whether the given center is surrounded by biomes, and for checking biome proximity. For example, Minecraft uses this to place deep oceans if all of the biomes to the sides are ocean.
