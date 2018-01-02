### һ�ֶ���������������ÿ���ڵ�����������������ĸ߶Ȳ�����Ϊ1.
#### ƽ�����ӣ��������Ͻڵ����������ȼ�ȥ��������ȵ�ֵ��
#### 1.�����ǿ�����2.���粻�ǿ������κ�һ������������������������ƽ������������Ҹ߶�֮��ľ���ֵ������1
##### ��ʶƽ�����ӿ�
![����дͼƬ����](http://img.blog.csdn.net/20170329102017480?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFja19fRnJvc3Q=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### ƽ���������ʧ�������Ҫ��ͨ����ת��Сʧ��������ʵ�ֵġ�
#### ��Сʧ�����������²���Ľ�����ϲ��ң��Ե�һ��ƽ�����ӵľ���ֵ����1�Ľ��Ϊ����������Ϊ��С��ƽ��������Ҳ����˵��һ��ʧ����������п����ж������ͬʱʧ��ģ����¡������ʱ������ֻҪ������С�Ĳ�ƽ�����������ܹ�����ƽ���������Ϊƽ�������
![����дͼƬ����](http://img.blog.csdn.net/20170329112015706?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFja19fRnJvc3Q=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
#### ���Կ�����2�ڵ��ƽ������Ϊ2��3�ڵ��ƽ������ҲΪ2.��ô�ʹ������Ų�ƽ�������ˡ��������ǵ���������Сʧ������������ֻ����3Ϊ���ģ�����С��ƽ����������ת�����ɵõ�ƽ���������
***
### ������AVL���ȣ�
```
public class AVLTree {

    //ָ��ǰAVL���ĸ��ڵ�
    private AVLNode root;
}

public class AVLNode {

    //�ڵ��ֵ
    public int key;

    //�ڵ��ƽ���
    public int balance;

    //�ֱ�ָ��ڵ�����ӡ��Һ����븸�ڵ�
    public AVLNode left, right, parent;

    /**
     * @function Ĭ�Ϲ��캯��
     * @param k
     * @param p
     */
    AVLNode(int k, AVLNode p) {
        key = k;
        parent = p;
    }
}
```


## ����ʧ�����������
```
��ת��������̾��ǣ�
1- a��bָ��ĵ���
2- a��b���ӽڵ�ָ�����
3- ��ת���룬����a��b�����ָ��
4- a�ĸ��ڵ�ָ�����
5- ���¼���ƽ�������
```
### ��1��LL�ͣ������������ӽڵ�
![����дͼƬ����](http://img.blog.csdn.net/20170329121228143?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFja19fRnJvc3Q=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
```
//�������Ҫ�����ڵ�ĸ��ڵ㡣����ͼ��4������
private AVLNode rotateRight(AVLNode a) {
//ָ��ǰ�ڵ���Һ��ӣ�����ͼ��3������
    AVLNode b = a.left;
    //����ǰ�ڵ���Һ��ӹ��ص���ǰ�ڵ�ĸ��ڵ㡣�˴�Ŀ���ǣ�1.���a���ڵ��������b�ڵ�ȥ����a�ڵ㣻2.��������ڣ����൱����null�����������ٽ��������á�
    b.parent = a.parent;
 //��ԭ���ڵ���Һ��ӹ��ص��½ڵ�����ӡ��˴�Ŀ���ǣ�1.���b�ڵ㻹�����ӽڵ㣬��������a��������������ͬ������������������Ȼһ����ٻ����ӽڵ�������2.���û�о��ǰ�a��������null���Ͽ�ԭ�������á�
    a.left = b.right;
//�����Ӧ�ľ�����һ��ĵ�һ�������b�������������������Ϊ����ʽ�洢��Ҫ������ָ��a��
    if (a.left != null)
        a.left.parent = a;
/*
	������������������ת����˭�������ڵ㣬������˭ָ��˭��
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
### ��2��RR�ͣ������������ӽڵ�
![����дͼƬ����](http://img.blog.csdn.net/20170329121932757?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFja19fRnJvc3Q=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
```
//�������Ҫ�����ڵ�ĸ��ڵ㡣����ͼ��2������
private AVLNode rotateLeft(AVLNode a) {

    //ָ��ǰ�ڵ���Һ��ӣ�����ͼ��3������
    AVLNode b = a.right;

    //����ǰ�ڵ���Һ��ӹ��ص���ǰ�ڵ�ĸ��ڵ㡣�˴�Ŀ���ǣ�1.���a���ڵ��������b�ڵ�ȥ����a�ڵ㣻2.��������ڣ����൱����null�����������ٽ��������á�
    b.parent = a.parent;

    //��ԭ���ڵ���Һ��ӹ��ص��½ڵ�����ӡ��˴�Ŀ���ǣ�1.���b�ڵ㻹���ӽڵ㣬��������a��������������ͬ������������������Ȼһ����ٻ����ӽڵ�������2.���û�о��ǰ�a��������null���Ͽ�ԭ�������á�
    a.right = b.left;
//�����Ӧ�ľ�����һ��ĵ�һ�������b�������������������Ϊ����ʽ�洢��Ҫ������ָ��a��
    if (a.right != null)
        a.right.parent = a;
/*
	������������������ת����˭�������ڵ㣬������˭ָ��˭��
*/
    //��ԭ���ڵ���ص��½ڵ�������ϡ�
    b.left = a;

    //��ԭ���ڵ�ĸ��ڵ�����Ϊ�½ڵ�
    a.parent = b;

    //�����ǰ�ڵ�ĸ��ڵ㲻Ϊ�ա�������Ϊ����ɸո�ʣ�µ�һ��ָ�룬һ��ʼ���ǰ�bǿ�������a�����Ǹ��ڵ��ָ�뻹����ָ��a�ģ������������޸Ĺ���������
    if (b.parent != null) {
        if (b.parent.right == a) {
            b.parent.right = b;
        } else {
            b.parent.left = b;
        }
    }

    //���¼���ÿ���ڵ��ƽ���
    setBalance(a, b);

    return b;
}
```
### ��3��LR�ͣ������������ӽڵ㣺����������������
![����дͼƬ����](http://img.blog.csdn.net/20170329122114756?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFja19fRnJvc3Q=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
```
//n�������ͼ�е�һ��ʼ10�ڵ�λ��
private AVLNode rotateLeftThenRight(AVLNode n) {
    n.left = rotateLeft(n.left);//����������Ӧͼ�еڶ�����
    return rotateRight(n);//������
}
```
### ��4��RL�ͣ������������ӽڵ㣺����������������
![����дͼƬ����](http://img.blog.csdn.net/20170329122813697?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFja19fRnJvc3Q=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
```
//n�������ͼ�е�һ��ʼ10�ڵ�λ��
private AVLNode rotateRightThenLeft(AVLNode n) {
    n.right = rotateRight(n.right);
    return rotateLeft(n);
}
```
***
### ��ô֪����ô������������Ľ��󣬾��ǲ����ɾ�����
### ���룺
```
 //ָ��ǰAVL���ĸ��ڵ�
private AVLNode root;

public boolean insert(int key) {

        //�����ǰ���ڵ�Ϊ��,��ֱ�Ӵ����½ڵ�
        if (root == null)
            root = new AVLNode(key, null);
        else {

            //�����µ���ʱ�ڵ�
            AVLNode n = root;

            //ָ��ǰ�ĸ��ڵ�
            AVLNode parent;

            //ѭ��ֱ���ҵ����ʵĲ���λ��
            while (true) {

                //������ҵ�����ֵͬ�Ľڵ�
                if (n.key == key)
                    //��ֱ�ӱ���
                    return false;

                //����ǰ���ڵ�ָ��ǰ�ڵ�
                parent = n;

                //�ж����ƶ�����ڵ㻹���ҽڵ㡣true�������ƶ�������������false�Ͳ���������
                boolean goLeft = n.key > key;
                n = goLeft ? n.left : n.right;

                //������ӻ����Һ���Ϊ��
                if (n == null) {
                    if (goLeft) {
                        //���ڵ���ص�������
                        parent.left = new AVLNode(key, parent);
                    } else {
                        //������ص��Һ�����
                        parent.right = new AVLNode(key, parent);
                    }

                    //��ƽ�����
                    rebalance(parent);
                    break;
                }

                //�����Ϊ��,����nΪ��ǰ�ڵ���в���
            }
        }
        return true;
    }
```
### ɾ����
```

    /**
     * @param delKey
     * @function ���ݹؼ�ֵɾ��ĳ��Ԫ��, ��Ҫ����������ƽ��
     */
    public void delete(int delKey) {
     //�����ǰ���ڵ�Ϊ��,��ֱ�ӷ���null
        if (root == null)
            return;
        AVLNode n = root;//��ǰ�ڵ�
        AVLNode parent = root;//��ǰ�ڵ�ĸ��ڵ�
        AVLNode delAVLNode = null;//Ҫɾ���Ľڵ�
        AVLNode child = root;//��ǰ�ڵ�ĺ���
	//�ҳ�Ҫɾ���Ľڵ�
        while (child != null) {
            parent = n;
            n = child;
            child = delKey >= n.key ? n.right : n.left;//���ݶ������������ȥ������һ���ڵ����
            if (delKey == n.key)
                delAVLNode = n;//�ҵ�Ҫɾ�Ľڵ��ˣ����ǵ�ǰ���Ǹ�
        }
	//ɾ���ڵ�
        if (delAVLNode != null) {
            delAVLNode.key = n.key;//ֱ�Ӱ��Ǹ�Ҫɾ����ֵ�����ǵ���

            child = n.left != null ? n.left : n.right;//�ҵ�Ҫɾ���ڵ���ӽڵ�ȥ�滻��

            if (root.key == delKey) {//Ҫɾ��������Ǹ��ڵ�
                root = child;//�Ͱ��ӽڵ㵱�����ڵ�
            } else {
                if (parent.left == n) {//���ɾ�����Ǹ��ڵ�����������Ͱ������ӽڵ�������ڵ��������
                    parent.left = child;
                } else {//ͬ��
                    parent.right = child;
                }
                rebalance(parent);//����ƽ��
            }
        }
    }
```
### �����ɾ�������еģ�����ƽ�������
```
/**
     * @param n
     * @function ��ƽ�����
     */
    private void rebalance(AVLNode n) {

        //Ϊÿ���ڵ�������Ը߶�
        setBalance(n);

        //�������������������
        if (n.balance == -2) {

            //������ص���������������
            if (height(n.left.left) >= height(n.left.right))

                //������������
                n = rotateRight(n);
            else

                //������ص������������Һ���,��������������
                n = rotateLeftThenRight(n);

        }
        //�������������������
        else if (n.balance == 2) {

            //������ص������������Һ���
            if (height(n.right.right) >= height(n.right.left))

                //������������
                n = rotateLeft(n);
            else

                //�������������������
                n = rotateRightThenLeft(n);
        }

        if (n.parent != null) {

            //�����ǰ�ڵ�ĸ��ڵ㲻Ϊ��,��ƽ���丸�ڵ�
            rebalance(n.parent);
        } else {
            root = n;
        }
    }
```
### �����ɾ��ʱ�̱��ֶ�������ƽ�⣬��ô����֪��AVL��Ҳ�Ƕ�������������ԣ�����ʹ�ö���������Ĳ��Ҳ����
```
public Node findNode(int data){
		if(root==null){
			return null;
		}
		TreeNode currentNode = root;//�Ѹ�������currentNode��������ʼ�ݹ�
		while(currentNode!=null){
			if(currentNode.data>data){//����data�����������ݹ���
				currentNode = currentNode.left;
			}else if(currentNode.data<data){//С��data������������
				currentNode = currentNode.right;
			}else{//�ҵ��˾ͷ��أ�
				return currentNode;
			}
		}
		return null;
	}
```
### ����һЩ�ر��������
```
    /**
     * @param n
     * @return
     * @function ����ĳ���ڵ�ĸ߶�
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
     * @function ������ÿ���ڵ��ƽ���
     */
    private void setBalance(AVLNode... AVLNodes) {
        for (AVLNode n : AVLNodes)//�϶��Ǳ���ȥ���õ���
            n.balance = height(n.right) - height(n.left);
    }
```