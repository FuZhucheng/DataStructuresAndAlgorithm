## ˳�����ʵ���ǰ���˳��洢��ʽ�洢�����Ա���㰴���߼��������δ���ڼ������һ�������Ĵ洢��Ԫ�С�
### �ŵ㣺�ɿ��ٲ����Լ��޸�
### ȱ�㣺��1���ڲ����ɾ������ʱ����Ҫ�ƶ��������ݣ���2�������Ƚϴ�ʱ���������Է����㹻�������洢�ռ䣬�����ڴ����ʧ�ܣ��޷��洢��
***
### ׼�����ݣ�
```
//����һ�����Խṹ˳��洢�ṹ��ʵ����Ҳ��������������ʵ�ֵ����Ա��˳��洢�ṹ
class DATA {
	String key; //ѧ��						// �������Ԫ�ص�������
	String name;//����
	int age;	//����
}
class SLType { 											// ������������ʵ�ֵ����Ա�˳��洢�ṹ
	static final int MAXLEN = 100;					 // ����˳������󳤶�
	DATA[] ListData = new DATA[MAXLEN + 1]; 		// ����˳���Ľṹ����
	int ListLen; 									// ˳����Ѵ��������
}
```
### ��ʼ��˳���
```
public void SLInit(SLtype SL){
	Sl.ListLen = 0;
}
```
### ��ȡ˳�����
```
public int SLLength(SLtype SL){
	return SL.ListLen;
}
```
### �����㣺
```
// �������,���ǰ�һ���½��嵽n��λ�ã�ԭ˳���nλ���Ժ����n�������ƶ�һλ
public int SLInsert(SLtype SL,int n,DATA data){
	int i;
	if(SL.Listlen > MAXLEN){
		System.out.println("˳����Ѿ����ˣ������ٲ��룡")��
		return 0;
	}
	if(n<1||n>SL.ListLen-1){
		System.out.println("����λ�ò���ȷ����")��
		return 0;
	}
	for(i=SL.ListLen;i>=n;i--){ // ��˳���Ӻ��濪ʼ�ƶ���������n�Ǹ�λ���������λ�ã���n�������λ�õ���ֵҲ�����ƶ�һλ
			SL.ListData[i+1]=SL.ListData[i];
	}
	SL.ListData[n]=data;// ������
	SL.ListLen++;// ˳�������������1
	return 1;
}
```
### ׷�ӽ�㣺
```
	public int SLAdd(SLType SL,data){
		if(SL.ListLen >= MAXLEN){
			System.out.println("˳����Ѿ����ˣ������ټӽ�㣡");
			return 0;
		}
		SL.ListData[++SL.ListLen]=data;//˳���û���������Ľ��λ��+1�����Ǹ�λ��set��data
		return 1;
	}
```
### ɾ����㣺
```
public int SLDelete(SLType SL,int n){
		int i;
		if(n<1||n>SL.ListLen+1){
			System.out.println("ɾ��λ�ò���ȷ����");
		}
		for(i=n;i<SL.ListLen;i++){
			SL.ListData[i]=SL.ListData[i+1];//ֱ�ӷ��ʵ��������n�±꣬�����ĺ�һ��λ�õĽ�����ݸ���n�±����ڵĽ����ɾ���Ǹ�����Ԫ��
		}
		SL.ListLen--;//˳���Ԫ��������1
		return 1;
}
```
### ���ҽ�㣺
```
//ֱ�ӷ��ʽ��
	//��ѯ������������ŷ�������Ԫ�أ���ѯһ����㣬����һ�����
public DATA SLFindByNum(SLType SL,int n){
		if(n<1||n>SL.ListLen+1){
			System.out.println("�����Ŵ��󣬲��ܷ��ؽ�㣡");
		}
		return SL.ListData[n];
}
```
```
//���ݹؼ��ֲ��ҽ��
public DATA SLFindByKey(SLType SL,String key){
		int i;
		for(i=1;i<=SL.ListLen;i++){
			if(SL.ListData[i].key.compareTo(key)==0){//�ҵ��Ǹ����Ļ��ͷ��ظý����±����
				return i;
			}
		}
		return 0;
}
```
### ��ʾ���н�㣺
```
	//��ӡ��ȫ�����˳����е���Ϣ
	int SLAll(SLType SL){
		int i;
		for(i=1;i<=SL.ListLen;i++){
			System.out.printf("(%s,%s,%d)\n", SL.ListData[i].key,SL.ListData[i].name,SL.ListData[i].age);		
			
		}
		return 0;
	}
	
```

