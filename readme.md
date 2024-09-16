# What is this?
This plugin allows you to "record" frames, storing user defined data for each frame and replaying it later. Allowing far easier debugging in situations where breakpoints or printing isn't sufficient.
# Why would I want this?


# How to use


- Add Navmesh to scene with runtime generation set to dynamic


- reserved keywords (Class, Direction, etc)
- FBFHide (Useful on position, rot, meshpath etc) Only possible in c++

# C++
1. Create class inheriting from UFBFData
2. Create properties for the data you want to save
    (You can add the FBFHide meta tag to hide this property in the debug view)
3. Inherit IFBFDebugActor on the Actor you want to save.
    (If its the root object, override IsRoot() and return true.)
4. Override GetDebugFrame() 
5. In GetDebugFrame() create an instance of your class and assign its properties and return it
## Defining an Actor
1. 
# Blueprint
1. Create object inheriting from UFBFData
2. Create properties for the data you want to save (Tip: Tick expose on spawn).
3. Create component inheriting from UFBFDebugComponent
3. Override GetDebugFrame()
    (If its the root object, override IsRoot() and return true.)
4. In GetDebugFrame() create an instance of your UFBFData class, assign its properties and return it.
5. Add the component to an actor.

# Reserved keywords
Some property names are in use by the plugin. Avoid using these when defining your own properties.
 // They aren't reserved. But the user may not define it with a different type
-- Don't inherit from interface in blueprint. Will cause crash. 