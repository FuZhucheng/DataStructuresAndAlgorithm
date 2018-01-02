### 一种二叉排序树，其中每个节点的左子树和右子树的高度差至多为1.
#### 平衡因子：二叉树上节点的左子树深度减去右子树深度的值。
#### 1.可以是空树。2.假如不是空树，任何一个结点的左子树与右子树都是平衡二叉树，并且高度之差的绝对值不超过1
##### 认识平衡树接口
![这里写图片描述](http://img.blog.csdn.net/20170329102017480?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFja19fRnJvc3Q=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### 平衡二叉树的失衡调整主要是通过旋转最小失衡子树来实现的。
#### 最小失衡子树：在新插入的结点向上查找，以第一个平衡因子的绝对值超过1的结点为根的子树称为最小不平衡子树。也就是说，一棵失衡的树，是有可能有多棵子树同时失衡的，如下。而这个时候，我们只要调整最小的不平衡子树，就能够将不平衡的树调整为平衡的树。
![这里写图片描述](http://img.blog.csdn.net/20170329112015706?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFja19fRnJvc3Q=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
#### 可以看到，2节点的平衡因子为2，3节点的平衡因子也为2.那么就存在两颗不平衡子树了。但是我们调整的是最小失衡子树。我们只需以3为中心，将最小不平衡树向左旋转，即可得到平衡二叉树。
***
### 定义下AVL树先：
```
public class AVLTree {

    //指向当前AVL树的根节点
    private AVLNode root;
}

public class AVLNode {

    //节点的值
    public int key;

    //节点的平衡度
    public int balance;

    //分别指向节点的左孩子、右孩子与父节点
    public AVLNode left, right, parent;

    /**
     * @function 默认构造函数
     * @param k
     * @param p
     */
    AVLNode(int k, AVLNode p) {
        key = k;
        parent = p;
    }
}
```


## 多种失衡情况调整：
```
旋转的整体过程就是：
1- a、b指针的调整
2- a、b的子节点指针调整
3- 旋转代码，就是a和b互相的指向
4- a的父节点指针调整
5- 重新计算平衡调整。
```
### （1）LL型，左子树的左子节点
![这里写图片描述](http://img.blog.csdn.net/20170329121228143?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFja19fRnJvc3Q=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
```
//传入的是要调整节点的父节点。如上图的4！！！
private AVLNode rotateRight(AVLNode a) {
//指向当前节点的右孩子，如上图的3！！！
    AVLNode b = a.left;
    //将当前节点的右孩子挂载到当前节点的父节点。此处目的是：1.如果a父节点存在则用b节点去顶替a节点；2.如果不存在，则相当于至null啦！！可以再接入新引用。
    b.parent = a.parent;
 //将原本节点的右孩子挂载到新节点的左孩子。此处目的是：1.如果b节点还有右子节点，把它给到a的左子树，这样同样满足二叉查找树（当然一般很少还有子节点啦）；2.如果没有就是把a右子树至null，断开原来的引用。
    a.left = b.right;
//这里对应的就是上一句的第一种情况，b还有右子树的情况，因为是链式存储，要把引用指向a。
    if (a.left != null)
        a.left.parent = a;
/*
	下面的两句操作才是旋转啦，谁来做父节点，引用是谁指向谁！
*/
    b.right = a;
    a.parent = b;

    if (b.parent != null) {
        if (b.parent.right == a) {
            b.parent.right = b;
        } else {
            b.parent.left = b;
        }
    }

    setBalance(a, b);

    return b;
}
```
### （2）RR型，右子树的右子节点
![这里写图片描述](http://img.blog.csdn.net/20170329121932757?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFja19fRnJvc3Q=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
```
//传入的是要调整节点的父节点。如上图的2！！！
private AVLNode rotateLeft(AVLNode a) {

    //指向当前节点的右孩子，如上图的3！！！
    AVLNode b = a.right;

    //将当前节点的右孩子挂载到当前节点的父节点。此处目的是：1.如果a父节点存在则用b节点去顶替a节点；2.如果不存在，则相当于至null啦！！可以再接入新引用。
    b.parent = a.parent;

    //将原本节点的右孩子挂载到新节点的左孩子。此处目的是：1.如果b节点还有子节点，把它给到a的右子树，这样同样满足二叉查找树（当然一般很少还有子节点啦）；2.如果没有就是把a右子树至null，断开原来的引用。
    a.right = b.left;
//这里对应的就是上一句的第一种情况，b还有左子树的情况，因为是链式存储，要把引用指向a。
    if (a.right != null)
        a.right.parent = a;
/*
	下面的两句操作才是旋转啦，谁来做父节点，引用是谁指向谁！
*/
    //将原本节点挂载到新节点的左孩子上。
    b.left = a;

    //将原本节点的父节点设置为新节点
    a.parent = b;

    //如果当前节点的父节点不为空。这里是为了完成刚刚剩下的一个指针，一开始我们把b强行替代了a，但是父节点的指针还是有指向a的，所以在这里修改过来！！！
    if (b.parent != null) {
        if (b.parent.right == a) {
            b.parent.right = b;
        } else {
            b.parent.left = b;
        }
    }

    //重新计算每个节点的平衡度
    setBalance(a, b);

    return b;
}
```
### （3）LR型，左子树的右子节点：（先左旋再右旋）
![这里写图片描述](http://img.blog.csdn.net/20170329122114756?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFja19fRnJvc3Q=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
```
//n代表的是图中的一开始10节点位置
private AVLNode rotateLeftThenRight(AVLNode n) {
    n.left = rotateLeft(n.left);//先左旋，对应图中第二过程
    return rotateRight(n);//再右旋
}
```
### （4）RL型，右子树的左子节点：（先右旋再左旋）
![这里写图片描述](http://img.blog.csdn.net/20170329122813697?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFja19fRnJvc3Q=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
```
//n代表的是图中的一开始10节点位置
private AVLNode rotateRightThenLeft(AVLNode n) {
    n.right = rotateRight(n.right);
    return rotateLeft(n);
}
```
***
### 那么知道怎么调整，调整后的结点后，就是插入跟删除了嘛。
### 插入：
```
 //指向当前AVL树的根节点
private AVLNode root;

public boolean insert(int key) {

        //如果当前根节点为空,则直接创建新节点
        if (root == null)
            root = new AVLNode(key, null);
        else {

            //设置新的临时节点
            AVLNode n = root;

            //指向当前的父节点
            AVLNode parent;

            //循环直至找到合适的插入位置
            while (true) {

                //如果查找到了相同值的节点
                if (n.key == key)
                    //则直接报错
                    return false;

                //将当前父节点指向当前节点
                parent = n;

                //判断是移动到左节点还是右节点。true就往左移动，插左子树，false就插右子树。
                boolean goLeft = n.key > key;
                n = goLeft ? n.left : n.right;

                //如果左孩子或者右孩子为空
                if (n == null) {
                    if (goLeft) {
                        //将节点挂载到左孩子上
                        parent.left = new AVLNode(key, parent);
                    } else {
                        //否则挂载到右孩子上
                        parent.right = new AVLNode(key, parent);
                    }

                    //重平衡该树
                    rebalance(parent);
                    break;
                }

                //如果不为空,则以n为当前节点进行查找
            }
        }
        return true;
    }
```
### 删除：
```

    /**
     * @param delKey
     * @function 根据关键值删除某个元素, 需要对树进行再平衡
     */
    public void delete(int delKey) {
     //如果当前根节点为空,则直接返回null
        if (root == null)
            return;
        AVLNode n = root;//当前节点
        AVLNode parent = root;//当前节点的父节点
        AVLNode delAVLNode = null;//要删除的节点
        AVLNode child = root;//当前节点的孩子
	//找出要删除的节点
        while (child != null) {
            parent = n;
            n = child;
            child = delKey >= n.key ? n.right : n.left;//根据二叉查找树性质去遍历下一个节点查找
            if (delKey == n.key)
                delAVLNode = n;//找到要删的节点了，就是当前的那个
        }
	//删除节点
        if (delAVLNode != null) {
            delAVLNode.key = n.key;//直接把那个要删除的值给覆盖掉。

            child = n.left != null ? n.left : n.right;//找到要删除节点的子节点去替换。

            if (root.key == delKey) {//要删除的如果是根节点
                root = child;//就把子节点当作根节点
            } else {
                if (parent.left == n) {//如果删除的是父节点的左子树，就把它的子节点给到父节点的左子树
                    parent.left = child;
                } else {//同上
                    parent.right = child;
                }
                rebalance(parent);//重新平衡
            }
        }
    }
```
### 插入和删除必须有的，重新平衡操作：
```
/**
     * @param n
     * @function 重平衡该树
     */
    private void rebalance(AVLNode n) {

        //为每个节点设置相对高度
        setBalance(n);

        //如果左子树高于右子树
        if (n.balance == -2) {

            //如果挂载的是左子树的左孩子
            if (height(n.left.left) >= height(n.left.right))

                //进行右旋操作
                n = rotateRight(n);
            else

                //如果挂载的是左子树的右孩子,则先左旋后右旋
                n = rotateLeftThenRight(n);

        }
        //如果左子树高于右子树
        else if (n.balance == 2) {

            //如果挂载的是右子树的右孩子
            if (height(n.right.right) >= height(n.right.left))

                //进行左旋操作
                n = rotateLeft(n);
            else

                //否则进行先右旋后左旋
                n = rotateRightThenLeft(n);
        }

        if (n.parent != null) {

            //如果当前节点的父节点不为空,则平衡其父节点
            rebalance(n.parent);
        } else {
            root = n;
        }
    }
```
### 插入和删除时刻保持二叉树的平衡，那么我们知道AVL树也是二叉查找树，所以，还是使用二叉查找树的查找操作嘛。
```
public Node findNode(int data){
		if(root==null){
			return null;
		}
		TreeNode currentNode = root;//把根结点给到currentNode，由它开始递归
		while(currentNode!=null){
			if(currentNode.data>data){//大于data就往左子树递归找
				currentNode = currentNode.left;
			}else if(currentNode.data<data){//小于data就往右子树找
				currentNode = currentNode.right;
			}else{//找到了就返回！
				return currentNode;
			}
		}
		return null;
	}
```
### 还有一些特别操作啦：
```
    /**
     * @param n
     * @return
     * @function 计算某个节点的高度
     */
    private int height(AVLNode n) {
        if (n == null)
            return -1;
        return 1 + Math.max(height(n.left), height(n.right));
    }
```
```
 /**
     * @param AVLNodes
     * @function 重设置每个节点的平衡度
     */
    private void setBalance(AVLNode... AVLNodes) {
        for (AVLNode n : AVLNodes)//肯定是遍历去设置的啦
            n.balance = height(n.right) - height(n.left);
    }
```