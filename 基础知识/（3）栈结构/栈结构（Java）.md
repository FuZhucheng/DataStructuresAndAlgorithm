### ˳��ջ����ʹ��һ���ַ�������ڴ浥Ԫһ�α���ջ�е����ݡ�������һ��ָ����С�Ľṹ������Ϊջ�����Ϊ0��Ԫ�ؾ���ջ�ף��ٶ���һ������top����ջ����š�
### ��ʽջ����ʹ��������ʽ����ջ�и�Ԫ�ص�ֵ�������ײ���head������ָ��Ԫ�أ�Ϊջ��������β����ָ���ַnull��Ϊջ�ײ�
### ����ȳ�ԭ��

***
### ׼������
```
//˳��ջ�ṹ��ʵ��
class DATA3{
	String name;
	int age;
}
class StackType{
	static final int MAXLEN=50;					//����ջ�Ĵ�С
	DATA3[]data=new DATA3[MAXLEN+1];			//������ʵ�ִ洢����Ԫ��
	int top;									//ջ����־��ʼ�ձ�־ջ��
}
	
```
### ջ��ʼ����
```
StackType STInit(){						//��ʼ��ջ��С��ջ������ָ��ջ���ĵ�ַ
		StackType p;
		if((p=new StackType())!=null){			//����ջ�ڴ�
			p.top=0;							//����ջ��Ϊ0
			return p;							//����ָ��ջ��������
		}
		return null;							//����ʧ�ܷ���null
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
### ջ�пգ�
```
boolean STIsEmpty(StackType s){				//�ж�ջ�Ƿ�Ϊ��
		boolean t;								//����ǿ�ջ���ʾջû�����ݣ����Խ�����ջ�����������ɽ��г�ջ����
		t=(s.top==-1);
		return t;
	}
```
### ջ����
```
boolean STIsFull(StackType s){				//�ж�ջ�Ƿ�����
		boolean t;								//�������ջ�����ʾ��ջ�ṹû�ж���Ŀռ��������������ݣ���ʱ���ɽ�����ջ�������Գ�ջ
		t=(s.top==MAXLEN);
		return t;
	}
```
### ���ջ��
```
void STClear(StackType s){					//���ջ��
		s.top=-1;							//�������s��һ��ָ�������ջ�����ã���������ã����ڳ����У���ջ��top����Ϊ0����ʾִ�����ջ����
	}
```
### �ͷ�ջ�ڴ棺
```
void STFree(StackType s){				//�ͷ�ջ��ռ�õĿռ䡣��ʵ���ǰѶ������null���ڴ���ƾͻ�����
		if(s!=null){											
			s=null;
		}
}
```

### ��ջ����Push��
```
void PushST(StackType s,DATA3 data){
		if((s.top+1)>MAXLEN){					//���ж�ջ��top�����top���ڵ���SIZE�����ʾ���
			System.out.print("ջ�����\n");			//����top=top+1��ջ�����ü�1��ָ����ջ��ַ��
		}
		s.data[++s.top]=data;			//Ԫ����ջ
	}
```
### ��ջ����pop��
```
DATA3 PopST(StackType s){					
		if(s.top==-1){								//�ж�ջ��top�����topΪ0�����ʾΪ��ջ�����г�����
													//��ջ������top��ָλ�õ�Ԫ�ط��أ�����top=top-1��Ҳ����ʹ��ջ�����ü�1��ָ��ջ����һ��Ԫ�أ�ԭ��ջ��Ԫ�ر�����
			System.out.print("ջΪ�գ�\n");				
			System.exit(0);
		}
		return (s.data[s.top--]);				//����ջ��top����ǣ�ʹtop-1��Ȼ�󷵻����Ҫ��ջ�Ľ�㡣����ִ�������Ϊ�Ǻ�--�ģ����Ա�����ջ��ͼ�ȥ��ջ���Ľ�㣬���Ծ����������ĳ�ջ������
	}
```
### ��ȡջ�����ݣ�
```
DATA3 PeekST(StackType s){				//����ջ�ṹֻ����һ�ν��в��������Զ�ȡ�������Ƕ�ȡջ���Ľ������
		if(s.top==-1){						
			System.out.print("ջΪ�գ�\n");
			System.out.print(0);
		}
		return (s.data[s.top]);				//��������ֵ��һ��DATA3���͵����ݣ�����ֵ��ջ��������Ԫ�أ�ջ����㣩
	}
```
