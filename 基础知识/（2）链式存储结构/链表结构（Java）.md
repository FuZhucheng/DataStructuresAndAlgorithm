## �������������ɣ�ÿ����㶼���������֣�1.�����򣬱���ý���ʵ�����ݣ�2.ָ���򱣴���һ�����ĵ�ַ����һ�ֶ�̬�洢����Ľṹ��ʽ���ɸ�����Ҫ��̬����������ڴ浥Ԫ��
### �ŵ㣺��˳�����ԣ������ɾ����ʱ��ʮ�ֿ죡��
### ȱ�㣺���ǲ����Լ��޸ĵ�ʱ����Ҫ����������㡣
***
### ׼�����ݣ�
```
class DATA2{
	String key;						// �������Ԫ�ص�������
	String name;
	int age;
}
//û��ͷ����������
class CLType{					//��������ṹ
	DATA2 nodeData=new DATA2();		//�������ݱ�����һ����DATA2��
	CLType nextNode;	//�Զ���洢�������á��������CLType,����nextNode������ָ����һ�����ģ�ÿ��׷�����¸�ֵ�����Դ���ǽ�����������ָ����һ�������
}
```
### ׷�ӽ�㣺
```
//׷��һ�����������β��.����Ϊ�෽����headΪ����ͷ���ã��������nodeDataΪ���Ҫ���������
public CLType CLAddEnd(CLtype head,DATA2 nodeData){
		CLType node,htemp;
		if(node=new CLType==null){
			System.out.println("��������ڴ�ʧ�ܣ���");
			return null;
		}else{
			node.nodeData=nodeData;//���������ݵ�����½���������
			node.nextNode = null;	//����ӵ��Ǹ�����ָ�����¿�
			if(head==null){
				head=node;//����ǽ���������һ�ε����ݲ��룬Ҳ���������ǲ����һ����㡣
				return head;
			}
			htemp=head;
			//���²�����ͷָ���Ѿ�ָ������˵Ľ�㣬Ҳ���ǵ�һ������������ˡ��������ͷָ��ָ��Ľ���htemp��ʹ�þֲ�����ѭ��
			//���������ĩβ�����ǲ�������Ľ�㣬�ҵ������Ǹ�����Ϊ�����Ǹ�����ָ������null��û��ָ��
			//��ȫ��������θ�ֵ��htemp��ֱ��htemp����ָ����Ϊ����ֹѭ�����ҵ������Ľ��
			while(head.nextNode!=null){
				htemp=htemp.nextNode;
			}
			htemp.nextNode=node;//�ҵ�����㣬�Ϳ��԰Ѵ��������½����Ҫ���������Ǹ����ǳ�ʼ���Ľ��node�����档
			return head;//����ͷָ��
		}
}
```
### ����ͷ��㣺
```
public CLType CLAddFirst(CLType head,DATA2 nodeData){
		CLType node;
		if(node=new CLType()==null){
			System.out.println("�����ڴ�ʧ�ܣ���");
			return null;
		}else{
			node.nodeData=nodeData;
			node.nextNode=head;//Ŀ���ǰ�ԭ���Ǹ��ս����Ƶ���һλ
			head=node; //�ܹؼ����ǰ�ԭ����ͷָ�������������趨Ϊͷ����ָ��
			return head;
		}
}
```
### ���ҽ�㣺
```
	public CLType CLFindNode(CLType head,String key){
		CLType htemp;
		htemp=head;
		while(htemp!=null){//�Ծֲ�����htemp��ѭ��������Ӱ�쵽ͷָ��
			if(htemp.nodeData.key.compareTo(key)==0){//�������̶ԱȽ���key�봫������key�������ͬ���ͷ���������
				return htemp;
			}
			htemp=htemp.nextNode;
		}
		return null;//����Ҳ������ͷ���null
	}
```
### �����㣺
```
	public CLType CLInsertNode(CLType head,String findkey,DATA2 nodeData){
		CLType node,nodetemp;
		if(node=new CLType()==null){
			System.out.println("�����ڴ�ʧ�ܣ���");
			return null;
		}
		node.nodeData=nodeData;
		nodetemp=CLFindeNode(head,findkey);//ʹ�÷������ҵ��ý��
		if(nodetemp!=null){
			node.nextNode = nodetemp.nextNode;//��������ָ����ָ�����ǲ��ҵ��Ľ�����һ�����������򣨾��ǲ��ҵ��Ľ���ָ��������
			nodetemp.nextNode=node;//�����ǲ��ҵ��Ľ���ָ������ָ���������������򣨾�������������������
		}else{
			System.out.println("δ�ҵ���ȷ�Ĳ���λ�ã�");
		}
		return head;
	}
```
### ɾ����㣺
```
	public int CLDeleteNode(CLType head,String key){
		CLType node,htemp;//node��ʾҪ���ҵĽ���ǰһ����㣬htemp��ʾҪ�鵽�Ľ�㣬������ָ�����ָ������һ�������
		htemp=head;
		node=head;
		while(htemp!=null){
			if(htemp.nodeData.keycompareTo(key)==0){
				node.nextNode=htemp.nextNode;	//���ҵ��Ǹ�Ҫɾ���Ľ��ʱ�������ҵ��Ľ���ָ���򣨾����ҵ��Ľ�����һ���������ã���ֵ��node��htemp��ǰһ����㣩��������������ɾ��������û���ڴ�
				htemp=null;//�ͷŽ���ڴ棬javaֻ����null�������Զ����������ý��л���
				return 1;
			}else{
				node=htemp;//ָ��ǰ�Ľ��
				htemp=htemp.nextNode;//ָ����һ�����
			}	
		}
		return 0;
	}
```
### ���㳤�ȣ�
```
	public int CLLength(CLType head){
		CLType htemp;
		htemp=head;
		int Len=0;
		while(htemp!=null){
			htemp=htemp.nextNode;
			Len++;
		}
		return Len;
	}
```
### ��ʾ���н�㣺
```
	//��ӡ��ȫ����������
	void CLAllNode(CLType head){
		CLType htemp;			
		DATA2 nodeData;
		htemp=head;
		System.out.printf("��ǰ������%d����㡣���������������£�\n",CLLength(head));
		while(htemp!=null){					
		//��ͷ��㸳ֵ��htemp��Ȼ����htemp�ֲ�������ѭ��������
		//�ڱ������̰ѽ�㸳ֵ���ֲ�����nodeData���д�ӡ��
		//Ȼ������nextNode����ָ��Ķ�������ָ������һ���������֣�����ֵ���ֲ�����htemp��htemp�ͱ�������һ�����Ķ�����htemp.Data����ȡ�õ���һ������������
			nodeData=htemp.nodeData;
			System.out.printf("���(%s,%s,%d)",nodeData.key,nodeData.name,nodeData.age);
			htemp=htemp.nextNode;				
		}
	}
```