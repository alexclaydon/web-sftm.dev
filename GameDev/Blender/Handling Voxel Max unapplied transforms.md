When using Voxel Max for a game asset development pipeline - especially if you're familiar with other modeling programs such as Blender - you may be wondering about any unapplied scale or transforms on your meshes when it comes time to export to your DCC.

One of the golden rules of game asset modeling seems to be: you should never have unapplied transforms on anything where you consider the current location, rotation and scale of objects to be the default rest position.  This way, if another program or the animator resets the transforms (intentionally, by design or by mistake), you won't lose those transforms in scene space.

In short, you can't "apply" scale or transforms in Voxel Max; but for the purposes of exporting to your DCC, you also don't need to.  When a Voxel Max scene is exported to Blender using the recommended Khronos `.gltf` format, all objects in the scene are parented to a root node called `previewRootNode`.  One of the functions of `previewRootNode` is to hold object scaling and transform information _intact_ (i.e., unapplied) from Voxel Max.  You probably don't want all your meshes arbitrarily paired to an artificial `previewRootNode` object for the next part of your pipeline, so part of the cleaning you do in your DCC should include de-parenting and applying unapplied transforms.

See [[Preparing Voxel Max models for use in 3D game engines]] for a complete checklist covering export of a model from Voxel Max to Blender for use in 3D game engines as either a static or skeletal mesh.

_Last update: 14 Jan 2023_