### 同样的介绍在对应的Java文档里，这里就直接解析代码吧。
## 不过我们需要记住一点，C语言需要准确地去操作内存，也就是要操作到对应位置的内存数据，而不是像Java那样一个对象数据，对象名即引用。这样说的区别体现在哪里呢？？
### 也就是c中存给方法的是地址还是一个变量名的问题了！！
### 如果我们需要操作它的数据的，也就是要访问它的内存，所以需要它的引用，在c中就是需要它的指针。
### 如果我们只是想拿到它里面的数据，那么我们不需传指针地址过去，只需变量名。
*** 
### 准备数据
```
#include<stdio.h>
//定义常量 存储空间的初始化分配
#define MAXSIZE 20
#define TRUE 1
#define ERROR -1
#define FALSE 0
#define OK 1
//用typedef定义类型
typedef int Status;
typedef int ElemType;

//定义一个结构体类型
typedef struct{
    ElemType data[MAXSIZE];
    int length;
} SqList; 
```
### 初始化函数
```
Status initList(SqList *L){
	L->length = 0;
	return OK;
}
```
### 返回线性表的长度
```
Status getListLength(SqList L){
	return L.length;
}
```
### 线性表清空,长度为0 
```
Status clearList(SqList *L){
	L->length=0;
	return OK;
}
```
### 线性表为空返回true,否则返回false
```
Status listEmpty(SqList L){
	if(L.length==0){
		return TRUE;
	}
	return FALSE;
}
```
### 获取指定的元素的值,返回下标为i - 1的元素,赋值给e
```
Status getElem(SqList L,int i, ElemType *e){
	 //判断元素位置是否合法[i]
	 if(i<1||i>L.length){
	 	printf("查找的位置不正确 \n");
        return ERROR; 
	 }
	 //判断线性表是否为空
    if(listEmpty(L)){
        return ERROR;
    } 
    *e = L.data[i-1];
    return OK;
}
```
### 在线性表中查找指定的e相等的元素,如果查找成功,返回该元素的下标,否则返回ERROR
```
Status locateElem(SqList L,ElemType e){
	int i;
	for(i=0;i<L.length-1;i++){
		if(L.data[i]==e){
			return i;
		}
	}
	printf("没有查找到元素 %d 指定的下标\n",e);
	return ERROR;
}
```
### 自动创建 MAXSIZE 个元素,并赋值为0 
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
### 在线性表中第i个位置前插入新元素e
```
Status listInsert(SqList *L,int i, ElemType e){
	//判断长度是否可以允许插入新的数据
	if(L->length>=MAXSIZE){
		printf("空间已满,不能再插入数据\n");
        return FALSE; 
	}
	//判断插入位置的合法性
    if(i < 1 || i > L->length) {
        printf("插入位置不正确\n");
        return FALSE;
    }
    int j;
    for(j=L->length;j>=i;j--){
    	L->data[j+1]=L->data[j];//从i位置开始，后面的元素都往后移动一位
    }
    L->data[i-1]=e;
    L->length++;
    return TRUE;
}
```
### 删除线性表中第i个元素,成功后表长减1,用e返回其值 
```
Status deleteList(SqList *L, int i, ElemType *e){
	//判断线性表是否为空
    if(listEmpty(*L)){
        return ERROR;
    }
    //判断删除的位置是否合法
    if(i < 1 || i > L->length) {
        printf("删除位置不合法\n");
        return ERROR;
    }
    *e=L->data[i-1];
    for(i;i<L->length;i++){
    	L->data[i-1]=L->data[i];//从i元素开始，往后的数据都往前移动一位    }
    L->length;
    return TRUE;
}
```
### 遍历线性表
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