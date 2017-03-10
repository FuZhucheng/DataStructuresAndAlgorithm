## 顺序表其实就是按照顺序存储方式存储的线性表。结点按照逻辑次序依次存放在计算机的一组连续的存储单元中。
### 优点：可快速查找以及修改
### 缺点：（1）在插入或删除结点的时候，需要移动大量数据；（2）如果表比较大时，又是难以分配足够的连续存储空间，导致内存分配失败，无法存储。
***
### 准备数据：
```
//这是一个线性结构顺序存储结构的实例，也就是利用数组来实现的线性表的顺序存储结构
class DATA {
	String key; //学号						// 结点数据元素的数据项
	String name;//名字
	int age;	//年龄
}
class SLType { 											// 定义以数组来实现的线性表顺序存储结构
	static final int MAXLEN = 100;					 // 设置顺序表的最大长度
	DATA[] ListData = new DATA[MAXLEN + 1]; 		// 保存顺序表的结构数组
	int ListLen; 									// 顺序表已存结点的数量
}
```
### 初始化顺序表：
```
public void SLInit(SLtype SL){
	Sl.ListLen = 0;
}
```
### 获取顺序表长度
```
public int SLLength(SLtype SL){
	return SL.ListLen;
}
```
### 插入结点：
```
// 插入操作,就是把一个新结点插到n的位置，原顺序表n位置以后包括n都往后移动一位
public int SLInsert(SLtype SL,int n,DATA data){
	int i;
	if(SL.Listlen > MAXLEN){
		System.out.println("顺序表已经满了，不能再插入！")；
		return 0;
	}
	if(n<1||n>SL.ListLen-1){
		System.out.println("插入位置不正确！！")；
		return 0;
	}
	for(i=SL.ListLen;i>=n;i--){ // 将顺序表从后面开始移动，遍历到n那个位置所代表的位置，将n所代表的位置的数值也往后移动一位
			SL.ListData[i+1]=SL.ListData[i];
	}
	SL.ListData[n]=data;// 插入结点
	SL.ListLen++;// 顺序表结点数量增加1
	return 1;
}
```
### 追加结点：
```
	public int SLAdd(SLType SL,data){
		if(SL.ListLen >= MAXLEN){
			System.out.println("顺序表已经满了，不能再加结点！");
			return 0;
		}
		SL.ListData[++SL.ListLen]=data;//顺序表没满就在最后的结点位置+1，在那个位置set进data
		return 1;
	}
```
### 删除结点：
```
public int SLDelete(SLType SL,int n){
		int i;
		if(n<1||n>SL.ListLen+1){
			System.out.println("删除位置不正确！！");
		}
		for(i=n;i<SL.ListLen;i++){
			SL.ListData[i]=SL.ListData[i+1];//直接访问到该数组的n下标，把他的后一个位置的结点数据赋给n下标所在的结点来删除那个数据元素
		}
		SL.ListLen--;//顺序表元素数量减1
		return 1;
}
```
### 查找结点：
```
//直接访问结点
	//查询方法，根据序号返回数据元素，查询一个结点，返回一个结点
public DATA SLFindByNum(SLType SL,int n){
		if(n<1||n>SL.ListLen+1){
			System.out.println("结点序号错误，不能返回结点！");
		}
		return SL.ListData[n];
}
```
```
//根据关键字查找结点
public DATA SLFindByKey(SLType SL,String key){
		int i;
		for(i=1;i<=SL.ListLen;i++){
			if(SL.ListData[i].key.compareTo(key)==0){//找到那个结点的话就返回该结点的下标序号
				return i;
			}
		}
		return 0;
}
```
### 显示所有结点：
```
	//打印出全部这个顺序表中的信息
	int SLAll(SLType SL){
		int i;
		for(i=1;i<=SL.ListLen;i++){
			System.out.printf("(%s,%s,%d)\n", SL.ListData[i].key,SL.ListData[i].name,SL.ListData[i].age);		
			
		}
		return 0;
	}
	
```

