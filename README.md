# Lowest Common Ancestor of a Binary Tree
## https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: "The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself)."

### Example :
```
                3
              /   \
             5     1
            / \   / \
           6   2 0   8
              / \
             7   4
```
For the above binary tree :

1. The LCA of nodes 5 and 1 is 3.
2. The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.

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
Note that we are given in the question that both nodes p and q will exist in the binary tree.

### Follow up : What if we are not guaranteed that both nodes p and q will exist in the binary tree?
We are going to take two boolean properties `firstNodeExist` and `secondNodeExist`, and when we find that first or the second node exist in the binary tree, we will set the appropriate boolean property to `true`. This way we can find out whether both the values exist in the tree or not, and if both the values are not found in the binary tree we return `null` as LCA from the `lowestCommonAncestor` method.

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
    public boolean firstNodeExist;
    public boolean secondNodeExist;
    
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null)
            return null;
        TreeNode lca = lca(root, p, q);
        return (firstNodeExist && secondNodeExist)? lca : null;
    }
    
    public TreeNode lca(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null)
            return null;
       
        TreeNode leftSearchResult = lca(root.left, p, q);
        TreeNode rightSearchResult = lca(root.right, p, q);
        if (root.val == p.val) {
        	firstNodeExist = true;
        	return root;
        } else if(root.val == q.val) {
        	secondNodeExist = true;
        	return root;
        }
           
        if(leftSearchResult != null && rightSearchResult!= null )
            return root;
        return leftSearchResult != null? leftSearchResult : rightSearchResult;
    }
}

```

# References :
https://www.youtube.com/watch?v=py3R23aAPCA

