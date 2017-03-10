### 顺序栈：即使用一组地址连续的内存单元一次保存栈中的数据。即定义一个指定大小的结构数组作为栈，序号为0的元素就是栈底，再定义一个变量top保存栈顶序号。
### 链式栈：即使用链表形式保存栈中各元素的值。链表首部（head引用所指向元素）为栈顶，链表尾部（指向地址null）为栈底部。
### 后进先出原则。

***
### 栈 链式存储结构实现
####   第一个结构体是每一个节点元素, 类似于链表 
####   第二个结构体是用个指针top指向链表的尾部 
### 注意：a.data，a是一个结构体变量。a->data，a是一个指针变量。LinkStackPtr是一个指针类型变量
### 准备数据
```
#include<stdio.h>
#include<stdlib.h>
#define OK 1
#define ERROR 0

typedef int SElemType;
typedef int Status;
//栈中的节点 
typedef struct StackNode{
    SElemType data; 
    struct StackNode *next; 
} StackNode, *LinkStackPtr;
//专门用来指示整个栈以及保存栈信息 
typedef struct LinkStack{
    LinkStackPtr top;
    int count;
} LinkStack;

```
### 初始化链栈：
```
Status initStack(LinkStack *S){
	LinkStackPtr p;
	//malloc返回一个指向这块空间起始地址的void*
	p=(LinkStackPtr)malloc(sizeof(StackNode));
	p->next=NULL;//把该结点初始化 
	S->top=p;//把链表的头指针指向栈顶 
	S->count=0;
	return OK;
}
```
### 判空：
```
Status StackEmpty(LinkStack S){
	if(S.count == 0){
		return OK;//为null
	}else{
		return ERROR;
	}
}
```
### 返回线性表的长度
```
int getLength(LinkStack S) {
		return S.count;
	}
```

### 入栈操作Push：
```
Status push(LinkStack *S,SElemType e){
	LinkStackPtr s = (LinkStackPtr)malloc(sizeof(StackNode));
	s->data=e;
	s->next=S->top;//必须先把栈顶指针给到新节点的直接后继 ，不然一会位置错误 
	S->top=s;//我们都是操作头节点的，也就是栈顶节点，所以把新的节点s给到栈顶指针 
	S->count++;
	return OK;
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
###  出栈，获取栈顶元素：
```
Status pop(LinkStack *S,SElemType *e){
	//判空 
	if(StackEmpty(*S)){
		return ERROR;
	}
	*e=S->top->data;
	LinkStackPtr p;//为了删除节点
	p=S->top;//将栈顶结点赋值给p ，先拿到它的地址，出栈后再利用此地址删除节点 
	S->top=S->top->next;//栈顶指向下一个结点 
	free(p);//释放结点p
	S->count--;
	return OK; 
}
```
### 遍历栈：
```
void stackTraverse(LinkStack S){
	if(S.count==0){
		 printf("栈为空\n");
	}else{
		LinkStackPtr p;//一个指针变量，所以只能给指针变量咯 
		p=S.top;
		while(p->next){//为什么根据这个遍历？？因为每个结点都有指针域，用此来判是否继续 
			printf("%d ",p->data);
			p=p->next;
		}
	}
}
```