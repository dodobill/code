# 二叉树

## 156. 上下翻转的树

后序遍历

```java
public class Main {
      class TreeNode {
          int val;
          TreeNode left;
          TreeNode right;
          TreeNode() {}
          TreeNode(int val) { this.val = val; }
          TreeNode(int val, TreeNode left, TreeNode right) {
              this.val = val;
              this.left = left;
              this.right = right;
          }
      }

    public TreeNode upsideDownBinaryTree(TreeNode root) {
        TreeNode tr = null;
        if (root==null) return null;
        if (root.left==null&&root.right==null) return root;

        if (root.left!=null) tr = upsideDownBinaryTree(root.left);
        if (root.right!=null) upsideDownBinaryTree(root.right);

        root.left.left = root.right;
        root.left.right = root;
        root.left = null;
        root.right = null;
        return tr;

    }
    
    public static void main(String[] args) {

    }
}
```

