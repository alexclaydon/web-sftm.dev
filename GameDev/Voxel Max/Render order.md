The order in which objects are rendered to the screen by Voxel Max's current rendering engine is determined by the object hierarchy, and can be manipulated from the outliner.

You can think of Voxel Max's scene format like a folder structure, ordered as follows:
- arbitrary parent (including, but not limited to, the scene root itself);
- list of groups (sorted); and
- list of objects (sorted).

This may seem esoteric but it has consequences: you may get unexpected results on account of your scene hierarchy.

Here's one example involving the use of reference images and a transparent mesh.

![[Publish/zImages/vm-render-order.png]]

This scene has a flat structure - no hierarchy.  Just a bunch of reference images and the mesh itself, all under the scene root.  The reference image on the left is ahead of the mesh in the render order (situated above it in the outliner), while the image on the right is behind it (situated below in the outliner).  On the left, the mesh is correctly rasterized on top of the reference image; on the right, we have a rasterization error that results in a render that doesn't make sense to the human eye: an opaque image behind a transparent mesh that is nevertheless obscured by it.

Note that as of build 572, Voxel Max automatically gives the active object (in this case, the mesh) priority rendering order, fixing this issue for the purposes of your editing workflow.  You do still need to consider it in the context of how your whole scene fits together outside of editing, though - when viewing in Voxel Max's Presentation Mode, or when rendering out to .png or video.

For more complicated scenes, you may need to set up a suitable scene hierarchy, with the above in mind, in order to ensure you get the render result you intend.  At the moment, there's no drag-drop re-ordering in the outliner (although this may be coming in a future update), so this can be a bit fiddly to get right.

However, for scenarios such as the one above - which contains only a few meshes, all of which (when using a low alpha value) should make visible the reference images behind them - there is an easy workaround: simply select the offending object in the outliner, and cut-paste it (paying attention to any transforms, which you may need to copy across).  It will be deposited at the bottom of the outliner, and will appear correctly when rasterized.

There is one drawback to this workaround, though: for meshes raised off the floor (for example, because you have carved wheel arches out of your car body _after_ starting work), they will lose their vertical transforms upon re-paste; take a note beforehand so that you can manually restore it to preserve relative transforms against any of your other meshes.

_Last update: 11 Jan 2023_