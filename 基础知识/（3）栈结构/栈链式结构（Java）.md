### 顺序栈：即使用一组地址连续的内存单元一次保存栈中的数据。即定义一个指定大小的结构数组作为栈，序号为0的元素就是栈底，再定义一个变量top保存栈顶序号。
### 链式栈：即使用链表形式保存栈中各元素的值。链表首部（head引用所指向元素）为栈顶，链表尾部（指向地址null）为栈底部。
### 后进先出原则。

***
### 准备数据
```
//代表结点的类
class Node {
	public int data;// 保存节点的数据元素 
	public Node next;// 保存下一个节点的引用  

	public Node(int data, Node next) {
		this.data = data;
		this.next = next;
	}
}
//这个是代表栈的类
class LinkStack {
	private Node top;// 存放栈顶节点
	private int count;// 存放栈中已有的元素个数  
}

```
### 初始化链栈：
```
public void init() {
		top = null;
		count = 0;
	}
```
### 判空：
```
public boolean isEmpty() {
		return (count == 0);
	}
```
### 构造器，构造链栈：指定数据元素创建链栈，只有一个元素
```
public LinkStack(int data) {
		top = new Node(data, null);
		count++;
	}
```

### 返回线性表的长度
```
public int getLength() {
		return count;
	}
```

### 入栈操作Push：
```
public void push(int data) {
		// 因为是链栈也就不用判断大小了。
		//让top指向新节点，新节点的next指向原来的top  
		top = new Node(data, top);
		count++;
	}
```
### 出栈操作pop：
```
public int pop() {
// 若当前为空栈，则返回null 
		if (count == 0) {
			System.out.println("栈为空！！");
			return -1;
		} 
		
			Node htempNode = top;
			 // 让top指向原栈顶的下一个节点  
			top = top.next;
			// 释放原栈顶元素的引用  
			htempNode.next = null;
			count--;
			return htempNode.data;
		
	}
```
###  获取栈顶元素：
```
public int getTop() {
		if (count == 0) {
			return -1;
		}
		return top.data;
	}
```
### 清空栈：
```
public void clear() {
		top = null;
		count = 0;
	}
```