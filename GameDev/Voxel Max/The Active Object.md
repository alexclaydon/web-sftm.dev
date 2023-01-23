Voxel Max uses the concept of an "Active Object" to, in general terms, distinguish the object on which operations will be performed, from other objects which may be selected (for example, in a multi-object operation such as booleans).[^1]  This includes any object currently being edited.  There cannot be more than one Active Object at any time, but a group can be an Active Object.

You may be referred back to this note from other contexts where the identity of the Active Object is significant to the operation you are trying to perform.

In addition to understanding the significance of the Active Object, it is helpful to understand how it is selected:
- Entering edit mode on an object makes it the Active Object.
- Left-clicking an object in the viewport makes it the Active Object.
- Left-clicking an object in the outliner will only select it, without making it the Active Object.
- Soon, you will be able to CMD + left-click an object in the outliner to make it the Active Object.

In addition to the above, you can also right-click an object in the outliner and make that object into the Active Object with `Selection` -> `Select Item`.

A corollary to the above is that:
- If you are selecting multiple objects from the viewport using either `Select - Expand`, or `Select - New` with the `Shift` key modifier[^2], the last object you add to your selection will be the Active Object.
- On the other hand, selecting multiple objects from the outliner (whether in the `Expand` or `New` select mode) will have no effect on which object is the Active Object.  In this case, if you don't have an Active Object already selected, you may end up with multiple objects selected but no Active Object, which may lead to undesirable results in multi-object operations (such as with the `Combine` tool).[^3]  Better to ensure you choose your Active Object (by clicking first in the viewport, for instance, or by CMD + left-clicking it in the outliner) before selecting your other objects.

_Last update: 17 Jan 2023_

[^1]: See [[Boolean operations fundamentals]].
[^2]: See [[Using the Select tool on Mac]].
[^3]: See [[Boolean operations fundamentals]].