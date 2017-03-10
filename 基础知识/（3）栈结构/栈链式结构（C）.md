### ˳��ջ����ʹ��һ���ַ�������ڴ浥Ԫһ�α���ջ�е����ݡ�������һ��ָ����С�Ľṹ������Ϊջ�����Ϊ0��Ԫ�ؾ���ջ�ף��ٶ���һ������top����ջ����š�
### ��ʽջ����ʹ��������ʽ����ջ�и�Ԫ�ص�ֵ�������ײ���head������ָ��Ԫ�أ�Ϊջ��������β����ָ���ַnull��Ϊջ�ײ���
### ����ȳ�ԭ��

***
### ջ ��ʽ�洢�ṹʵ��
####   ��һ���ṹ����ÿһ���ڵ�Ԫ��, ���������� 
####   �ڶ����ṹ�����ø�ָ��topָ�������β�� 
### ע�⣺a.data��a��һ���ṹ�������a->data��a��һ��ָ�������LinkStackPtr��һ��ָ�����ͱ���
### ׼������
```
#include<stdio.h>
#include<stdlib.h>
#define OK 1
#define ERROR 0

typedef int SElemType;
typedef int Status;
//ջ�еĽڵ� 
typedef struct StackNode{
    SElemType data; 
    struct StackNode *next; 
} StackNode, *LinkStackPtr;
//ר������ָʾ����ջ�Լ�����ջ��Ϣ 
typedef struct LinkStack{
    LinkStackPtr top;
    int count;
} LinkStack;

```
### ��ʼ����ջ��
```
Status initStack(LinkStack *S){
	LinkStackPtr p;
	//malloc����һ��ָ�����ռ���ʼ��ַ��void*
	p=(LinkStackPtr)malloc(sizeof(StackNode));
	p->next=NULL;//�Ѹý���ʼ�� 
	S->top=p;//�������ͷָ��ָ��ջ�� 
	S->count=0;
	return OK;
}
```
### �пգ�
```
Status StackEmpty(LinkStack S){
	if(S.count == 0){
		return OK;//Ϊnull
	}else{
		return ERROR;
	}
}
```
### �������Ա�ĳ���
```
int getLength(LinkStack S) {
		return S.count;
	}
```

### ��ջ����Push��
```
Status push(LinkStack *S,SElemType e){
	LinkStackPtr s = (LinkStackPtr)malloc(sizeof(StackNode));
	s->data=e;
	s->next=S->top;//�����Ȱ�ջ��ָ������½ڵ��ֱ�Ӻ�� ����Ȼһ��λ�ô��� 
	S->top=s;//���Ƕ��ǲ���ͷ�ڵ�ģ�Ҳ����ջ���ڵ㣬���԰��µĽڵ�s����ջ��ָ�� 
	S->count++;
	return OK;
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
###  ��ջ����ȡջ��Ԫ�أ�
```
Status pop(LinkStack *S,SElemType *e){
	//�п� 
	if(StackEmpty(*S)){
		return ERROR;
	}
	*e=S->top->data;
	LinkStackPtr p;//Ϊ��ɾ���ڵ�
	p=S->top;//��ջ����㸳ֵ��p �����õ����ĵ�ַ����ջ�������ô˵�ַɾ���ڵ� 
	S->top=S->top->next;//ջ��ָ����һ����� 
	free(p);//�ͷŽ��p
	S->count--;
	return OK; 
}
```
### ����ջ��
```
void stackTraverse(LinkStack S){
	if(S.count==0){
		 printf("ջΪ��\n");
	}else{
		LinkStackPtr p;//һ��ָ�����������ֻ�ܸ�ָ������� 
		p=S.top;
		while(p->next){//Ϊʲô�����������������Ϊÿ����㶼��ָ�����ô������Ƿ���� 
			printf("%d ",p->data);
			p=p->next;
		}
	}
}
```