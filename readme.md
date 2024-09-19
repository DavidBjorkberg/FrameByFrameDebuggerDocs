# What is this?
This plugin allows you to "record" frames, storing user defined data for each frame and replaying it later. Allowing far easier debugging in situations where breakpoints or printing isn't sufficient.
# Why would I want this?


# How to use

# C++
![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)
## Create Root Frame
![Test](Assets/Test.png)
1. Create class inheriting from UFBFData
2. Create properties for the data you want to save
    Note: All Properties must be marked as UPROPERTY()
3. Inherit IFBFDebugActor on any singleton (Gamemode, PlayerController, etc)
4. Override IsRoot() and return true
4. Override GetDebugFrame() 
5. In GetDebugFrame() create an instance of your class and assign its properties and return it
6. Optional: Add an array of UFBFData* called Actors

## Create Actor
1. Create class inheriting from UFBFData
2. Add any other properties you want to track

### Required Properties 
    1. Position (FVector)
    2. Name (FString)
    (You can add the FBFHide meta tag to a property to hide it in the debug view)

### Optional Properties
    1. Extents (FVector). If not set, will just spawn with (1,1,1) scale
    2. MeshPath (FString). If not set, will spawn a generic cylinder
    Note: All Properties must be marked as UPROPERTY()
3. Inherit IFBFDebugActor on the actor you want to track 
4. Override GetDebugFrame()
5. Construct your UFBFData object, set its properties and return it.

# Blueprint
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
### Required Properties 
    1. Position (FVector)
    3. Name (FString)
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


# TODO
1. Reserved keywords section
2. Supported types
3. Tip: If you remove UPROPERTY() from a property it will no longer be saved (Maybe useful?)
4. How to start / stop record
5. How to launch debug play
6. Find a better word for "debug Scene"
7. Add pics
