See [[Boolean operations fundamentals]] and [[Creating an asset library]] first.

A common hard-surface modeling workflow involves using boolean tools to create model details.  You can create your own sets of useful boolean tools in Voxel Max[^1] - either in your project scene file itself, or in a separate scene file which can then be imported into your project scene as an asset library[^2] - and use them together with Voxel Max's `Combine` tool,[^3] both for sculpting and to add details to your meshes.

## Boolean operations using voxels on non-Euclidean geometry

For most voxel densities, attempting to use two voxel art-style meshes with non-Euclidean relative rotation to one another in a boolean union or subtract operation is likely to produce undesirable results.  Even in cases where there is only one tool mesh operating on one model mesh, at all but the very highest voxel densities you are likely to end up with jagged seams in your model mesh.  The effect is heightened when using multiple instances of the same tool mesh at varying angles, as the shapes of the seams at each site of the operation will likely be inconsistent, as well as ugly.

![[Publish/zImages/booltools-non-euclidean.png]]

In the context of a game art pipeline, this may be particularly problematic as you may not be able to hide the seams with, for example, camera placement, and the player camera may get close to your mesh.  Wheels are a special example in that they may have not only lots of non-Euclidean detail geometry owing to their shape, but may also need to rotate in-game.

If you intend to perform lots of boolean operations on non-Euclidean geometry, you might like to consider modeling that part of your model with polygons instead.

## Preparing your boolean tools

As boolean operations are destructive, unless they are destined for one-off operations, it's usually worth keeping your tool meshes in a separate library file from where they can be instanced on import and used destructively, but remain available for re-import in future projects.

Assuming you choose to do this, each top level object in your library file will be available for import in the project scene as a discrete object.  This means that you can import not only single-mesh boolean tools, but also groups of meshes, and that when preparing your asset library, you can arbitrarily nest additional groups and meshes within any top level group for later convenience.

Whether to group your booltools in your asset library file prior to exporting to your scene file depends entirely on what you're trying to achieve.  Some good rules of thumb might be that:
- if a given tool mesh is intended to be used in a spatial grouping together with either instances of itself, or with other tool meshes, grouping those meshes together can facilitate the retention of the correct number of clones and relative transforms inside the group; and
- for tool meshes intended for use as part of a larger group of tool meshes, consider grouping meshes together by the operation in which they will be used.  Putting all meshes intended for the same operation together can greatly improve legibility and facilitate their use.  Note that you can use such "by operation" groupings at any level of the scene tree and together with the type of grouping referred to above, so for example:

![[Publish/zImages/boolean-nested-grouping.svg]]

One such example is as below: since there are always five leaves to the traditional Fuchs wheel, and since they should always retain their transforms and scale relative to each other, it makes sense to group them together in your asset library, so that they can be used as-is, in-scene, without having to start from a single mesh and recreate the transforms and scale every time they are used.

![[Publish/zImages/fuchs-wheel-bool-grouping.png]]

## Using your boolean tools in-scene

In order to support boolean operations, the tool mesh(es) either must be at the same level of the Outliner tree as the Active Object, or attached - either directly or indirectly - to a group object that is.  Nested grouping is possible, provided that the ultimate root group to which the tool meshes are attached is on the same level as the Active Object.

If some of your imported tool meshes don't fulfill this condition, you'll have to ungroup them prior to use.  That's usually not a big deal in a project scene, where the tool meshes usually only hang around as long as the boolean operation anyway.

See [[Creating an asset library]] for details on the import process.  Once complete, and assuming the above requirement is satisfied, using the imported tool meshes is as simple as putting them where they need to be and invoking the correct boolean operation one by one.  See [[Boolean operations fundamentals]] for more information.

In the context of a details workflow, there is one section of the `Object Properties` panel in particular with which it helps to be familiar: `Pivot`.  See [[The Object Properties panel]] for detail on setting an object's pivot point.

Voxel Max does not currently support arbitrary pivot points external to an object.  For boolean workflows, there are two potentially useful workarounds for this.  Perhaps the better one is to use a larger object workspace, creating space around your actual mesh, and then place a dummy voxel at your intended pivot point, "external" to your mesh, and then set your pivot point on the workspace edge adjacent to it.  Alternatively you can use the `Clone & Move` tool on your mesh _in-place_ to get the desired relative rotation of each boolean instance, then manually move them to where they are required in your project scene, preserving the correct rotation set earlier.  This second approach involves somewhat more guesswork.

_Last update: 17 Jan 2023_

[^1]: See, for example, [[Sculpting curves and curved surfaces with the Line tool]], although as arbitrary meshes, there is no limit to the different ways in which you can create boolean tools.  Note also that on the Voxel Max roadmap is the ability to import generic `.fbx` models and have Voxel Max naively voxelize them.  This would open the door to using imported meshes as booleans, amongst other things.
[^2]: See [[Creating an asset library]].
[^3]: See [[Boolean operations fundamentals]].