# Developer console

To activete it, go to Settings -> Other -> Debug Menu, it uses some resources when active <br>
Standard activation on F12 key, but you can change it in Setting -> Controls -> ("Other" section) -> Open Debug Menu

It has 4 tabs:
 - Console
 - Hierarchy
 - Registered classes
 - Rpc registry

## Console

Just log output, if you are server (singleplayer also counts) you can type lua into the input field and invoke it.

## Hierarchy

Here we have left and right sides. On the left side you have a hierarchy of nodes (as in the godot editor), you can click on each node, and if it has a lua table binded, it will be shown in the inspector on the right.

## Registered classes

Just list of registered classes, which was added here by `game.RegisterClass(name, table, baseClass)`. Shown in style `<ClassName> | Base type: <baseClass>`

## Rpc registry

Shows all rpc call from all RpcNodes, shows in style `SenderId | FunctionName | NodePath | Size`<br>

- SenderId - peer id of sender, server is always 1
- FunctionName - which function was called
- NodePath - path to node, which was binded to RpcNode by `rpcNode:BindTable(table)`
- Size always shows in bytes