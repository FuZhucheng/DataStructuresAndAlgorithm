## 链表由许多结点组成，每个结点都包含两部分：1.数据域，保存该结点的实际数据；2.指针域保存下一个结点的地址。是一种动态存储分配的结构形式，可根据需要动态申请所需的内存单元。
### 优点：跟顺序表相对，插入和删除的时候，十分快！！
### 缺点：就是查找以及修改的时候需要遍历大量结点。
***
### 准备数据：
```
class DATA2{
	String key;						// 结点数据元素的数据项
	String name;
	int age;
}
//没有头结点的链表类
class CLType{					//定义链表结构
	DATA2 nodeData=new DATA2();		//具体数据保存在一个类DATA2中
	CLType nextNode;	//以对象存储对象引用。链表的类CLType,引用nextNode是用来指向下一个结点的，每次追加重新赋值。所以存的是结点名字嘛，就是指向下一个结点了
}
```
### 追加结点：
```
//追加一个结点在链表尾部.以下为类方法。head为链表头引用，输入参数nodeData为结点要保存的数据
public CLType CLAddEnd(CLtype head,DATA2 nodeData){
		CLType node,htemp;
		if(node=new CLType==null){
			System.out.println("申请分配内存失败！！");
			return null;
		}else{
			node.nodeData=nodeData;//保存新数据到这个新结点的数据域
			node.nextNode = null;	//把添加的那个结点的指针域致空
			if(head==null){
				head=node;//这个是建立链表后第一次的数据插入，也就是这里是插入第一个结点。
				return head;
			}
			htemp=head;
			//以下操作是头指针已经指向存在了的结点，也就是第一个结点有数据了。而这里把头指针指向的结点给htemp来使用局部变量循环
			//查找链表的末尾。就是查找链表的结点，找到最后的那个，因为最后的那个结点的指针域是null，没有指向
			//从全部结点依次赋值给htemp，直到htemp结点的指针域为空终止循环即找到了最后的结点
			while(head.nextNode!=null){
				htemp=htemp.nextNode;
			}
			htemp.nextNode=node;//找到最后结点，就可以把传进来的新结点需要的数据用那个我们初始化的结点node来保存。
			return head;//返回头指针
		}
}
```
### 插入头结点：
```
public CLType CLAddFirst(CLType head,DATA2 nodeData){
		CLType node;
		if(node=new CLType()==null){
			System.out.println("申请内存失败！！");
			return null;
		}else{
			node.nodeData=nodeData;
			node.nextNode=head;//目的是把原来那个空结点给推到下一位
			head=node; //很关键的是把原来的头指针给到我们这个设定为头结点的指针
			return head;
		}
}
```
### 查找结点：
```
	public CLType CLFindNode(CLType head,String key){
		CLType htemp;
		htemp=head;
		while(htemp!=null){//以局部变量htemp来循环，避免影响到头指针
			if(htemp.nodeData.key.compareTo(key)==0){//遍历过程对比结点的key与传过来的key，如果相同，就返回这个结点
				return htemp;
			}
			htemp=htemp.nextNode;
		}
		return null;//如果找不到，就返回null
	}
```
### 插入结点：
```
	public CLType CLInsertNode(CLType head,String findkey,DATA2 nodeData){
		CLType node,nodetemp;
		if(node=new CLType()==null){
			System.out.println("申请内存失败！！");
			return null;
		}
		node.nodeData=nodeData;
		nodetemp=CLFindeNode(head,findkey);//使用方法查找到该结点
		if(nodetemp!=null){
			node.nextNode = nodetemp.nextNode;//新增结点的指针域指向我们查找到的结点的下一个结点的数据域（就是查找到的结点的指针域啦）
			nodetemp.nextNode=node;//而我们查找到的结点的指针域则指向新增结点的数据域（就是新增结点的名字啦）
		}else{
			System.out.println("未找到正确的插入位置！");
		}
		return head;
	}
```
### 删除结点：
```
	public int CLDeleteNode(CLType head,String key){
		CLType node,htemp;//node表示要查找的结点的前一个结点，htemp表示要查到的结点，而他的指针域就指向了下一个结点啦
		htemp=head;
		node=head;
		while(htemp!=null){
			if(htemp.nodeData.keycompareTo(key)==0){
				node.nextNode=htemp.nextNode;	//当找到那个要删除的结点时，就用找到的结点的指针域（就是找到的结点的下一个结点的引用）赋值给node（htemp的前一个结点），即可完成链表的删除，但还没清内存
				htemp=null;//释放结点内存，java只需至null，即可自动设置弱引用进行回收
				return 1;
			}else{
				node=htemp;//指向当前的结点
				htemp=htemp.nextNode;//指向下一个结点
			}	
		}
		return 0;
	}
```
### 计算长度：
```
	public int CLLength(CLType head){
		CLType htemp;
		htemp=head;
		int Len=0;
		while(htemp!=null){
			htemp=htemp.nextNode;
			Len++;
		}
		return Len;
	}
```
### 显示所有结点：
```
	//打印出全部结点的数据
	void CLAllNode(CLType head){
		CLType htemp;			
		DATA2 nodeData;
		htemp=head;
		System.out.printf("当前链表共有%d个结点。链表所有数据如下：\n",CLLength(head));
		while(htemp!=null){					
		//把头结点赋值给htemp，然后以htemp局部变量来循环遍历，
		//在遍历过程把结点赋值给局部变量nodeData进行打印。
		//然后再用nextNode类似指针的东西（他指向了下一个结点的名字），赋值给局部变量htemp，htemp就保存了下一个结点的东西，htemp.Data就是取得到下一个结点的数据啦
			nodeData=htemp.nodeData;
			System.out.printf("结点(%s,%s,%d)",nodeData.key,nodeData.name,nodeData.age);
			htemp=htemp.nextNode;				
		}
	}
```