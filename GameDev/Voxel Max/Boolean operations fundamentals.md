Boolean tools, or "booltools", are meshes of arbitrary shape, the sole purpose of which is to shape other meshes using destructive boolean operations in ways that would be difficult or inconvenient with other tools.  Boolean operations can be performed with the `Combine` tool in Voxel Max.

In order to support boolean operations, tool mesh(es) either must be at the same level of the Outliner tree as the Active Object, or attached - either directly or indirectly - to a group object that is.  Nested grouping is possible, provided that the ultimate root group to which the tool meshes are attached is on the same level as the Active Object.  See [[Sculpting details with booleans and the Combine tool]] for further discussion.

The following assumes an understanding of what the Active Object is in Voxel Max,[^1] and how to select it,[^2] although note that only in the case of a `Subtract` operation does it actually matter which object you choose as your Active Object.  Note also that it doesn't matter in which order you add other objects to your selection in any of the following operations.

## Union

The `Combine - Union` operation is easy to understand - not least because it doesn't really matter which object you have selected as the Active Object.  This operation retains all voxels of each selected object[^3], and combines the selected input objects into a single new object.

To perform this operation, add all relevant objects to your selection.  Right click either on any such object in the outliner, or on the white selection circle visible in the viewport, and choose `Combine - Union`.

## Subtract

Referred to in some other DCCs as a `Difference` boolean, the `Combine - Subtract` operation removes _from the Active Object_ any voxel overlapping in scene space with a voxel of any other selected object.  Note that accordingly, your choice of Active Object matters to your results.  It is possible to perform this operation on the Active Object using multiple tool meshes at the same time.

To perform this operation, make the volume you want to cut into the Active Object.  Add to the selection any objects you want to use as tool meshes.  Right click on any of these objects in the outliner, or on the white selection circle visible in the viewport, and choose `Combine - Subtract`.

## Intersect

In an `Intersect` operation, each voxel of the Active Object will be retained only if it shares scene space with a voxel from at least one other object.  It is possible to perform this operation using two or more objects.  As with the `Union` tool, the nature of this operation means that which object you choose to be the Active Object is arbitrary.  

To perform this operation, add all relevant objects to your selection.  Right click on any of these objects in the outliner, or on the white selection circle visible in the viewport, and choose `Combine - Intersect`.

For tips on using `Combine - Intersect` in a reference modeling workflow in Voxel Max, see [[Sculpting from reference images with Combine - Intersect]]. 

_Last update: 16 Jan 2023_

[^1]: See [[The Active Object]].
[^2]: See [[Using the Select tool on Mac]].
[^3]: Strictly speaking, it removes "doubled" geometry from objects which have voxels sharing the same scene space.