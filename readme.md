<h1 style="text-align:center;">C++</h1>

[Blueprint](Blueprint.md)

# What is this?
This plugin allows you to "record" frames, storing user defined data for each frame and replaying it later. Allowing far easier debugging in situations where breakpoints or logging isn't sufficient.
# Why would I want this?
This plugin is designed to help debug problems where traditional breakpoints or logging methods are insufficient. Often, pausing the application with a breakpoint disrupts the test case, and logging every relevant value becomes too messy.

For example if the player throws a grenade but you notice that after a bit, the trajectory seems off. Debugging this can be challenging since setting breakpoints is impractical without knowing exactly when the issue occurs. Although logging velocity and other relevant data each frame is an option, it often results in an overwhelming amount of convoluted data to sift through. With this plugin you can easily record the velocity and any other relevant data and replay it later frame by frame to see exactly when and how it goes wrong.

# How to use
This plugin consists of two core parts: the root frame and the actor frame.
The root frame is where you store any global variable you want to track, for example the frames DeltaTime.
The actor frame is where you store any variable specific to a certain actor. By creating an actor frame, the actor is drawn out in the debug scene and you can select it and view its properties at any time.

## Create Root Frame
1. Create class inheriting from UFBFData
2. Create properties for the data you want to save
    > All Properties must be marked as UPROPERTY()
    
    > Supported types are FString, int, float, bool, FVector, FLinearColor, FBFDrawableArrow, FBFDrawableBox and FBFDrawableSphere
3. (Optional) Create the Actors array (TArray<UFBFData*> Actors)
    > The Actors array is automatically filled with actors in the scene. You do not manually fill it.

    ![FrameExample](Assets/FrameExample.png)

4. Inherit IFBFDebugActor on any singleton (Gamemode, PlayerController, etc)
5. Override IsRoot() and return true
6. Override GetDebugFrame() 
7. In GetDebugFrame() create an instance of your class and assign its properties and return it

## Create Actor
1. Create class inheriting from UFBFData
2. Add any other properties you want to track

### Required Properties 
1. Position (FVector)
2. Name (FString)
    > Name must be unique for that actor.

    > You can add the FBFHide meta tag to a property to hide it in the debug view

### Optional Properties
1. Extents (FVector). If not set, will just spawn with (1,1,1) scale
2. MeshPath (FString). If not set, will spawn a generic cylinder
3. Inherit IFBFDebugActor on the actor you want to track 
4. Override GetDebugFrame()
5. Construct your UFBFData object, set its properties and return it.

## Drawable classes
FBFDrawableArrow, FBFDrawableBox and FBFDrawableSphere are custom classes that will be drawn out in the scene if added as a property in a frame class.
> Instances of these classes are created with their static Create() Function.

## Navmesh
By adding a navmesh to the scene and setting 'Runtime Generation' to Dynamic the navmesh will automatically be saved and displayed in the debug scene.
> Runtime Generation is set on the RecastNavmesh.

> Navmesh can't be saved if the plugin path has a whitespace in it.

## Start/Stop Record
Start recording by using the command FBF.StartRecord and stop recording with either FBF.StopRecord or by exiting PIE.

With the bRecordOnStartUp Project setting, it will automatically start recording on start.

## Reserved keywords
Some property names are reserved for use by the plugin. These can be reused, but not with the wrong type.
- Position (FVector)
- Name (FString)
- Extents (FVector)
- MeshPath (FString)
- Origin (FVector)
- Direction (FVector)
- Color (FLinearColor)
- ArrowLength (float)
- Radius (float)
- Segments(int)

Property names that you add to a frame class may also be reused, but not with a different type.

