递归写法非常简单，非递归的写法就是要借助栈来模拟递归的过程~ 非递归的格式也是类似的 两个while循环，判断条件也一样，唯一需要注意的就是后序遍历的非递归写法~

1、前序遍历	[二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)
+ 递归代码
```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {

        List<Integer> result = new ArrayList<>();
        dfs(root, result);
        return result;
    }

    void dfs(TreeNode node, List<Integer> result) {
        if (null == node)
            return;

        result.add(node.val);
        dfs(node.left, result);
        dfs(node.right, result);
    }
}
```
+ 非递归代码
```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {

        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;

        while(null != cur || !stack.isEmpty()){
            while(null != cur){
                result.add(cur.val);
                stack.push(cur);
                cur = cur.left;
            }
            cur = stack.pop().right;
        }

        return result;
    }
}
```
2、中序遍历	[二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)	
+ 递归代码
```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {

        List<Integer> result = new ArrayList<>();
        dfs(root, result);
        return result;
    }

    void dfs(TreeNode node, List<Integer> result) {
        if (null == node)
            return;

        dfs(node.left, result);
        result.add(node.val);
        dfs(node.right, result);
    }
}
```
+ 非递归代码
```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;

        while (null != cur || !stack.isEmpty()) {
            while (null != cur) {
                stack.push(cur);
                cur = cur.left;
            }
            cur = stack.pop();
            result.add(cur.val);
            cur = cur.right;
        }

        return result;
    }
}
```
3、后序遍历 [二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)
+ 递归代码
```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {

        List<Integer> result = new ArrayList<>();
        dfs(root, result);
        return result;
    }

    void dfs(TreeNode node, List<Integer> result) {
        if (null == node)
            return;

        dfs(node.left, result);
        dfs(node.right, result);
        result.add(node.val);
    }
}
```
+ 非递归代码
```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {

        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root, pre = null;

        while (null != cur || !stack.isEmpty()) {
            while (null != cur) {
                stack.push(cur);
                cur = cur.left;
            }

            cur = stack.peek();
            if(null == cur.right || pre == cur.right){
                result.add(cur.val);
                pre = cur;
                cur = null;
                stack.pop();
            }else
                cur = cur.right;
        }
        return result;
    }
}
```