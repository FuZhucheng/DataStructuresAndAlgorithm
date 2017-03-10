### ͬ���Ľ����ڶ�Ӧ��Java�ĵ�������ֱ�ӽ�������ɡ�
## ����������Ҫ��סһ�㣬C������Ҫ׼ȷ��ȥ�����ڴ棬Ҳ����Ҫ��������Ӧλ�õ��ڴ����ݣ���������Java����һ���������ݣ������������á�����˵�����������������أ���
### Ҳ����c�д���������ǵ�ַ����һ���������������ˣ���
### ���������Ҫ�����������ݵģ�Ҳ����Ҫ���������ڴ棬������Ҫ�������ã���c�о�����Ҫ����ָ�롣
### �������ֻ�����õ�����������ݣ���ô���ǲ��贫ָ���ַ��ȥ��ֻ���������
*** 
### ׼������
```
#include<stdio.h>
//���峣�� �洢�ռ�ĳ�ʼ������
#define MAXSIZE 20
#define TRUE 1
#define ERROR -1
#define FALSE 0
#define OK 1
//��typedef��������
typedef int Status;
typedef int ElemType;

//����һ���ṹ������
typedef struct{
    ElemType data[MAXSIZE];
    int length;
} SqList; 
```
### ��ʼ������
```
Status initList(SqList *L){
	L->length = 0;
	return OK;
}
```
### �������Ա�ĳ���
```
Status getListLength(SqList L){
	return L.length;
}
```
### ���Ա����,����Ϊ0 
```
Status clearList(SqList *L){
	L->length=0;
	return OK;
}
```
### ���Ա�Ϊ�շ���true,���򷵻�false
```
Status listEmpty(SqList L){
	if(L.length==0){
		return TRUE;
	}
	return FALSE;
}
```
### ��ȡָ����Ԫ�ص�ֵ,�����±�Ϊi - 1��Ԫ��,��ֵ��e
```
Status getElem(SqList L,int i, ElemType *e){
	 //�ж�Ԫ��λ���Ƿ�Ϸ�[i]
	 if(i<1||i>L.length){
	 	printf("���ҵ�λ�ò���ȷ \n");
        return ERROR; 
	 }
	 //�ж����Ա��Ƿ�Ϊ��
    if(listEmpty(L)){
        return ERROR;
    } 
    *e = L.data[i-1];
    return OK;
}
```
### �����Ա��в���ָ����e��ȵ�Ԫ��,������ҳɹ�,���ظ�Ԫ�ص��±�,���򷵻�ERROR
```
Status locateElem(SqList L,ElemType e){
	int i;
	for(i=0;i<L.length-1;i++){
		if(L.data[i]==e){
			return i;
		}
	}
	printf("û�в��ҵ�Ԫ�� %d ָ�����±�\n",e);
	return ERROR;
}
```
### �Զ����� MAXSIZE ��Ԫ��,����ֵΪ0 
```
Status createList(SqList *L){
	int i;
	for(i=0;i<10;i++){
		L->data[i]=0;
	}
	L->length=10;
	return OK;
}
```
### �����Ա��е�i��λ��ǰ������Ԫ��e
```
Status listInsert(SqList *L,int i, ElemType e){
	//�жϳ����Ƿ������������µ�����
	if(L->length>=MAXSIZE){
		printf("�ռ�����,�����ٲ�������\n");
        return FALSE; 
	}
	//�жϲ���λ�õĺϷ���
    if(i < 1 || i > L->length) {
        printf("����λ�ò���ȷ\n");
        return FALSE;
    }
    int j;
    for(j=L->length;j>=i;j--){
    	L->data[j+1]=L->data[j];//��iλ�ÿ�ʼ�������Ԫ�ض������ƶ�һλ
    }
    L->data[i-1]=e;
    L->length++;
    return TRUE;
}
```
### ɾ�����Ա��е�i��Ԫ��,�ɹ������1,��e������ֵ 
```
Status deleteList(SqList *L, int i, ElemType *e){
	//�ж����Ա��Ƿ�Ϊ��
    if(listEmpty(*L)){
        return ERROR;
    }
    //�ж�ɾ����λ���Ƿ�Ϸ�
    if(i < 1 || i > L->length) {
        printf("ɾ��λ�ò��Ϸ�\n");
        return ERROR;
    }
    *e=L->data[i-1];
    for(i;i<L->length;i++){
    	L->data[i-1]=L->data[i];//��iԪ�ؿ�ʼ����������ݶ���ǰ�ƶ�һλ    }
    L->length;
    return TRUE;
}
```
### �������Ա�
```
Status listTraverse(SqList L){
    int i;
    for(i = 0; i < L.length; i++){
        printf("%d ",L.data[i]);
    }
    printf("\n");
    return OK;
} 
```