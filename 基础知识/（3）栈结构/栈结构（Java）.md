### 顺序栈：即使用一组地址连续的内存单元一次保存栈中的数据。即定义一个指定大小的结构数组作为栈，序号为0的元素就是栈底，再定义一个变量top保存栈顶序号。
### 链式栈：即使用链表形式保存栈中各元素的值。链表首部（head引用所指向元素）为栈顶，链表尾部（指向地址null）为栈底部
### 后进先出原则。

***
### 准备数据
```
//顺序栈结构的实现
class DATA3{
	String name;
	int age;
}
class StackType{
	static final int MAXLEN=50;					//定义栈的大小
	DATA3[]data=new DATA3[MAXLEN+1];			//用数组实现存储数据元素
	int top;									//栈顶标志，始终标志栈顶
}
	
```
### 栈初始化：
```
StackType STInit(){						//初始化栈大小。栈名就是指向栈顶的地址
		StackType p;
		if((p=new StackType())!=null){			//申请栈内存
			p.top=0;							//设置栈顶为0
			return p;							//返回指向栈顶的引用
		}
		return null;							//申请失败返回null
	}
```

### 返回线性表的长度
```
//获取链表的长度 
Status getListLength(LinkList L){
    int i = 0; //计数器
    while(L->next){
        L = L->next;
        i++;
    } 
    return i;
}
```
### 栈判空：
```
boolean STIsEmpty(StackType s){				//判断栈是否为空
		boolean t;								//如果是空栈则表示栈没有数据，可以进行入栈操作，但不可进行出栈操作
		t=(s.top==-1);
		return t;
	}
```
### 栈判满
```
boolean STIsFull(StackType s){				//判断栈是否已满
		boolean t;								//如果是满栈，泽表示该栈结构没有多余的空间来保存额外的数据，此时不可进行入栈，但可以出栈
		t=(s.top==MAXLEN);
		return t;
	}
```
### 清空栈：
```
void STClear(StackType s){					//清空栈。
		s.top=-1;							//输入参数s是一个指向操作的栈的引用（对象的引用）。在程序中，将栈顶top设置为0，表示执行清空栈操作
	}
```
### 释放栈内存：
```
void STFree(StackType s){				//释放栈所占用的空间。其实就是把对象给至null，内存机制就回收他
		if(s!=null){											
			s=null;
		}
}
```

### 入栈操作Push：
```
void PushST(StackType s,DATA3 data){
		if((s.top+1)>MAXLEN){					//先判断栈顶top，如果top大于等于SIZE，则表示溢出
			System.out.print("栈溢出！\n");			//设置top=top+1（栈顶引用加1，指向入栈地址）
		}
		s.data[++s.top]=data;			//元素入栈
	}
```
### 出栈操作pop：
```
DATA3 PopST(StackType s){					
		if(s.top==-1){								//判断栈顶top，如果top为0，则表示为空栈，进行出错处理。
													//将栈顶引用top所指位置的元素返回，设置top=top-1，也就是使用栈顶引用减1，指向栈的下一个元素，原来栈顶元素被弹出
			System.out.print("栈为空！\n");				
			System.exit(0);
		}
		return (s.data[s.top--]);				//利用栈顶top来标记，使top-1，然后返回这个要出栈的结点。而在执行完后，因为是后--的，所以本来的栈表就减去了栈顶的结点，所以就作出这样的出栈动作啦
	}
```
### 读取栈顶数据：
```
DATA3 PeekST(StackType s){				//由于栈结构只能在一段进行操作，所以读取操作就是读取栈顶的结点数据
		if(s.top==-1){						
			System.out.print("栈为空！\n");
			System.out.print(0);
		}
		return (s.data[s.top]);				//方法返回值是一个DATA3类型的数据，返回值是栈顶的数据元素（栈顶结点）
	}
```
