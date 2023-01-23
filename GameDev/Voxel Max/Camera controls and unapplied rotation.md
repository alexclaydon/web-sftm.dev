_Stub_

Pending the introduction of "global" camera control mode when in object edit mode.

%%You can't "apply" scale or transforms in Voxel Max as you would in Blender.  For the purposes of exporting to your DCC, you'll need to take steps to address that before proceeding to cleaning.  Se[](Handling%20Voxel%20Max%20unapplied%20transforms.md)]].

However, there is one modeling scenario in Voxel Max where the inability to apply rotation, in particular, can have an undesirable effect on camera controls.  Camera controls - including orbit - are relative to the selected object.  For un-rotated objects, camera controls will be aligned with the scene "ground" plane, which is usually what you want.  However, when you're modeling multi-object meshes, you may find yourself in a situation where your "sub"-meshes are rotated away from your "main" object.

When modeling a car, for example, the car body may be at 0 degrees rotation on all axes and aligned with the scene ground plane.  If you find yourself in a situation of needing to import your wheels from another model file, though - perhaps your asset library - they may need to be rotated to fit correctly in your car body's wheel arches.

With voxels in particular, it is almost always preferable to rotate a mesh as a complete object, in-scene, rather than trying to do it in edit mode, which amounts to rotating each individual voxel relative to each other and usually produces artifacts you are unlikely to want.  They are fundamentally different operations.

However, rotating your object in scene mode results in your camera controls also ending up rotated away from the scene ground plane when you enter edit mode on that object.  This means that as you move between meshes to edit them, your camera controls will change too.

I find this disorienting.%%

