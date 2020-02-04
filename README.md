# Lowest Common Ancestor of a Binary Tree
## https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

```
Note:

1. All of the nodes' values will be unique.
2. p and q are different and both values will exist in the binary tree.
```

## Implementation :

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null)
            return null;
        TreeNode leftSearchResult = lowestCommonAncestor(root.left, p, q);
        TreeNode rightSearchResult = lowestCommonAncestor(root.right, p, q);
        
        if (root.val == p.val || root.val == q.val)
            return root;
        if(leftSearchResult != null && rightSearchResult!= null )
            return root;
        return leftSearchResult != null? leftSearchResult : rightSearchResult;
    }
}
```

# References :
https://www.youtube.com/watch?v=py3R23aAPCA

