## Prepearing tower scene

> Please, read [Loading scenes](pages/loading_scenes.md) first

When you filled [tower config](pages/towersconfig.md) you maybe had a question, how you need to set metafield properly.

As you may know after reading [Loading scenes](pages/loading_scenes.md) you can add metadata `baseLuaClass` and node will become this class

So to create tower add to the root `baseLuaClass`(string) and write your tower lua class.

Also add **`placementArea`** (`NodePath`): **Required** - The zone, which tower will take on placement, needs to check is avalible to place it. This must be a valid `Area3D` node.

So other metadata just will add field into binded lua table