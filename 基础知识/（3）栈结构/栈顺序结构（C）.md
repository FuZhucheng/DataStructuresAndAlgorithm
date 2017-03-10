### 顺序栈：即使用一组地址连续的内存单元一次保存栈中的数据。即定义一个指定大小的结构数组作为栈，序号为0的元素就是栈底，再定义一个变量top保存栈顶序号。
### 链式栈：即使用链表形式保存栈中各元素的值。链表首部（head引用所指向元素）为栈顶，链表尾部（指向地址null）为栈底部
### 后进先出原则。

***
### 准备数据
```
/*栈 顺序存储结构实现*/
#include<stdio.h>

//定义常量 存储空间的初始化分配
#define MAXSIZE 20
#define ERROR 0
#define OK 1
//用typedef定义类型
typedef int Status;
typedef int SElemType;
//定义一个结构体类型
typedef struct{
    SElemType data[MAXSIZE];
    int top;
} Stack; 
```
### 栈初始化：
```
Status initStack(Stack *s){
	s->top=-1;
	return OK;
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

### 入栈操作Push：
```
Status push(Stack *s,SElemType e){
	// 判断栈是否满
	if(s->top == MAXSIZE -1){
		return ERROR;
	}
	s->top++;
	s->data[s->top]=e;
	return OK;
}
```
### 出栈操作pop：
```
Status pop(Stack *s, SElemType *e){
    //判断栈是否为空 
    if(s->top == -1){
        return ERROR;
    } 
    *e = s->data[s->top];   //保存要出栈的元素 
    s->top--;   //栈顶下移 
    return OK; 
}
```
### 输出栈中的所有元素：
```
void stackTraverse(Stack s){
	if(s.top==-1){
		 printf("栈中无元素\n");
	}else{
		while(s.top!=-1){
			printf("%d ",s.data[s.top]);
			s.top--;
		}
		printf("\n");
	}
}
```
