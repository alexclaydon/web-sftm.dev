The following is a checklist (i.e., it contains process, but is light on explanation for the sake of brevity) covering how to take a model made in Voxel Max all the way through to your 3D game engine for use as either a static or skeletal mesh.

For further discussion on challenges in preparing voxel-art models for use as skeletal meshes with 3D game engines, see [[Particular challenges involved in using voxel-art models as skeletal meshes in 3D game engines]].

## Voxel Max
- When modeling organic characters intended for in-engine use as skeletal meshes:
	- for humanoids, use either the T or A-Pose
	- for non-humanoids, use an analogous pose to simplify rigging later on
	- use separate appendages (limbs, head); this will help you retain vertices where you'll need them later for deformation
- Use separate objects to establish correct separation between non-deforming parts of the model that may require independent relative orientation to other parts - either as a skeletal mesh with rigging, or a static mesh with several different "poses"
	- some examples would be car doors, wheels, bonnet
	- you do not need to use separate objects for mesh parts intended for deformation
- Avoid using groups in Voxel Max for your first run through this pipeline
- Although you will need to create materials from scratch in your game engine,[^1] you should nevertheless apply "dummy" materials in Voxel Max
	- the groups of vertices constituted by these materials will form the basis of your in-engine mesh material slots, greatly simplifying application to your mesh in-engine
	- the textures baked for each such material in Blender will be suitably scaled for drop-in use in your in-engine materials, allowing you to easily retain the painted colour detail of your model 
	- assuming you are using a PBR pipeline, you might also like to ensure that the PBR characteristics of dummy materials in Voxel Max roughly approximates what you intend to recreate in your game engine; while not strictly speaking necessary, this will allow you to use Voxel Max's ray-tracing renderer to eyeball an approximation of how your materials will look like in-engine
- Under `Settings` -> `Meshing Algorithm`, ensure that `Textured - Naive` is selected
	- this will aid with non-manifold geometry, but incurs an additional triangle cost; we will address that next in Blender
- You may have unapplied scale transforms on one or more of your objects; that's no problem.  See [[Handling Voxel Max unapplied transforms]] for more information.
- Export either the scene, or just your model objects, in the `Khronos GLTF` format.

## Blender
- The following is tested on Blender 3.3 LTS.
- Ensure that the following plugins are downloaded, installed and enabled:
	- Vox Cleaner v2 or above - for cleaning voxel geometry
	- and, for skeletal meshes:
		- Rigify - Blender's recommended rigging library
		- Game Rig Tools - for creating game-ready rigs
		- if available, the correct Game Rig Tools module for your game engine (in my case, Game Rig Tools - Unreal Module)
- Under `File` -> `External Data`, enable `Automatically Pack Resources`
- Use `File` -> `Import` - `gltf 2.0` with the default settings to import your Voxel Max model
- Under `Show Overlays` icon, enable `Statistics`
- Select your mesh (or, if you have multiple meshes constituting a single entity, select the `empty` group to which they are attached)
- Clear Parent and Keep Transformation: Hit F3 and select `Object` -> `Parent` -> `Clear and Keep Transformation`
- Delete the empty `previewRootNode` and anything attached to it
- Select the mesh (or group)
- Change rotation mode from `Quaternion` to `XYZ Euler`
- Rename your object(s) with something meaningful; the names set here will carry throughout the rest of the pipeline
- Decide where you want your model origin to be; situate the model so that your desired origin is on the 3D cursor, which should still be located at the scene origin.
- Select the object, hit F3 then select `Set origin to 3D cursor`
- Scale your object to your desired in-engine size
	- this will depend on what engine you are using; trial and error will help here
	- hit the `n` key and select the `Item` tab; for Unreal Engine, you should consider the dimensions visible here here a good approximation for "real-world" size
	- highlight all of the X, Y, Z scales, which should currently be 0.1, and replace it with your scaling factor
		- for Unreal Engine, for example, for a human character, if your height in this panel is 4m, then assuming your model's proportions are correct, changing scaling factor from 0.1 to 0.04 will give you an approximately human-sized (i.e., the size of UE's default mannequin character) model in Unreal Engine
- Hit Ctrl + A, then `Apply` -> `All Transforms`
- Your model should be located at origin, resting on the floor, and facing -Y direction
- If you have used separate appendages and intend for your model to be used as a skeletal mesh, now is the time to reconstitute those appendages
	- enabling `Snap To` -> `Vertex` will help with this operation
	- but be careful not to move your model off its origin
	- disable `Snap To` -> `Vertex`  when finished
	- note that this approach will leave you with inner faces, which can be selected with F3, `Select` -> `Select All by Trait` -> `Interior Faces`
		- whether you want that is outside the scope of this checklist; if you don't want them, now is the time to remove them
- Next, we'll clean the geometry and bake textures using Vox Cleaner v2 or above:
	- keep in mind that the free version of Vox Cleaner will not preserve emissive materials
		- we will be re-building materials from scratch in-engine anyway
		- but you should ensure that any surfaces intended to be emissive have their own emissive dummy material applied after cleaning, otherwise they will have no separate material slot in-engine
	- for each mesh object in scene, select it, press the `n` key, the under the `Vox Cleaner` panel, on the `Lazy Clean` preset, select `Clean Model`
	- note the reduction in triangle count in the viewport `Statistics` display enabled earlier
	- note that Vox Cleaner does not prepare lightmap UVs; if your engine requires them, they should be done either in Blender or in-engine
- For skeletal meshes intended for deformation (such as organics), now is the time to consider adding back specific geometry to ease deformation
	- the cleaning process will likely not leave you with enough geometry for good deformation; this is to some extent an unavoidable incident of a rectilinear voxel-art style
	- edge loops are the preferred tool here, but you can't use that on n-gons, which you will have; the knife tool helps here
- Ensure that each part of your model has a suitable dummy material; any emissive surfaces in particular will need to be manually re-allocated here
- Do a final check for bad normals and non-manifold geometry:
	- under the `Show Overlays` icon, enable `Face Orientation` and recalculate normals if necessary
	- In edit mode, using the `Select` -> `Select All by trait` -> `Non-Manifold` tool, confirm that there's no non-manifold geometry (there shouldn't be)
- If intended for use as a skeletal mesh in-engine, now is the time to rig your mesh
	- rigging is heavily dependent on what you're trying to achieve and is outside the scope of this checklist
	- I use and recommend the Game Rig Tools add-on for Blender, and will have a separate post up in future covering how to rig a humanoid mesh for export to Unreal Engine
- If you still have separate sub-meshes, consider combining them into a single model mesh prior to export to your game engine
	- whether this is appropriate depends on what you're trying to achieve
	- note that this operation is destructive; for my workflow exporting to Unreal Engine, it is also not necessary, since Epic's `Send2UE` tool has an option to non-destructively join child meshes as part of the export process
- Export your mesh to your game engine; the process will be particular to your engine
	- I'll have a separate post up in future on exporting to Unreal Engine

[^1]: See [this excellent StackExchange post](https://blender.stackexchange.com/questions/57531/fbx-export-why-there-are-no-materials-or-textures) for further explanation.