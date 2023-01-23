See [[Boolean operations fundamentals]] first.

Modeling complex objects from reference images placed perpendicular to the X, Y, and Z axes of a scene is a common use-case.  With the introduction of the `Combine - Intersection` tool in beta 580, this is now straightforward.

Drag your reference images into the scene and orient them around the origin as you normally would, so that the schematic visual elements of all three line up in the correct places for the object being modeled.

For each reference image, orient the camera face-on and trace a 2D outline of the section you intend to model using the line tool or free hand tool, whatever is convenient.  See [[Sculpting curves and curved surfaces with the Line tool]] for additional context.  Ensure that each such outline is closed - that is, it has no open sides.  Select the `Face` tool on `Adjacent` only.  Click once inside the line to fill the outline, then extrude the entire face towards the camera - that is, perpendicular to the reference image itself.  You may like to extrude it all the way to the edge of the object workspace (256 cubed, by default) or, if you already have a sense of the depth in that dimension of the object you're trying to model, just ensure it's deep enough that the object will sit wholly inside it.

When finished, you should be left with three overlapping filled volumes clustered about the scene origin.

Select one of these as the Active Object[^1] - in practice, for our purposes it doesn't matter which.  Then add the other two volumes to the selection.  Right click either on the white circle visible in the viewport, or on any of the objects in the outliner and choose `Combine - Intersect`.

This should leave you with a three-dimensionally correct mesh of your reference object.

[^1]: See [[Using the Select tool on Mac]] and [[The Active Object]].