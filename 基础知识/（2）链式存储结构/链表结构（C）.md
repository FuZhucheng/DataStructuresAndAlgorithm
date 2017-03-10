### ͬ���Ľ����ڶ�Ӧ��Java�ĵ�������ֱ�ӽ�������ɡ�
## ����������Ҫ֪��һЩ�������Ǿ���ָ�����ʶ��
![����дͼƬ����](http://img.blog.csdn.net/20170304234533568?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSmFja19fRnJvc3Q=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
### Ҳ�������ǵ�����������ͷָ�룬��ֻ��һ��ָ���һ������ָ�롣������������ɾ�Ĳ�ʱ������Ҫʱ����ʶ������������в�����Դͷ�������������
### ������������ҲҪע�⣺��������ͷ���ģ���
***
### ׼������
```
//������洢�ṹ 
#include<stdio.h>
#include<stdlib.h>
#define OK 1
#define ERROR 0

typedef int ElemType;
typedef int Status;


typedef struct Node{
    ElemType data;
    struct Node *next; 
} Node;
typedef struct Node *LinkList;
```
### �����������ַ�ʽ��ͷ�巨��β�巨����ͷ���Ĳ巨��
```
//������Ĵ���,�������n�������,������ͷ���ĵ�����(ͷ�巨) 
Status createListHead(LinkList *L, int n){
    LinkList p;
    int i;
    *L = (LinkList)malloc(sizeof(Node)); //�������� 
    (*L)->next = NULL;  //����һ��ͷ��� 
    for(i = 0; i < n; i++){     //���ɽ�� 
        p = (LinkList)malloc(sizeof(Node));
        p->data = rand() % 100 + 1; //����100���ڵ����� 
        p->next = (*L)->next;   
        (*L)->next = p; //���뵽��ͷ     
    }   
    return OK;  
}
```
```
//������Ĵ���,�������n�������,������ͷ���ĵ�����(β�巨)
Status createListTail(LinkList *L,int n){
	LinkList pNew,q;//pNew��Ϊ������½���ݴ������q��Ϊÿ�η�����β����ݴ���� 
	int i;
	*L=(LinkList)malloc(sizeof(Node));//�����Դ˽������������һ����� 
	q=*L;
	for(i=0;i<n;i++){
		pNew = (LinkList)malloc(sizeof(Node));//����һ���µĽڵ�
		pNew->data=2*i;//����һ��100���ڵ����� 
		q->next=pNew; //�½ڵ���ӵ������ĩβ 
		q=pNew;	//�½ڵ㶨��Ϊβ�ڵ� 
	} 
	q->next=NULL;
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
### ����Ķ�ȡ
```
//������Ķ�ȡ,��e����L�еĵ�i��Ԫ�ص�ֵ , 0 < i < L.length
Status getElem(LinkList L,int i,ElemType *e){
	int j=1;
	LinkList p;
	p = L->next;//pΪ��һ���ڵ�
	while(p&&j<i){
		p=p->next;
		j++;
	}
	if(!p||i>j){//��˼���ǣ�������ĵ�i������������i 
		return ERROR;
	}
	*e = p->data;
	return OK;
}
```
### ����������,���ֵ
```
void listTraverse(LinkList L){
	if(L->next==NULL){
		 printf("����Ϊ��");
	}else{
		LinkList p;
		p=L->next;
//		while(p!=NULL){
		while(p){
			printf("%d ",p->data);
            p = p->next;  
		}
		printf("\n");   
	}
}
```
### Ԫ�صĲ��룺
```
//����Ĳ��� ��e���뵽��i��λ��֮ǰ 0 < i < listLenght + 1 
//��λ����i���ڵ�,����һ���µĽڵ�,����e�������µĽڵ���,�����뵽������ 
Status listInsert(LinkList *L, int i, ElemType e) {
	LinkList p,s;//p����ǰ��㣬s����Ҫ���������½�� 
	int j=1;
	p = *L; 
	while(p&&j<i){
		p=p->next;
		j++;
	}
	if(!p||i<j){
		return ERROR;
	}
	s=(LinkList)malloc(sizeof(Node));//����һ���µĽڵ�
	s->data=e;
	s->next=p->next;
	p->next=s;
	return OK;
}
```
### ����ɾ����
```
//����ɾ�� ��������ɾ����i��Ԫ��,��ɾ����Ԫ�ر��浽e�� 
Status ListDelete(LinkList *L, int i, ElemType *e){
	LinkList p,q;
	int j=1;
	p=*L;
	while(p&&j<i){
		p=p->next;
		j++;
	}
	if(!p||i<j){
		return ERROR;
	}
	q=p->next;
	*e=q->data;
	p->next=q->next;
	free(q);
	return OK;
}
```

### ɾ�����еĽڵ㣺
```
Status clearList(LinkList *L) {
	LinkList p,q;
	p=(*L)->next;
	while(p){
		q=p->next;
		free(p);
		p=q;
	}
	(*L)->next =NULL;
	return OK;
}
```
