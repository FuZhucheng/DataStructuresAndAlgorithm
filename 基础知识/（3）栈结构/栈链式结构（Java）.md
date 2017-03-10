### ˳��ջ����ʹ��һ���ַ�������ڴ浥Ԫһ�α���ջ�е����ݡ�������һ��ָ����С�Ľṹ������Ϊջ�����Ϊ0��Ԫ�ؾ���ջ�ף��ٶ���һ������top����ջ����š�
### ��ʽջ����ʹ��������ʽ����ջ�и�Ԫ�ص�ֵ�������ײ���head������ָ��Ԫ�أ�Ϊջ��������β����ָ���ַnull��Ϊջ�ײ���
### ����ȳ�ԭ��

***
### ׼������
```
//���������
class Node {
	public int data;// ����ڵ������Ԫ�� 
	public Node next;// ������һ���ڵ������  

	public Node(int data, Node next) {
		this.data = data;
		this.next = next;
	}
}
//����Ǵ���ջ����
class LinkStack {
	private Node top;// ���ջ���ڵ�
	private int count;// ���ջ�����е�Ԫ�ظ���  
}

```
### ��ʼ����ջ��
```
public void init() {
		top = null;
		count = 0;
	}
```
### �пգ�
```
public boolean isEmpty() {
		return (count == 0);
	}
```
### ��������������ջ��ָ������Ԫ�ش�����ջ��ֻ��һ��Ԫ��
```
public LinkStack(int data) {
		top = new Node(data, null);
		count++;
	}
```

### �������Ա�ĳ���
```
public int getLength() {
		return count;
	}
```

### ��ջ����Push��
```
public void push(int data) {
		// ��Ϊ����ջҲ�Ͳ����жϴ�С�ˡ�
		//��topָ���½ڵ㣬�½ڵ��nextָ��ԭ����top  
		top = new Node(data, top);
		count++;
	}
```
### ��ջ����pop��
```
public int pop() {
// ����ǰΪ��ջ���򷵻�null 
		if (count == 0) {
			System.out.println("ջΪ�գ���");
			return -1;
		} 
		
			Node htempNode = top;
			 // ��topָ��ԭջ������һ���ڵ�  
			top = top.next;
			// �ͷ�ԭջ��Ԫ�ص�����  
			htempNode.next = null;
			count--;
			return htempNode.data;
		
	}
```
###  ��ȡջ��Ԫ�أ�
```
public int getTop() {
		if (count == 0) {
			return -1;
		}
		return top.data;
	}
```
### ���ջ��
```
public void clear() {
		top = null;
		count = 0;
	}
```