In a gamedev pipeline, in particular, reusing materials when modeling in Voxel Max can be a huge time-saver.

Since you have to rebuild final materials from scratch in-engine anyway,[^1] materials that you use in Voxel Max serve as dummy / proxy materials, marking out parts of your model for their own "material slot" in the game engine, to which final materials can be applied.  Accordingly, their PBR characteristics do not need to be perfect - an approximation that lets you eyeball what your model will approximately look like in-engine is sufficient.

This means that you can potentially get away with using one "dummy" palette across a huge number of models.

While Voxel Max does not currently directly support materials export / import between scene files (or between objects), there is a workaround: create a new file containing a dummy empty "materials object", attaching materials tailored to the type of modeling you're doing, then import it into each new scene.[^2]  Since materials (and palettes) are per-object in Voxel Max, for each new object you model, simply duplicate the dummy object and start modeling from there.

[^1]: See [this excellent Blender StackExchange post](https://blender.stackexchange.com/questions/57531/fbx-export-why-there-are-no-materials-or-textures) for more information.
[^2]: See [[Creating an asset library]] for details of the import process.