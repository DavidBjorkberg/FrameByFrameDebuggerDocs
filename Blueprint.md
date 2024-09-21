[Blueprint](Readme.md)
# How to use
## Create Root Frame
1. Create class inheriting from UFBFData
2. Create properties for the data you want to save (Tip: Tick expose on spawn).
3. Create component inheriting from UFBFDebugComponent
3. Override GetDebugFrame()
    (If its the root object, override IsRoot() and return true.)
4. In GetDebugFrame() create an instance of your UFBFData class, assign its properties and return it.
5. Add the component to the actor you want to track.
## Defining an Actor
1. Create class inheriting from UFBFData
2. Add any other properties you want to track
> Supported types are FString, int, float, double, bool, FVector, FLinearColor
### Required Properties 
1. Position (FVector)
2. Name (FString)
### Optional Properties
1. Extents (FVector)
2. MeshPath (FString)

3. Create a component inheriting from UFBFDebugComponent 
4. Override GetDebugFrame()
5. Construct your UFBFData object, set its properties and return it.


# Navmesh
By adding a navmesh to the scene and setting 'Runtime Generation' to Dynamic the navmesh will automatically be saved and displayed in the debug scene.
    Note: Runtime Generation is set on the RecastNavmesh.
    Note: Can't save if the plugin path has a whitespace in it. (Can i remove the whitespace?)

# Reserved keywords
Some property names are in use by the plugin. Avoid using these when defining your own properties.
 // They aren't reserved. But the user may not define it with a different type
-- Don't inherit from interface in blueprint. Will cause crash. 