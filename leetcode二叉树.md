### leetcode 刷题
二叉树的题目 总结起来都是三种遍历方式 BFS  DFS  还有啥？
##leetcode 110
##看到的评论：
附上一个我觉得很啰嗦的解法...但是我觉得树的递归大部分都可以这么套路的解决，相当于一个解题模版（初学数据结构的菜鸡
模版一共三步，就是递归的三部曲：
找终止条件：什么时候递归到头了？此题自然是root为空的时候，空树当然是平衡的。
思考返回值，每一级递归应该向上返回什么信息？参考我代码中的注释。
单步操作应该怎么写？因为递归就是大量的调用自身的重复操作，因此从宏观上考虑，只用想想单步怎么写就行了，左树和右树应该看成一个整体，即此时树一共三个节点：root，root.left，root.right。
如果独立写递归函数有困难的，可以参考一下我写的一个博客，附有详细的图文介绍：博客链接 https://lyl0724.github.io/2020/01/25/1/

class Solution {
    //这个ReturnNode是参考我描述的递归套路的第二步：思考返回值是什么
    //一棵树是BST等价于它的左、右俩子树都是BST且俩子树高度差不超过1
    //因此我认为返回值应该包含当前树是否是BST和当前树的高度这两个信息
    private class ReturnNode{
        boolean isB;
        int depth;
        public ReturnNode(int depth, boolean isB){
            this.isB = isB;
            this.depth = depth;
        }
    }
    //主函数
    public boolean isBalanced(TreeNode root) {
        return isBST(root).isB;
    }
    //参考递归套路的第三部：描述单次执行过程是什么样的
    //这里的单次执行过程具体如下：
    //是否终止?->没终止的话，判断是否满足不平衡的三个条件->返回值
    public ReturnNode isBST(TreeNode root){
        if(root == null){
            return new ReturnNode(0, true);
        }
        //不平衡的情况有3种：左树不平衡、右树不平衡、左树和右树差的绝对值大于1
        ReturnNode left = isBST(root.left);
        ReturnNode right = isBST(root.right);
        if(left.isB == false || right.isB == false){
            return new ReturnNode(0, false); 
        }
        if(Math.abs(left.depth - right.depth) > 1){
            return new ReturnNode(0, false);
        }
        //不满足上面3种情况，说明平衡了，树的深度为左右俩子树最大深度+1
        return new ReturnNode(Math.max(left.depth, right.depth) + 1, true);
    }
}