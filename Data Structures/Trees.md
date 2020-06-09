##### Trees:
- Wide- parent nodes referencing many child nodes.
- Deep- many parent-child relationships.
- Each time we move from a parent to a child, we’re moving down a level. Depending on the orientation we refer to this as the depth (counting levels down from the root node) or height (counting levels up from a leaf node).
- Useful for modeling data that has a hierarchical relationship which moves in the direction from parent to child. 
- No child node will have more than one parent.
- root: A node which has no parent. One per tree.
- parent: A node which references other nodes.
- child: Nodes referenced by other nodes.
- sibling: Nodes which have the same parent.
- leaf: Nodes which have no children.
- level: The height or depth of the tree. Root nodes are at level 1, their children are at level 2, and so on.

![tree_diagram.png](/Users/admin/Desktop/Screenshots/tree_diagram.png)

##### Binary Search Trees
- Type of tree where each parent can have no more than two children, known as the left child and right child.
- Left child values must be lesser than their parent.
- Right child values must be greater than their parent.