### ˳��ջ����ʹ��һ���ַ�������ڴ浥Ԫһ�α���ջ�е����ݡ�������һ��ָ����С�Ľṹ������Ϊջ�����Ϊ0��Ԫ�ؾ���ջ�ף��ٶ���һ������top����ջ����š�
### ��ʽջ����ʹ��������ʽ����ջ�и�Ԫ�ص�ֵ�������ײ���head������ָ��Ԫ�أ�Ϊջ��������β����ָ���ַnull��Ϊջ�ײ�
### ����ȳ�ԭ��

***
### ׼������
```
/*ջ ˳��洢�ṹʵ��*/
#include<stdio.h>

//���峣�� �洢�ռ�ĳ�ʼ������
#define MAXSIZE 20
#define ERROR 0
#define OK 1
//��typedef��������
typedef int Status;
typedef int SElemType;
//����һ���ṹ������
typedef struct{
    SElemType data[MAXSIZE];
    int top;
} Stack; 
```
### ջ��ʼ����
```
Status initStack(Stack *s){
	s->top=-1;
	return OK;
}
```

### �������Ա�ĳ���
```
//��ȡ����ĳ��� 
Status getListLength(LinkList L){
    int i = 0; //������
    while(L->next){
        L = L->next;
        i++;
    } 
    return i;
}
```

### ��ջ����Push��
```
Status push(Stack *s,SElemType e){
	// �ж�ջ�Ƿ���
	if(s->top == MAXSIZE -1){
		return ERROR;
	}
	s->top++;
	s->data[s->top]=e;
	return OK;
}
```
### ��ջ����pop��
```
Status pop(Stack *s, SElemType *e){
    //�ж�ջ�Ƿ�Ϊ�� 
    if(s->top == -1){
        return ERROR;
    } 
    *e = s->data[s->top];   //����Ҫ��ջ��Ԫ�� 
    s->top--;   //ջ������ 
    return OK; 
}
```
### ���ջ�е�����Ԫ�أ�
```
void stackTraverse(Stack s){
	if(s.top==-1){
		 printf("ջ����Ԫ��\n");
	}else{
		while(s.top!=-1){
			printf("%d ",s.data[s.top]);
			s.top--;
		}
		printf("\n");
	}
}
```
